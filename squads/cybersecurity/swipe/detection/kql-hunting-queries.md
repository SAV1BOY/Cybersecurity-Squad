# KQL Hunting Queries for Microsoft Sentinel

## Purpose

Kusto Query Language (KQL) queries for threat hunting in Microsoft Sentinel. Covers authentication anomalies, data exfiltration, persistence mechanisms, and lateral movement detection.

## Authentication Anomalies

### Query 1: Impossible Travel Detection

```kql
// Detect logins from geographically impossible locations
// Logic: Two successful logins from different countries within timeframe
// that would require travel faster than possible

let timeWindow = 1h;
let maxTravelSpeedKmH = 900; // Approximate max commercial flight speed
SigninLogs
| where ResultType == 0  // Successful sign-ins only
| where isnotempty(LocationDetails.city)
| extend City = tostring(LocationDetails.city),
         Country = tostring(LocationDetails.countryOrRegion),
         Latitude = todouble(LocationDetails.geoCoordinates.latitude),
         Longitude = todouble(LocationDetails.geoCoordinates.longitude)
| sort by UserPrincipalName, TimeGenerated
| serialize
| extend PrevTime = prev(TimeGenerated, 1),
         PrevCity = prev(City, 1),
         PrevCountry = prev(Country, 1),
         PrevLat = prev(Latitude, 1),
         PrevLon = prev(Longitude, 1),
         PrevUser = prev(UserPrincipalName, 1)
| where UserPrincipalName == PrevUser
| where Country != PrevCountry
| extend TimeDiffMinutes = datetime_diff('minute', TimeGenerated, PrevTime)
| where TimeDiffMinutes > 0 and TimeDiffMinutes < 60 * 24  // Within 24 hours
| extend DistanceKm = geo_distance_2points(Longitude, Latitude, PrevLon, PrevLat) / 1000
| extend RequiredSpeedKmH = DistanceKm / (TimeDiffMinutes / 60.0)
| where RequiredSpeedKmH > maxTravelSpeedKmH
| project TimeGenerated, UserPrincipalName,
          FromCity = PrevCity, FromCountry = PrevCountry,
          ToCity = City, ToCountry = Country,
          TimeDiffMinutes, DistanceKm,
          RequiredSpeedKmH, IPAddress
| sort by RequiredSpeedKmH desc

// Tuning Notes:
// - Exclude known VPN exit points that appear in multiple countries
// - Exclude service accounts and automation identities
// - Adjust maxTravelSpeedKmH based on tolerance
// - Consider adding ConditionalAccessStatus filtering
```

### Query 2: Password Spray Detection

```kql
// Detect password spray attacks: single password tried against many accounts
// Pattern: Many failed logins from same IP, different usernames, same error code

let timeWindow = 30m;
let failureThreshold = 15;
SigninLogs
| where TimeGenerated > ago(timeWindow)
| where ResultType != 0  // Failed sign-ins
| where ResultType in (50126, 50053, 50055)  // Invalid password error codes
| summarize
    FailedAttempts = count(),
    DistinctUsers = dcount(UserPrincipalName),
    TargetUsers = make_set(UserPrincipalName, 50),
    DistinctApps = dcount(AppDisplayName),
    FirstAttempt = min(TimeGenerated),
    LastAttempt = max(TimeGenerated)
    by IPAddress
| where DistinctUsers > failureThreshold
| where DistinctUsers > FailedAttempts * 0.6  // High user-to-attempt ratio = spray
| extend DurationMinutes = datetime_diff('minute', LastAttempt, FirstAttempt)
| sort by DistinctUsers desc
| project IPAddress, DistinctUsers, FailedAttempts,
          DurationMinutes, FirstAttempt, LastAttempt,
          DistinctApps, TargetUsers

// Tuning Notes:
// - Adjust failureThreshold based on organization size
// - Filter known load balancer or proxy IPs (they aggregate users)
// - Check if any targeted users subsequently had successful logins
// - Cross-reference IP with threat intelligence
```

### Query 3: MFA Fatigue / Push Bombing

