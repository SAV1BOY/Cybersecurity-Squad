# Common Log Analysis Queries

## Purpose

Provide ready-to-use log analysis queries for common security investigation scenarios across major SIEM platforms (Splunk SPL, Elastic/OpenSearch KQL, and cloud-native query languages). These queries cover authentication anomalies, lateral movement, data exfiltration, persistence, and other attacker techniques commonly encountered during incident response and threat hunting.

## Platforms Covered
- Splunk (SPL)
- Elastic/OpenSearch (KQL/Lucene)
- AWS CloudWatch Logs Insights
- Microsoft Sentinel (KQL)

---

## Authentication and Credential Attacks

### Failed Login Brute Force Detection

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count by src_ip, TargetUserName
| where count > 10
| sort -count
```

**Elastic KQL:**
```
event.code: "4625" | stats count(*) by source.ip, user.name | where count > 10
```

**Sentinel KQL:**
```kusto
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts=count() by IpAddress, TargetAccount, bin(TimeGenerated, 1h)
| where FailedAttempts > 10
| order by FailedAttempts desc
```

### Password Spray Detection
Multiple accounts targeted from single source with low attempt count per account:

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=30m
| stats dc(TargetUserName) as unique_users, count by src_ip, _time
| where unique_users > 5 AND count < (unique_users * 3)
```

**Sentinel KQL:**
```kusto
SecurityEvent
| where EventID == 4625
| summarize UniqueUsers=dcount(TargetAccount), Attempts=count() by IpAddress, bin(TimeGenerated, 30m)
| where UniqueUsers > 5 and Attempts < UniqueUsers * 3
```

### Impossible Travel (Login from Geographically Distant Locations)

**Splunk:**
```spl
index=authentication action=success
| iplocation src_ip
| sort user, _time
| streamstats current=f last(City) as prev_city, last(_time) as prev_time by user
| eval time_diff_hours=(_time - prev_time)/3600
| where time_diff_hours < 2 AND City!=prev_city AND isnotnull(prev_city)
```

### Kerberoasting Detection (TGS Requests for Service Accounts)

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4769 TicketEncryptionType=0x17
| stats count by ServiceName, TargetUserName, IpAddress
| where count > 3
```

**Sentinel KQL:**
```kusto
SecurityEvent
| where EventID == 4769 and TicketEncryptionType == "0x17"
| where ServiceName !endswith "$"
| summarize Count=count() by ServiceName, TargetAccount, IpAddress
| where Count > 3
```

### DCSync Detection

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4662
| where ObjectType="*domainDNS*" AND (Properties="*1131f6aa*" OR Properties="*1131f6ad*" OR Properties="*89e95b76*")
| table _time, SubjectUserName, SubjectDomainName, ObjectName
```

## Lateral Movement

### PsExec-Style Remote Execution

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4648
| where TargetServerName!="localhost"
| stats count by SubjectUserName, TargetServerName
| where count > 3
| sort -count
```

### WMI Remote Execution

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=1 ParentImage="*wmiprvse.exe"
| where Image!="*\\WmiApSrv.exe" AND Image!="*\\WmiPrvSE.exe"
| table _time, Computer, User, ParentImage, Image, CommandLine
```

### RDP Lateral Movement

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4624 LogonType=10
| stats count, values(TargetUserName) as users by IpAddress
| where count > 3
| sort -count
```

**Sentinel KQL:**
```kusto
SecurityEvent
| where EventID == 4624 and LogonType == 10
| summarize RDPSessions=count(), Users=make_set(TargetAccount) by IpAddress, bin(TimeGenerated, 1h)
| where RDPSessions > 3
```

### SMB Share Access Enumeration

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=5140
| stats dc(ShareName) as unique_shares, count by SubjectUserName, IpAddress
| where unique_shares > 5
| sort -unique_shares
```

## Data Exfiltration

### Large Outbound Data Transfers

**Splunk (proxy logs):**
```spl
index=proxy
| stats sum(bytes_out) as total_bytes by src_ip, dest_host
| eval MB=round(total_bytes/1024/1024,2)
| where MB > 100
| sort -MB
```

### DNS Tunneling Detection (High-Entropy Subdomains)

**Splunk:**
```spl
index=dns query_type=A
| eval subdomain=mvindex(split(query,"."),0)
| eval length=len(subdomain)
| where length > 30
| stats count by query, src_ip
| where count > 10
| sort -count
```

### Cloud Storage Upload Detection

**Splunk (proxy):**
```spl
index=proxy http_method=POST
| where match(dest_host, "(mega\.nz|dropbox\.com|drive\.google\.com|onedrive\.live\.com|upload\.box\.com|rclone)")
| stats count, sum(bytes_out) as total_bytes by src_ip, dest_host, user
| eval MB=round(total_bytes/1024/1024,2)
| sort -MB
```

