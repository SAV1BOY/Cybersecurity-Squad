# Blameless Postmortem Examples — Learning from Incidents

## Purpose
Exemplary postmortem formats and practices that drive organizational learning without creating fear.

## The Blameless Postmortem Framework

### Core Principles
1. **Human error is a symptom**, not a cause — look for systemic failures
2. **The person closest to the failure has the most information** — protect and listen to them
3. **Accountability without blame** — own outcomes, improve systems
4. **Publicize widely** — shared learning prevents repeated failures
5. **Action items with owners and deadlines** — or the postmortem was theater

## Exemplary Format

### Header
```markdown
# Incident Postmortem: [INCIDENT-ID] — [Short Description]
- **Severity**: SEV-1/2/3
- **Date**: YYYY-MM-DD
- **Duration**: X hours Y minutes
- **Impact**: [Users affected, data exposed, systems impacted]
- **Author**: [IR Lead]
- **Reviewers**: [Engineering Lead, CISO, affected team leads]
- **Status**: Draft / Reviewed / Published / Action Items Complete
```

### Timeline (Factual, No Blame)
```
14:23 UTC — Monitoring alert fires: unusual outbound traffic from prod-db-03
14:25 UTC — SOC analyst acknowledges alert, begins triage
14:31 UTC — Analyst identifies data exfiltration pattern, escalates to IR
14:35 UTC — IR lead declares SEV-1, assembles response team
14:42 UTC — Network team isolates affected segment
14:55 UTC — Forensics begins memory capture on affected hosts
15:30 UTC — Root cause identified: compromised service account via phished developer
16:00 UTC — All compromised credentials rotated
17:00 UTC — Full containment confirmed
18:30 UTC — Recovery operations begin
```

### What Went Well
- Alert fired within 3 minutes of exfiltration start
- SOC escalation to IR was fast and followed playbook
- Network isolation was executed without impacting other services
- Executive communication was clear and timely

### What Went Poorly
- Service account had excessive privileges (admin on 12 databases)
- No MFA on service account authentication
- Phishing simulation for engineering team was 3 months overdue
- Runbook for this scenario was outdated (referenced deprecated tooling)

### Root Cause Analysis (5 Whys)
1. **Why** was data exfiltrated? → Attacker had database admin access
2. **Why** did attacker have admin access? → Compromised service account had admin privileges
3. **Why** did the service account have admin? → Provisioned 2 years ago, never reviewed
4. **Why** was it never reviewed? → No automated privilege review process
5. **Why** is there no review process? → Deprioritized in favor of feature delivery

**Systemic root cause**: Lack of automated service account lifecycle management and periodic privilege review.

### Action Items
| # | Action | Owner | Deadline | Status |
|---|--------|-------|----------|--------|
| 1 | Implement service account privilege review (quarterly) | IAM Team | 30 days | Open |
| 2 | Enforce MFA on all service accounts | IAM Team | 14 days | Open |
| 3 | Update IR runbook for data exfiltration | IR Lead | 7 days | Open |
| 4 | Resume phishing simulation program | Security Awareness | 7 days | Open |
| 5 | Deploy least-privilege analyzer for database accounts | DBA Team | 60 days | Open |

## Anti-Patterns in Postmortems
- Naming individuals as the "cause" of the incident
- Skipping the "What went well" section
- Action items without deadlines or owners
- Restricting access to the postmortem document
- Never following up on action items
- Rewriting history to make the response look better

## Cross-References
- `templates/reports/incident-postmortem-report.md` — Full template
- `checklists/incident-response/post-incident-checklist.md` — Post-incident process
- `agents/chris-sanders.md` — IR and evidence-based analysis
