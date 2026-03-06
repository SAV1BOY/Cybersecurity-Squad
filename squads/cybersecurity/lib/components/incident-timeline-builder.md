# Incident Timeline Construction Guide

## Purpose

Provide a structured methodology for building accurate, comprehensive incident timelines by correlating events from multiple data sources. A well-constructed timeline is the backbone of incident investigation, root cause analysis, legal proceedings, and post-incident improvement. It answers the fundamental questions: what happened, when, how, and in what order.

## When to Use
- Active incident response (building timeline in real-time)
- Post-incident forensic analysis
- Legal and regulatory proceedings preparation
- Lessons-learned reviews
- Red team/purple team exercise analysis

---

## Timeline Fundamentals

### Time Synchronization
Before correlating events across sources, normalize all timestamps:
- [ ] Identify timezone for each data source (UTC preferred)
- [ ] Document clock skew between systems (NTP compliance status)
- [ ] Convert all timestamps to a single reference timezone (UTC recommended)
- [ ] Note any gaps in time coverage (log rotation, storage limits, clock drift)
- [ ] Flag timestamps with uncertainty (estimated events, manual entries)

### Timestamp Precision

| Source | Typical Precision | Reliability |
|--------|------------------|-------------|
| SIEM events | Millisecond | High (NTP-synced) |
| Windows Event Log | Second | High (if NTP configured) |
| Network packet captures | Microsecond | Very High |
| Cloud API logs (CloudTrail) | Second | High |
| Email headers | Second | Medium (relay delays) |
| Badge access logs | Second | High |
| Firewall logs | Second | High |
| Manual observations | Minute | Low (human recall) |

## Data Source Integration

### 2.1 Source Inventory
For each incident, identify all potentially relevant data sources:

**Endpoint Sources:**
- [ ] Windows Security Event Log (authentication, process, privilege events)
- [ ] Sysmon logs (process creation, network, file, registry)
- [ ] PowerShell Script Block Logging
- [ ] EDR telemetry (process tree, file operations, network connections)
- [ ] Antivirus/anti-malware logs
- [ ] Prefetch files (program execution history)
- [ ] Browser history and download logs
- [ ] Application logs

**Network Sources:**
- [ ] Firewall logs (accept/deny decisions, NAT translations)
- [ ] Proxy/web filter logs (URLs, user agents, bytes transferred)
- [ ] DNS query logs (resolution requests and responses)
- [ ] IDS/IPS alerts (signature matches)
- [ ] NDR telemetry (traffic metadata, anomaly detection)
- [ ] VPN logs (connection establishment, source IPs)
- [ ] DHCP logs (IP-to-MAC mapping)
- [ ] Packet captures (if available for incident window)

**Identity Sources:**
- [ ] Active Directory logs (authentication, group changes, GPO)
- [ ] IdP/SSO logs (SAML assertions, OIDC tokens)
- [ ] MFA logs (challenges, successes, failures)
- [ ] PAM logs (privileged access sessions)
- [ ] Badge/physical access logs

**Cloud Sources:**
- [ ] CloudTrail / Activity Log / Audit Log (API calls)
- [ ] VPC Flow Logs / NSG Flow Logs
- [ ] Cloud-native security alerts (GuardDuty, Defender, SCC)
- [ ] Load balancer access logs
- [ ] S3/Blob access logs

**Application Sources:**
- [ ] Application audit logs
- [ ] Database query logs
- [ ] Email server/gateway logs
- [ ] DLP alerts
- [ ] WAF logs

**External Sources:**
- [ ] Threat intelligence (IOC timestamps, campaign timelines)
- [ ] Vendor notifications (when were we notified?)
- [ ] Third-party reports (when did external parties detect?)

## Timeline Entry Format

### Standard Entry Structure
Each timeline entry should contain:

```
TIMESTAMP (UTC) | SOURCE | SYSTEM | ACTOR | ACTION | DETAIL | EVIDENCE REF

2026-03-05 14:32:17 | EDR | WS-FIN-042 | user.jsmith | Process Create |
  powershell.exe -enc [BASE64] launched by outlook.exe |
  EDR Alert #4521, Sysmon EventID 1
```

### Entry Categories
Color-code or tag entries by category for visual clarity:

| Category | Tag | Color | Examples |
|----------|-----|-------|---------|
| Attacker Action | [ATK] | Red | Exploitation, lateral movement, data staging |
| Defender Action | [DEF] | Blue | Alert, containment, remediation |
| System Event | [SYS] | Gray | Automated backups, scheduled tasks, updates |
| User Action | [USR] | Green | Legitimate user activity providing context |
| Intelligence | [INT] | Purple | Threat intel correlation, IOC match |
| Communication | [COM] | Orange | Notifications, escalations, decisions |

## Building the Timeline

### Step 1: Anchor Events
Start with known, high-confidence events:
- [ ] Initial detection alert (when did we first know something was wrong?)
- [ ] Patient zero activity (first confirmed malicious activity)
- [ ] Key attacker milestones (credential theft, lateral movement, data access)
- [ ] Containment actions (when did we start stopping the attack?)
- [ ] Recovery milestones (systems restored, all-clear declared)

