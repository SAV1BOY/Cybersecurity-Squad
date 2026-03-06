# Insider Threat Response Runbook

## Purpose

Response procedures for insider threat incidents covering behavioral indicators, legal coordination, evidence collection, and HR partnership. Balances investigation rigor with employee privacy and legal obligations.

## Insider Threat Categories

| Category | Description | Examples | Severity |
|----------|-------------|----------|----------|
| Malicious insider | Intentional harmful actions | Data theft, sabotage, espionage | Critical |
| Negligent insider | Careless or uninformed behavior | Mishandling data, policy violations | Medium |
| Compromised insider | Account or device taken over externally | Credential theft, malware | High |
| Departing employee | Leaving with organizational data | Copying files before resignation | High |
| Colluding insider | Working with external threat actor | Providing access, intelligence | Critical |

## Phase 1: Detection and Indicators

### Behavioral Indicators

| Category | Indicators | Detection Method |
|----------|-----------|-----------------|
| Digital | Unusual data downloads, after-hours access, USB usage | DLP, UEBA, audit logs |
| Digital | Access to files outside role, bulk printing | File access monitoring |
| Digital | Use of unauthorized cloud storage, personal email | CASB, email monitoring |
| Digital | Privilege escalation attempts, security bypass | SIEM, PAM logs |
| Behavioral | Disgruntlement, conflicts with management | HR reports, peer reports |
| Behavioral | Financial stress, lifestyle changes | Background checks (if authorized) |
| Behavioral | Working unusual hours without business need | Badge access, VPN logs |
| Behavioral | Reluctance to take vacation (preventing review of work) | HR tracking |
| Contextual | Resignation notice submitted | HR notification |
| Contextual | Denied promotion or raise | HR notification |
| Contextual | Under investigation for other matters | Legal/HR coordination |
| Contextual | Access to high-value intellectual property | Asset classification |

### UEBA Alert Correlation

| Alert Type | Score Weight | Example |
|-----------|-------------|---------|
| First-time access to sensitive share | Medium | User accesses finance share for first time |
| Volume anomaly | High | 10x normal download volume |
| Time anomaly | Medium | Access at 3 AM when never before |
| Sequence anomaly | High | Browse -> download -> USB copy -> cloud upload |
| Peer group deviation | Medium | Only person in role accessing specific data |
| Resignation + data access spike | Critical | Correlation of HR event + digital indicators |

## Phase 2: Legal and HR Coordination (CRITICAL)

### Before Starting Investigation

```
MANDATORY: Obtain legal and HR approval before any monitoring or investigation

1. Contact Legal Counsel
   - Confirm legal authority to investigate
   - Verify compliance with employment law
   - Review privacy obligations (GDPR, state laws)
   - Determine if law enforcement notification needed
   - Establish attorney-client privilege protections

2. Contact HR Business Partner
   - Confirm employment status and history
   - Review any prior incidents or warnings
   - Coordinate investigation approach
   - Align on potential outcomes
   - Plan communication strategy

3. Establish Investigation Team
   - Investigation lead (Security)
   - Legal counsel
   - HR representative
   - IT support (if technical collection needed)
   - Management stakeholder (need-to-know)

4. Document Authorization
   - Written authorization from legal to investigate
   - Scope of authorized monitoring/collection
   - Duration of authorized investigation
   - Escalation criteria
```

### Privacy and Legal Boundaries

| Action | US (Generally) | EU (GDPR) | Requirement |
|--------|---------------|-----------|-------------|
| Email monitoring | Permitted (company device/policy) | Restricted (proportionality) | Acceptable use policy + legal review |
| File access monitoring | Permitted (with policy) | Permitted (legitimate interest) | Privacy notice, DPA |
| Network monitoring | Permitted (with banner) | Permitted (legitimate interest) | Login banner, policy |
| Personal device search | Generally requires consent | Requires consent or legal basis | Legal review required |
| Physical surveillance | Varies by state | Highly restricted | Legal approval required |
| Keystroke logging | Varies, generally permitted with notice | Rarely permitted | Legal review required |
| Covert monitoring | Permitted in most US jurisdictions | Permitted only if overt monitoring would defeat purpose | Legal approval mandatory |

## Phase 3: Investigation

### Evidence Collection (Covert)

| Source | Data Collected | Collection Method | Legal Check |
|--------|---------------|-------------------|-------------|
| DLP logs | File transfers, email attachments, printing | DLP console export | Policy-authorized |
| Email audit | Sent items, forwarding rules, external recipients | Exchange audit log | Policy-authorized |
| File access logs | SharePoint/network share access patterns | Audit log export | Policy-authorized |
| Endpoint telemetry | USB usage, application usage, screenshots | EDR/UEBA console | Policy-authorized |
| Badge access | Physical access patterns, after-hours entry | Physical security system | Standard |
| Network logs | Web browsing, cloud storage access, data volumes | Proxy/firewall logs | Policy-authorized |
| Cloud access | CASB logs, SaaS application activity | CASB console | Policy-authorized |
| Print logs | Documents printed, volume, timing | Print server logs | Policy-authorized |

