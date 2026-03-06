# Urgency Calibration Guide

## Purpose

This guide standardizes how the squad communicates urgency — when to escalate, what response timelines to set, and how to align urgency language with organizational SLAs. Miscalibrated urgency either desensitizes stakeholders (everything is urgent, so nothing is) or delays critical response (understating urgency on genuinely time-sensitive issues). Calibrated urgency saves organizations.

## Urgency Tiers

### Tier 1: Immediate (Drop Everything)

**Response Window**: Within 1-4 hours of detection
**Remediation Target**: 24-72 hours

**Triggers**:
- Active adversary confirmed in the environment
- Ransomware execution detected or in progress
- Confirmed data exfiltration of sensitive data
- Exploitation of a zero-day vulnerability on internet-facing systems
- Safety-critical system compromise (industrial control, medical devices)
- Credential compromise of highly privileged accounts (domain admin, cloud root)

**Communication Pattern**:
- Phone call to incident commander, do not rely on asynchronous channels
- Incident bridge/war room opened within 30 minutes
- Stakeholder notification within 1 hour
- Status updates every 30 minutes until contained

**Language**:
- "IMMEDIATE ACTION REQUIRED — Active [threat type] detected. Incident bridge open at [location]. All responders join now."
- Do not soften the language. If it is Tier 1, say so unambiguously.

### Tier 2: Urgent (Next Business Hours)

**Response Window**: Within 8 business hours
**Remediation Target**: 7-30 days

**Triggers**:
- Critical vulnerability with public exploit on exposed systems (no active exploitation yet)
- CISA KEV addition for a vulnerability present in the environment
- Threat intelligence indicating imminent targeting of the organization or sector
- Failed security control on a critical system (EDR offline, firewall rule bypass)
- Compliance violation with regulatory reporting deadline approaching

**Communication Pattern**:
- Slack/Teams message in security channel with @mention of responsible parties
- Email to system owners with "URGENT" classification
- Tracking ticket created with SLA clock started
- Status check within 24 hours

**Language**:
- "URGENT: [Vulnerability/Threat] requires remediation within [timeframe]. Affected systems: [list]. Remediation owner: [name]. SLA deadline: [date/time]."

### Tier 3: Elevated (This Sprint/Cycle)

**Response Window**: Within 5 business days for triage
**Remediation Target**: 30-90 days

**Triggers**:
- High-severity vulnerability without active exploitation or public exploit
- Security architecture gap identified during review
- Audit finding with upcoming compliance deadline
- Threat intelligence indicating general (not targeted) risk increase
- Control degradation that increases risk but does not create immediate exposure

**Communication Pattern**:
- Ticket created and prioritized in the current or next sprint
- Email notification to system owner with action items
- Monthly reporting inclusion
- Tracked in vulnerability management dashboard

**Language**:
- "[Finding/Risk] identified. Remediation recommended within [timeframe]. Ticket [ID] assigned to [owner]. Include in [sprint/cycle] planning."

### Tier 4: Scheduled (Next Quarter)

**Response Window**: Triage within 30 days
**Remediation Target**: 90-180 days

**Triggers**:
- Medium or low severity findings from routine assessments
- Best practice deviations without direct exploitability
- Technical debt items with security implications
- Policy updates requiring procedural changes
- Training and awareness gaps

**Communication Pattern**:
- Documented in assessment report
- Ticket created and added to backlog
- Included in quarterly security review
- Tracked for trending

**Language**:
- "[Finding] documented in [report]. Recommend remediation by [date]. Backlog ticket [ID] created."

### Tier 5: Awareness (Track and Monitor)

**Response Window**: No active response required
**Remediation Target**: Next system refresh or as opportunity permits

**Triggers**:
- Informational findings
- Emerging threats with no current applicability
- Industry trends requiring monitoring but no action
- Long-term strategic recommendations

**Communication Pattern**:
- Included in periodic threat briefings
- Added to risk register for monitoring
- No individual notifications

## Escalation Decision Tree

```
Is there an active threat actor in the environment?
  YES --> Tier 1 (Immediate)
  NO  --> Continue

Is there a confirmed exploitable vulnerability with:
  - Public exploit AND internet exposure AND sensitive data?
    YES --> Tier 1 (Immediate)
    NO  --> Continue

  - Public exploit OR CISA KEV listing?
    YES --> Tier 2 (Urgent)
    NO  --> Continue

Is the finding severity Critical or High?
  CRITICAL --> Tier 2 (Urgent) minimum
  HIGH     --> Tier 3 (Elevated) minimum, Tier 2 if compensating controls are absent
  MEDIUM   --> Tier 4 (Scheduled)
  LOW      --> Tier 4 or Tier 5
  INFO     --> Tier 5 (Awareness)

Are there regulatory or compliance deadlines?
  YES, within 30 days   --> Elevate by one tier
  YES, within 90 days   --> Maintain current tier, flag deadline
  NO                     --> Maintain current tier
```

## SLA Alignment

Map urgency tiers to the organization's existing SLA structure:

| Urgency Tier | Vulnerability Management SLA | Incident Response SLA | Change Management |
|-------------|-----------------------------|-----------------------|-------------------|
| Tier 1 | Emergency patch (24-72h) | SEV-1 incident declared | Emergency change |
| Tier 2 | Critical patch window (7-30d) | SEV-2 investigation | Expedited change |
| Tier 3 | Standard patch cycle (30-90d) | Monitoring/hunting | Standard change |
| Tier 4 | Extended remediation (90-180d) | Risk register entry | Planned change |
| Tier 5 | Backlog / next refresh | Awareness only | No change required |

## Urgency Inflation and Deflation

### Signs of Inflation
- More than 20% of findings rated Tier 1 or Tier 2 — indicates miscalibration
- Stakeholders ignoring urgent notifications — "urgent fatigue"
- Every vulnerability scan result treated as an emergency

### Signs of Deflation
- Critical vulnerabilities languishing in Tier 3 or Tier 4 queues
- Post-incident reviews revealing that the exploited vulnerability was known but deprioritized
- Compliance deadlines missed because findings were not escalated in time

### Correction
- Monthly review of urgency distribution across all findings
- Post-incident comparison: was the urgency tier assigned to the exploited finding appropriate?
- Calibration discussions when analysts disagree on tier assignment

## Cross-References

- See `voice/calibration/severity-calibration.md` for severity rating that feeds urgency decisions
- See `voice/tone-profiles/incident-commander.md` for Tier 1 communication cadence
- See `voice/language-guides/incident-communication-language.md` for stakeholder notification language
- See `voice/channel-adaptation/slack-security-channels.md` for channel-appropriate urgency formatting