### Step 2: Fill in Context
Work outward from anchor events:
- [ ] What happened immediately before the detection? (find earlier indicators)
- [ ] What happened between major milestones? (discover the kill chain)
- [ ] What was happening on affected systems during key windows?
- [ ] What legitimate activity provides context for attacker actions?

### Step 3: Multi-Source Correlation
For each attacker action, correlate across sources:
```
Example: Lateral Movement Correlation

14:32:17 [EDR]  WS-FIN-042: PowerShell encoded command executed
14:32:18 [SIEM] WS-FIN-042: Sysmon Event 1 - powershell.exe, parent: outlook.exe
14:32:20 [SIEM] WS-FIN-042: Sysmon Event 3 - Network connection to 10.1.2.50:445
14:32:21 [FW]   WS-FIN-042 -> SRV-FILE-01 (10.1.2.50): TCP/445 ALLOW
14:32:22 [SIEM] SRV-FILE-01: Windows Security 4624 - Logon Type 3 from WS-FIN-042
14:32:23 [SIEM] SRV-FILE-01: Sysmon Event 1 - psexec service installed
14:32:25 [EDR]  SRV-FILE-01: New service "PSEXESVC" created
```

### Step 4: Gap Analysis
Identify periods without data:
- [ ] Are there time gaps in logs? (log rotation, deletion, collection failure)
- [ ] Are there systems without monitoring? (blind spots)
- [ ] Are there actions we suspect but cannot prove? (mark as "assessed" not "confirmed")
- [ ] Document gaps explicitly: "No log data available for SRV-DB-01 between 14:00-16:00"

### Step 5: Validate and Refine
- [ ] Cross-reference attacker timeline with defender timeline
- [ ] Verify causality (does event A actually cause event B, or just precede it?)
- [ ] Check for alternative explanations for observed activity
- [ ] Have a second analyst review the timeline for logic and completeness
- [ ] Mark confidence level for each entry (confirmed, probable, possible)

## Visualization

### Linear Timeline
For reports and presentations:
```
Time (UTC)     Event
-----------    ------------------------------------------------
14:32:17  [ATK] Initial payload execution (WS-FIN-042)
14:32:20  [ATK] Lateral movement to SRV-FILE-01
14:35:00  [ATK] Credential dump on SRV-FILE-01
14:38:00  [ATK] Connection to domain controller (DC-01)
14:40:00  [ATK] DCSync attack - domain admin hash obtained
14:45:00  [SYS] SIEM alert: DCSync detected
14:47:00  [DEF] SOC analyst begins investigation
14:55:00  [ATK] Data staging on SRV-FILE-01
15:10:00  [DEF] Incident escalated to Tier 2
15:15:00  [ATK] Data exfiltration begins to external IP
15:30:00  [DEF] Containment: WS-FIN-042 network isolated
15:35:00  [DEF] Containment: SRV-FILE-01 network isolated
15:40:00  [DEF] External IP blocked at firewall
```

### Swimlane Diagram
For complex incidents with multiple systems:
```
System        14:30    14:45    15:00    15:15    15:30    15:45
============================================================
WS-FIN-042   [EXEC]---[MOVE]------------------------[ISOLATED]
SRV-FILE-01  --------[COMP]--[DUMP]---[STAGE]---[EXFIL]--[ISOLATED]
DC-01        ------------------[DCSYNC]---------------------
SOC          -------------------------[ALERT]-[ESCALATE]---[CONTAIN]
Firewall     -----------------------------------------[BLOCK]--
```

### Tools for Timeline Visualization
- Plaso/log2timeline (automated super-timeline generation)
- Timeline Explorer (digital forensics timeline viewer)
- Timesketch (collaborative timeline analysis, open source)
- Elastic Timeline (SIEM-integrated timeline)
- draw.io / Lucidchart (manual swimlane diagrams)
- Excel/Google Sheets (quick manual timelines)

## Timeline Quality Checklist

- [ ] All timestamps normalized to single timezone (UTC)
- [ ] Each entry has source attribution (which log, which system)
- [ ] Evidence reference for each entry (event ID, alert number, hash)
- [ ] Confidence level assigned to uncertain entries
- [ ] Gaps in coverage explicitly documented
- [ ] Attacker and defender actions clearly distinguished
- [ ] Kill chain phases identified and mapped
- [ ] Timeline reviewed by second analyst
- [ ] Timeline supports or contradicts working hypotheses (documented)

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Disk evidence for timeline
- `tasks/forensics/memory-forensics.md` — Memory evidence for timeline
- `tasks/forensics/network-forensics.md` — Network evidence for timeline
- `scripts/forensic-triage-scripts.md` — Automated artifact collection
- `scripts/log-analysis-queries.md` — SIEM queries for event extraction
- `workflows/incident-response-workflow.md` — IR process and documentation