### Investigation Timeline Construction

```
Build a chronological timeline of:
1. Employment events (hire, promotion, denial, resignation notice)
2. Digital activity anomalies (with timestamps)
3. Physical access patterns
4. Communication patterns
5. Data access and movement
6. Any reported behavioral changes

Present as:
| Date/Time | Source | Event | Significance |
|-----------|--------|-------|-------------|
| 2026-02-15 | HR | Submitted resignation | Trigger event |
| 2026-02-16 | DLP | 500 files downloaded from engineering share | Volume anomaly |
| 2026-02-16 | USB | USB device connected (first time) | New behavior |
| 2026-02-17 | Email | Sent 15 attachments to personal email | Data exfiltration |
| 2026-02-18 | Badge | Accessed server room at 11 PM | After-hours physical access |
```

### Analysis Framework

| Question | Investigation Method |
|----------|---------------------|
| What data was accessed? | File access logs, DLP, endpoint telemetry |
| Was data exfiltrated? | Email audit, USB logs, cloud upload logs, print logs |
| Where was data sent? | Email recipients, cloud storage destinations |
| How much data was taken? | Volume analysis, file count |
| What is the data classification? | Data classification tags, content inspection |
| Was access authorized? | RBAC review, role comparison |
| Is there a pattern? | UEBA correlation, timeline analysis |
| Is there external involvement? | Email analysis, network connections |

## Phase 4: Containment

### Containment Options (Escalating)

| Level | Action | When to Use |
|-------|--------|------------|
| 1. Enhanced monitoring | Increase logging and alerting | Suspicion, insufficient evidence |
| 2. Access restriction | Remove access to sensitive data/systems | Moderate evidence, low flight risk |
| 3. Account suspension | Disable account, maintain employment | Strong evidence, legal/HR aligned |
| 4. Termination | End employment, full access revocation | Confirmed, legal/HR approved |
| 5. Law enforcement | Report to authorities | Criminal activity, significant loss |

### Departing Employee Protocol

```
When employee gives notice:

Immediate (Day 0):
[ ] Notify security team of departure
[ ] Enable enhanced monitoring on employee accounts
[ ] Review current access permissions
[ ] Baseline current data access patterns

During Notice Period:
[ ] Monitor for data hoarding (bulk downloads, unusual access)
[ ] Monitor for USB device usage
[ ] Monitor for personal email/cloud storage transfers
[ ] Review email forwarding rules
[ ] Restrict access to non-essential sensitive systems

Last Day:
[ ] Conduct exit interview (include security acknowledgment)
[ ] Disable all accounts within 1 hour of departure
[ ] Collect all company devices
[ ] Revoke physical access (badge, keys)
[ ] Remind of NDA/non-compete obligations (legal)
[ ] Review 30-day activity log for any concerns

Post-Departure:
[ ] Monitor for account usage attempts (disabled accounts)
[ ] Check for shared credentials still active
[ ] Verify backup copies of employee's work are retained
[ ] Monitor for intellectual property appearing externally
```

## Phase 5: Documentation and Reporting

### Investigation Report Structure

```
1. Case Summary
   - Subject identification (name, role, department)
   - Investigation trigger and dates
   - Authorization (legal approval reference)

2. Findings
   - Evidence-supported facts (what, when, how)
   - Data classification of affected information
   - Volume and scope of data involved
   - Timeline of events

3. Impact Assessment
   - Business impact (IP loss, competitive advantage)
   - Regulatory impact (data breach obligations)
   - Financial impact (estimated loss)
   - Reputational impact

4. Recommendations
   - Disciplinary action (HR/legal decision)
   - Law enforcement referral (if applicable)
   - Preventive controls to implement
   - Policy or process improvements

5. Evidence Index
   - All evidence items with chain of custody
   - Preservation details
```

### Metrics and Reporting

| Metric | Target | Purpose |
|--------|--------|---------|
| Mean time to detect insider threat | < 30 days | Program effectiveness |
| Investigation completion time | < 30 days | Process efficiency |
| Data volume prevented from exfiltration | Track | DLP effectiveness |
| Departing employee monitoring coverage | 100% | Protocol compliance |
| False positive rate (UEBA) | < 20% | Tool tuning |

## Cross-References

- [Incident Response Workflow](../../workflows/incident-response-workflow.md) -- overall IR process
- [Digital Forensics Methodology](../../frameworks/digital-forensics-methodology.md) -- evidence handling
- [DLP Implementation Checklist](../../checklists/data-protection/dlp-implementation-checklist.md) -- DLP setup
- [Data Classification Framework](../../frameworks/data-classification-framework.md) -- data sensitivity