```kql
// Detect MFA push bombing: rapid repeated MFA prompts to user
// Attacker has valid credentials, spamming MFA prompts hoping user accepts

let timeWindow = 10m;
let promptThreshold = 5;
AADNonInteractiveUserSignInLogs
| union SigninLogs
| where TimeGenerated > ago(1d)
| where ResultType == 50074  // MFA required
    or ResultType == 500121  // Strong auth required
    or Status.additionalDetails has "MFA"
| summarize
    MFAPrompts = count(),
    DistinctIPs = dcount(IPAddress),
    IPs = make_set(IPAddress, 10),
    FirstPrompt = min(TimeGenerated),
    LastPrompt = max(TimeGenerated)
    by UserPrincipalName, bin(TimeGenerated, timeWindow)
| where MFAPrompts >= promptThreshold
| extend DurationMinutes = datetime_diff('minute', LastPrompt, FirstPrompt)
| sort by MFAPrompts desc
| project UserPrincipalName, MFAPrompts, DurationMinutes,
          DistinctIPs, IPs, FirstPrompt, LastPrompt

// Follow-up: Check if user eventually approved MFA
// | join kind=inner (
//     SigninLogs | where ResultType == 0
// ) on UserPrincipalName
```

## Data Exfiltration Detection

### Query 4: Unusual Large File Downloads from SharePoint/OneDrive

```kql
// Detect abnormal volume of file downloads from SharePoint/OneDrive
// Compares against user's 30-day baseline

let lookbackDays = 30;
let baselineEnd = ago(1d);
let baselineStart = ago(lookbackDays);
let detectionWindow = 1d;
// Build baseline
let baseline = OfficeActivity
| where TimeGenerated between (baselineStart .. baselineEnd)
| where Operation in ("FileDownloaded", "FileSyncDownloadedFull")
| where RecordType == "SharePointFileOperation"
| summarize
    BaselineAvgDaily = count() / lookbackDays,
    BaselineStdDev = stdev(count()) ,
    BaselineMaxDaily = max(count())
    by UserId;
// Current activity
OfficeActivity
| where TimeGenerated > ago(detectionWindow)
| where Operation in ("FileDownloaded", "FileSyncDownloadedFull")
| where RecordType == "SharePointFileOperation"
| summarize
    TodayDownloads = count(),
    DistinctFiles = dcount(OfficeObjectId),
    TotalSizeMB = sum(toint(OfficeObjectId)) / 1048576,  // Approximate
    Sites = make_set(Site_Url, 10)
    by UserId
| join kind=leftouter baseline on UserId
| extend Anomaly = TodayDownloads > (BaselineAvgDaily * 5)  // 5x baseline
| where Anomaly == true or TodayDownloads > 100
| sort by TodayDownloads desc
| project UserId, TodayDownloads, DistinctFiles,
          BaselineAvgDaily, Sites

// Tuning Notes:
// - Exclude known bulk sync operations and backup accounts
// - Adjust multiplier (5x) based on environment
// - Correlate with HR data for departing employees
```

### Query 5: DNS Tunneling Detection

```kql
// Detect potential DNS tunneling: high-entropy or high-volume DNS queries
// to single domain, unusually long subdomain labels

DnsEvents
| where TimeGenerated > ago(1h)
| where QueryType in ("A", "AAAA", "TXT", "CNAME", "MX")
| extend DomainParts = split(Name, ".")
| extend SubdomainLength = strlen(tostring(DomainParts[0]))
| extend TotalLength = strlen(Name)
| extend BaseDomain = strcat(tostring(DomainParts[-2]), ".", tostring(DomainParts[-1]))
| summarize
    QueryCount = count(),
    AvgSubdomainLength = avg(SubdomainLength),
    MaxSubdomainLength = max(SubdomainLength),
    DistinctSubdomains = dcount(Name),
    TotalDataBytes = sum(TotalLength),
    DistinctClients = dcount(ClientIP),
    Clients = make_set(ClientIP, 10)
    by BaseDomain
| where AvgSubdomainLength > 20       // Long subdomain labels
    or DistinctSubdomains > 100        // Many unique subdomains
    or MaxSubdomainLength > 50         // Very long single query
| where QueryCount > 50               // Minimum volume
| sort by DistinctSubdomains desc
| project BaseDomain, QueryCount, DistinctSubdomains,
          AvgSubdomainLength, MaxSubdomainLength,
          TotalDataBytes, DistinctClients, Clients

// Tuning Notes:
// - Allowlist CDN domains (akamai, cloudfront, etc.) that have long subdomains
// - TXT queries with base64 content are strong indicators
// - Correlate with threat intelligence domain feeds
// - Check if BaseDomain is recently registered (DGA detection)
```

