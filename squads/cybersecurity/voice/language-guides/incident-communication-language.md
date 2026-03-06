# Incident Communication Language Guide

## Purpose

This guide standardizes language used during and after security incidents across all communication channels and audiences. Incident communication is high-stakes — the wrong word in a status update can trigger unnecessary panic, legal exposure, or loss of stakeholder confidence. The right language keeps the response focused, stakeholders informed, and the organization protected.

## Communication Phases

### Phase 1: Detection and Triage (Internal Only)

**Audience**: Security team, IT operations
**Objective**: Establish facts, avoid premature conclusions

**Language Pattern**:
- "We are investigating [anomalous activity / a potential security event] affecting [system/service]."
- "Initial indicators suggest [observation]. We are working to determine scope and impact."
- "This has been classified as a [SEV level] incident. The incident commander is [name]."

**Critical Rules**:
- Use "investigating" and "potential" until facts are confirmed
- Do not use "breach" until data exfiltration is confirmed by evidence
- Do not attribute to a threat actor until attribution meets confidence thresholds
- Include the time of detection (UTC) in every initial notification

### Phase 2: Containment (Internal Stakeholders)

**Audience**: IT leadership, business unit owners, legal
**Objective**: Communicate impact and containment actions without speculation

**Status Update Template**:
```
INCIDENT STATUS UPDATE — [TIMESTAMP UTC]
Incident ID: [ID]
Severity: [SEV-1/2/3]
Phase: Containment

CURRENT STATUS
[2-3 sentences: what is known, what is being done]

BUSINESS IMPACT
- [Service/system] is [operational / degraded / offline]
- Estimated users/customers affected: [number or "under assessment"]
- Data exposure: [confirmed / not confirmed / under investigation]

ACTIONS IN PROGRESS
1. [Action] — Owner: [name] — ETA: [time]
2. [Action] — Owner: [name] — ETA: [time]

NEXT UPDATE: [Timestamp]
```

**Language Rules**:
- State facts, not theories
- "We have contained the affected systems" (if true) vs. "We are working to contain" (if in progress)
- Never promise a resolution time you cannot meet
- Acknowledge what you do not yet know: "The full scope of affected data is still being determined"

### Phase 3: Stakeholder and Customer Notification

**Audience**: Customers, partners, regulators, media
**Objective**: Transparent, legally reviewed communication that maintains trust

**Customer Notification Template**:
```
Subject: Security Incident Notification — [Company Name]

[Date]

We are writing to inform you of a security incident that [may affect /
affected] [your account / your data / our services].

WHAT HAPPENED
[Plain language description of the incident — factual, no speculation.
Include timeline: when it occurred, when it was detected, when it was
contained.]

WHAT INFORMATION WAS INVOLVED
[Specific data types affected. Be precise: "email addresses and hashed
passwords" not "some personal information."]

WHAT WE ARE DOING
[Actions taken to contain, investigate, and prevent recurrence.]

WHAT YOU CAN DO
[Specific, actionable steps for the recipient: password reset links,
credit monitoring enrollment, contact information.]

FOR MORE INFORMATION
[Dedicated contact channel: email, phone, FAQ page.]
```

**Language Rules**:
- Have legal review all external communications before release
- Use "security incident" not "breach" unless legally required or factually confirmed
- Be specific about what data was affected — vagueness erodes trust faster than bad news
- Do not speculate on threat actor identity or motivation in public communications
- Include what you are doing to prevent recurrence — this demonstrates accountability

### Phase 4: Post-Mortem Communication

**Audience**: Internal teams, leadership, and (optionally) public
**Objective**: Learning and accountability without blame

**Post-Mortem Language Principles**:
- Use "contributing factors" not "root cause" — incidents rarely have a single cause
- Describe system failures, not people failures: "The deployment process did not include a security review step" not "The developer did not check for vulnerabilities"
- Focus on what happened and why, not who did what wrong
- Every contributing factor must have a corresponding remediation action with an owner and deadline

**Post-Mortem Structure**:
```
INCIDENT POST-MORTEM — [Incident ID]
Date: [Date]
Author: [Name]
Severity: [SEV level]
Duration: [Detection to resolution]

SUMMARY
[3-5 sentences covering what happened, impact, and resolution]

TIMELINE
[Detailed chronological sequence of events with UTC timestamps]

CONTRIBUTING FACTORS
1. [Factor] — [Why this contributed to the incident]
2. [Factor] — [Why this contributed to the incident]

WHAT WENT WELL
- [Positive aspects of the response]

WHAT COULD BE IMPROVED
- [Gaps identified during response]

ACTION ITEMS
| # | Action | Owner | Priority | Due Date | Status |
|---|--------|-------|----------|----------|--------|
| 1 | [Item] | [Name] | [P1/P2/P3] | [Date] | Open |
```

## Prohibited Language During Incidents

| Do Not Say | Say Instead | Reason |
|-----------|-------------|--------|
| "We were hacked" | "We experienced a security incident" | Legal implications, premature characterization |
| "Your data was stolen" | "Unauthorized access to [data type] was detected" | "Stolen" implies irreversibility and intent before confirmed |
| "This was a sophisticated attack" | "The attack leveraged [specific technique]" | "Sophisticated" is subjective and often inaccurate |
| "We guarantee this will not happen again" | "We are implementing [controls] to reduce the likelihood of recurrence" | No guarantee is credible; describe specific mitigations |
| "A disgruntled employee" | "An internal actor" or "unauthorized insider access" | Characterization before investigation is complete is premature |

## Regulatory Notification Timing

| Regulation | Notification Deadline | Recipient |
|-----------|----------------------|-----------|
| GDPR | 72 hours from awareness | Supervisory authority + affected individuals |
| HIPAA | 60 days from discovery | HHS + affected individuals |
| PCI-DSS | Immediately | Acquiring bank and payment brands |
| SEC (public companies) | 4 business days (material incidents) | SEC filing |
| State breach laws | Varies (30-90 days) | State AG + affected residents |

## Cross-References

- See `voice/tone-profiles/incident-commander.md` for IC communication cadence and tone
- See `voice/calibration/urgency-calibration.md` for severity-to-timeline mapping
- See `voice/channel-adaptation/slack-security-channels.md` for real-time channel communication
- See `voice/channel-adaptation/email-security-advisories.md` for advisory formatting