### Email Forwarding Rule Detection (BEC)

**Splunk (Exchange/O365):**
```spl
index=o365 Operation="New-InboxRule" OR Operation="Set-InboxRule"
| where ForwardTo!="" OR ForwardAsAttachmentTo!="" OR RedirectTo!=""
| table _time, UserId, Operation, ForwardTo, RedirectTo, Name
```

**Sentinel KQL:**
```kusto
OfficeActivity
| where Operation in ("New-InboxRule", "Set-InboxRule")
| where Parameters has "ForwardTo" or Parameters has "RedirectTo"
| project TimeGenerated, UserId, Operation, Parameters
```

## Persistence

### New Service Creation

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=7045
| table _time, Computer, ServiceName, ImagePath, ServiceType, AccountName
| where NOT match(ServiceName, "(Windows|Microsoft|Defender|Update)")
```

### Scheduled Task Creation

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=1 Image="*schtasks.exe" CommandLine="*/create*"
| table _time, Computer, User, CommandLine
| where NOT match(CommandLine, "(Microsoft|Windows|Defender)")
```

### Registry Run Key Modification

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=13
| where TargetObject="*\\CurrentVersion\\Run*" OR TargetObject="*\\CurrentVersion\\RunOnce*"
| table _time, Computer, User, TargetObject, Details
```

### New Local Account Creation

**Splunk:**
```spl
index=windows sourcetype=WinEventLog:Security EventCode=4720
| table _time, Computer, SubjectUserName, TargetUserName, SubjectDomainName
```

## Cloud-Specific Queries

### AWS: Unauthorized API Calls

**CloudWatch Logs Insights:**
```
fields @timestamp, userIdentity.arn, eventName, errorCode, sourceIPAddress
| filter errorCode = "AccessDenied" or errorCode = "UnauthorizedAccess"
| stats count by userIdentity.arn, eventName, sourceIPAddress
| sort count desc
```

### AWS: Console Login Without MFA

**CloudWatch Logs Insights:**
```
fields @timestamp, userIdentity.arn, sourceIPAddress, responseElements.ConsoleLogin
| filter eventName = "ConsoleLogin" and additionalEventData.MFAUsed = "No"
| sort @timestamp desc
```

### AWS: S3 Bucket Policy Changes

**CloudWatch Logs Insights:**
```
fields @timestamp, userIdentity.arn, eventName, requestParameters.bucketName
| filter eventName in ["PutBucketPolicy", "PutBucketAcl", "DeleteBucketPolicy", "PutBucketPublicAccessBlock"]
| sort @timestamp desc
```

### AWS: IAM Privilege Escalation

**CloudWatch Logs Insights:**
```
fields @timestamp, userIdentity.arn, eventName, sourceIPAddress
| filter eventName in ["CreatePolicyVersion", "SetDefaultPolicyVersion", "AttachUserPolicy", "AttachRolePolicy", "PutUserPolicy", "PutRolePolicy", "AddUserToGroup", "CreateLoginProfile", "UpdateLoginProfile", "CreateAccessKey"]
| sort @timestamp desc
```

## Threat Hunting Queries

### Process Execution from Unusual Locations

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=1
| where match(Image, "(\\Temp\\|\\Downloads\\|\\AppData\\Local\\|\\ProgramData\\|\\Users\\Public\\)")
| where NOT match(Image, "(chrome|firefox|teams|slack|zoom|onedrive)")
| stats count by Image, Computer
| sort -count
```

### Encoded PowerShell Commands

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=1 Image="*powershell*"
| where match(CommandLine, "(-enc|-EncodedCommand|-e )")
| table _time, Computer, User, CommandLine
```

### Living-Off-The-Land Binary (LOLBin) Usage

**Splunk (Sysmon):**
```spl
index=sysmon EventCode=1
| where match(Image, "(certutil|mshta|regsvr32|rundll32|msiexec|wscript|cscript|bitsadmin)\.exe")
| where match(CommandLine, "(http|ftp|\\\\|/download|/transfer|-decode|-encode|-urlcache)")
| table _time, Computer, User, Image, CommandLine, ParentImage
```

## Usage Notes

- Adjust index names, sourcetypes, and field names to match your SIEM configuration
- Time ranges should be specified appropriate to the investigation
- Test queries in non-production before using at scale
- High-volume queries may need optimization (add time constraints, use tstats)
- Tune thresholds based on your environment's baseline

## Cross-References

- `tasks/forensics/network-forensics.md` — Network-level analysis
- `scripts/detection-rule-templates.md` — Converting queries to detection rules
- `workflows/threat-hunting-sprint-workflow.md` — Using queries for threat hunting
- `workflows/detection-engineering-workflow.md` — Query-to-rule pipeline
- `tasks/threat-intel/ioc-enrichment.md` — IOC-based query generation
