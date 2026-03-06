# Ticketing System Communication Guide

## Purpose

This guide standardizes how the squad creates, updates, and manages security tickets in Jira, ServiceNow, or equivalent ticketing systems. Tickets are the system of record for security work — they drive prioritization, track remediation, measure SLA compliance, and provide evidence for audits. A well-written ticket gets resolved. A poorly written ticket gets deprioritized, bounced between teams, or closed without resolution.

## Ticket Title Conventions

### Format
`[Category] [Severity] — [Concise Description] — [Affected Asset]`

### Examples
- `[VULN] CRITICAL — CVE-2024-XXXX RCE in Apache Struts — app-web-01`
- `[INCIDENT] SEV-1 — Ransomware Detection — Finance Workstations`
- `[FINDING] HIGH — Missing MFA on Privileged Accounts — Active Directory`
- `[RISK] MEDIUM — Unencrypted PII in S3 Bucket — data-lake-prod`
- `[COMPLIANCE] HIGH — PCI-DSS 8.3.1 Gap — CDE Network Segment`

### Category Prefixes

| Prefix | Use Case |
|--------|----------|
| `[VULN]` | Vulnerability remediation |
| `[INCIDENT]` | Incident response tasks |
| `[FINDING]` | Assessment/audit findings |
| `[RISK]` | Risk register items |
| `[COMPLIANCE]` | Compliance gaps |
| `[HARDENING]` | System hardening tasks |
| `[ACCESS]` | Access review or provisioning |
| `[DETECTION]` | Detection rule development or tuning |

## Ticket Body Template

```
## Summary
[One paragraph: what the issue is, why it matters, and what needs to happen]

## Severity / Priority
- Security Severity: [Critical / High / Medium / Low]
- Business Priority: [P1 / P2 / P3 / P4]
- SLA Deadline: [Date based on severity-to-SLA mapping]
- Justification: [Why this severity rating — link to calibration guide]

## Affected Assets
| Asset | Type | Environment | Owner |
|-------|------|-------------|-------|
| [hostname/IP] | [Server/App/DB/Network] | [Prod/Stage/Dev] | [Team/Person] |

## Technical Details
[Specific technical information needed for remediation:
- CVE/CWE reference
- Vulnerability description
- Evidence (screenshots, scan output, log excerpts)
- Current configuration vs. required configuration
- Link to assessment report if applicable]

## Remediation Steps
1. [Specific action with enough detail for the assignee to execute]
2. [Specific action]
3. [Verification step to confirm fix]

## Acceptance Criteria
- [ ] [Measurable condition #1 that must be true for closure]
- [ ] [Measurable condition #2]
- [ ] [Verification scan/test completed showing remediation]
- [ ] [Evidence attached to ticket]

## References
- Assessment Report: [Link]
- Vendor Advisory: [Link]
- Internal KB Article: [Link]
- Related Tickets: [Link to parent/child/related tickets]
```

## Priority Mapping

Security severity does not always equal business priority. Map them explicitly:

| Security Severity | Default Business Priority | Override Conditions |
|------------------|--------------------------|-------------------|
| Critical | P1 — Immediate | May lower to P2 if strong compensating controls exist |
| High | P2 — Next Sprint | Elevate to P1 if compliance deadline is imminent |
| Medium | P3 — This Quarter | Elevate to P2 if asset is business-critical |
| Low | P4 — Backlog | Elevate to P3 if clustered findings indicate systemic issue |

**Document any priority override** in the ticket with rationale: "Security severity HIGH elevated to P1 due to PCI-DSS audit in 30 days. Finding must be remediated before audit window."

## Ticket Lifecycle Management

### Status Workflow
```
Open --> In Triage --> Assigned --> In Progress --> In Verification --> Closed
                                        |                                ^
                                        v                                |
                                   Blocked -----(unblocked)------------>-+
                                        |
                                        v
                                   Risk Accepted (requires approval)
```

### Status Update Cadence

| Priority | Update Frequency | Escalation If No Update |
|----------|-----------------|------------------------|
| P1 | Daily | After 24 hours with no update |
| P2 | Weekly | After 7 days with no update |
| P3 | Bi-weekly | After 14 days with no update |
| P4 | Monthly | After 30 days with no update |

### Comment Standards

Every status update comment should follow this format:
```
**Update [Date]**
- Status: [Current status]
- Progress: [What was done since last update]
- Blockers: [Any blockers, or "None"]
- Next Steps: [What will be done next]
- ETA: [Updated estimate if changed]
```

## Acceptance Criteria Standards

Acceptance criteria must be objective and verifiable. The question is: "Could a third party independently confirm this is fixed?"

### Good Acceptance Criteria
- "Vulnerability scan (Qualys/Nessus) of affected hosts shows CVE-2024-XXXX as resolved"
- "MFA enforcement verified for 100% of privileged accounts via Azure AD conditional access policy export"
- "TLS 1.0 and 1.1 disabled on all web servers — confirmed by SSL Labs scan showing A or A+ rating"

### Bad Acceptance Criteria
- "Vulnerability is fixed" (how do you verify?)
- "Security is improved" (not measurable)
- "Patch applied" (does not confirm the vulnerability is actually resolved — the patch might have failed)

## Linking and Hierarchy

- **Epic**: Assessment engagement or risk initiative (e.g., "Q1 2024 Pentest Remediation")
- **Story/Task**: Individual finding or remediation item
- **Sub-task**: Individual steps within a complex remediation
- **Related**: Findings that share root cause or remediation path
- **Blocks/Blocked by**: Dependencies between remediation tasks

Always link tickets to their source — the assessment report, vulnerability scan, audit finding, or incident report that generated them.

## Metrics Derived from Tickets

| Metric | Calculation | Target |
|--------|------------|--------|
| Mean Time to Remediate (MTTR) | Average time from ticket creation to closure by severity | Critical: <72h, High: <30d |
| SLA Compliance Rate | % of tickets closed within SLA deadline | >90% |
| Aging Findings | Count of open tickets past SLA deadline | Trending to zero |
| Reopen Rate | % of tickets reopened after closure | <5% |
| Risk Acceptance Rate | % of findings closed via risk acceptance vs. remediation | Monitor for trends |

## Cross-References

- See `voice/calibration/severity-calibration.md` for severity rating standards
- See `voice/calibration/urgency-calibration.md` for SLA alignment
- See `voice/channel-adaptation/slack-security-channels.md` for creating tickets from Slack discussions
- See `voice/tone-profiles/compliance-auditor.md` for audit finding ticket language