## Persistence Detection

### Query 6: New Service Principal or App Registration

```kql
// Detect creation of new Azure AD service principals or app registrations
// Attackers create these for persistent API access

AuditLogs
| where TimeGenerated > ago(24h)
| where OperationName in (
    "Add service principal",
    "Add application",
    "Add service principal credentials",
    "Update application - Certificates and secrets management"
)
| extend InitiatedBy = tostring(InitiatedBy.user.userPrincipalName)
| extend TargetApp = tostring(TargetResources[0].displayName)
| extend TargetAppId = tostring(TargetResources[0].id)
| extend ModifiedProperties = TargetResources[0].modifiedProperties
| project TimeGenerated, OperationName, InitiatedBy,
          TargetApp, TargetAppId, ModifiedProperties,
          CorrelationId
| sort by TimeGenerated desc

// Tuning Notes:
// - Baseline normal app registration patterns for your org
// - Alert on credential additions to existing service principals
// - High-privilege API permissions (Directory.ReadWrite.All) are critical
// - Correlate with sign-in logs for the initiating user
```

### Query 7: Inbox Rule Creation (Persistence/Evasion)

```kql
// Detect creation of email inbox rules that forward or delete email
// Common in BEC attacks to hide activity

OfficeActivity
| where TimeGenerated > ago(24h)
| where Operation in ("New-InboxRule", "Set-InboxRule", "Enable-InboxRule")
| extend RuleName = tostring(parse_json(Parameters)[0].Value)
| extend RuleCondition = tostring(Parameters)
| where RuleCondition has_any ("ForwardTo", "RedirectTo", "DeleteMessage",
                                "ForwardAsAttachmentTo", "MoveToFolder")
| project TimeGenerated, UserId, Operation, RuleName,
          RuleCondition, ClientIP, SessionId
| sort by TimeGenerated desc

// Tuning Notes:
// - Legitimate forwarding rules exist, but auto-delete rules are suspicious
// - External forwarding is higher risk than internal
// - Cross-reference with sign-in anomalies for the user
// - Check for rules that hide emails containing keywords like "invoice", "payment"
```

## Lateral Movement Detection

### Query 8: Remote Service Creation

```kql
// Detect remote service creation events indicating lateral movement
// (PsExec-like behavior)

SecurityEvent
| where TimeGenerated > ago(24h)
| where EventID == 7045  // New service installed
| where ServiceName !in ("Windows Defender", "WinDefend", "MsMpSvc")
| extend ServiceStartType = case(
    ServiceStartType == "0", "Boot",
    ServiceStartType == "1", "System",
    ServiceStartType == "2", "Automatic",
    ServiceStartType == "3", "Manual",
    ServiceStartType == "4", "Disabled",
    ServiceStartType)
| where ServiceFileName has_any ("cmd", "powershell", "psexec",
                                   "ADMIN$", "\\\\", "temp", "tmp")
    or ServiceName has_any ("PSEXE", "csexec", "paexec", "BTOBTO")
| project TimeGenerated, Computer, ServiceName,
          ServiceFileName, ServiceStartType, Account,
          SubjectLogonId
| sort by TimeGenerated desc

// Tuning Notes:
// - Correlate with EventID 4624 (logon) to identify source machine
// - Filter known management tool service names
// - ServiceFileName containing UNC paths (\\) is suspicious
// - Combine with network connection data for full picture
```

## Query Performance Guidelines

| Technique | Impact | Example |
|-----------|--------|---------|
| Time filtering first | Major | `where TimeGenerated > ago(1h)` at top |
| Specific table selection | Major | Use exact table vs `search` |
| Column projection | Moderate | `project` only needed columns |
| Summarize before join | Major | Reduce dataset before join operations |
| has vs contains | Moderate | `has` is word-boundary, faster |
| materialize() | Major | Cache intermediate results |
| Limit result sets | Minor | `take 1000` for exploration |

## Cross-References

- [Sigma Rule Examples](sigma-rule-examples.md) -- platform-agnostic detection
- [SPL Hunting Queries](spl-hunting-queries.md) -- Splunk equivalent queries
- [Detection Coverage Matrix](../../frameworks/detection-coverage-matrix.md) -- coverage mapping
- [BEC Runbook](../runbooks/business-email-compromise-runbook.md) -- email-specific response
