# Email Security Advisory Communication Guide

## Purpose

This guide standardizes how the squad writes and distributes security advisories via email. Email remains the authoritative channel for formal security notifications — vulnerability advisories, policy changes, incident notifications, and compliance updates. Unlike Slack, email creates a persistent, searchable record and reaches stakeholders who may not monitor real-time channels.

## Advisory Types and Templates

### Type 1: Vulnerability Advisory

**When to send**: New critical/high vulnerability affecting the organization's technology stack, CISA KEV additions relevant to the environment, or vendor security patches requiring coordinated deployment.

**Distribution**: IT operations, system owners, development teams, security team

```
Subject: [SECURITY ADVISORY] [SEV: CRITICAL/HIGH/MEDIUM] — [CVE-YYYY-NNNNN] [Vulnerability Name] in [Product]

CLASSIFICATION: [Internal / Confidential]
ADVISORY ID: SA-[YYYY]-[NNN]
DATE: [YYYY-MM-DD]
SEVERITY: [Critical / High / Medium]
CVE: [CVE-YYYY-NNNNN]
CVSS: [Score] ([Vector])

AFFECTED PRODUCTS:
- [Product name] versions [X.Y] through [X.Z]
- [Additional affected products]

SUMMARY:
[2-3 sentences: what the vulnerability is, how it can be exploited,
and what the impact is in plain technical language]

ORGANIZATIONAL EXPOSURE:
- [Number] systems identified running affected versions
- [System names/categories] in [environment: production/staging/dev]
- Internet-facing: [Yes/No]
- Compensating controls: [Present/Absent]

REQUIRED ACTION:
1. [Specific remediation step with deadline]
2. [Interim mitigation if patch cannot be applied immediately]
3. [Verification step to confirm remediation]

DEADLINE: [Date and time, based on severity SLA]

RESOURCES:
- Vendor advisory: [URL]
- Internal patch guide: [URL]
- Questions: Reply to this email or contact security@company.com

— Information Security Team
```

### Type 2: Incident Notification

**When to send**: Declared security incidents requiring stakeholder awareness, service impact notifications, or regulatory notification triggers.

**Distribution**: Varies by incident severity and type (see distribution matrix below)

```
Subject: [INCIDENT NOTIFICATION] [SEV-1/2/3] — [Brief Description]

CLASSIFICATION: CONFIDENTIAL
INCIDENT ID: INC-[YYYY]-[NNN]
DATE/TIME: [YYYY-MM-DD HH:MM UTC]
SEVERITY: [SEV-1 / SEV-2 / SEV-3]
STATUS: [Active / Contained / Resolved]

WHAT HAPPENED:
[Plain language description — factual, no speculation. 3-5 sentences.]

CURRENT IMPACT:
- Services affected: [list]
- Users/customers affected: [number or scope]
- Data exposure: [confirmed / under investigation / none detected]

WHAT WE ARE DOING:
- [Action in progress or completed]
- [Action in progress or completed]
- [Action planned]

WHAT YOU NEED TO DO:
- [Specific action for the recipient, if any]
- [Or: "No action required at this time. This is for awareness."]

NEXT UPDATE: [Date/time or "upon significant development"]

QUESTIONS:
- Technical: [contact]
- Business/Legal: [contact]
- Do not discuss this incident outside authorized channels.
```

### Type 3: Policy or Standards Update

**When to send**: New security policy published, existing policy updated, compliance requirement changes, or process changes affecting security operations.

```
Subject: [POLICY UPDATE] [Policy Name] — Effective [Date]

POLICY: [Full policy name and ID]
VERSION: [New version number] (previous: [old version])
EFFECTIVE DATE: [Date]
CHANGE TYPE: [New Policy / Major Revision / Minor Update]

SUMMARY OF CHANGES:
- [Change 1: brief description]
- [Change 2: brief description]
- [Change 3: brief description]

WHAT THIS MEANS FOR YOU:
[2-3 sentences explaining practical impact on the recipient's work]

REQUIRED ACTION:
- Review the updated policy by [date]
- Complete acknowledgment in [system] by [date]
- Implement required changes by [date]

FULL POLICY: [Link to policy document]
CHANGE LOG: [Link to detailed change log]

QUESTIONS: Contact [policy owner name] at [email] or [Slack channel].
```

## Subject Line Conventions

Subject lines must be scannable and filterable:

| Prefix | Meaning | Priority |
|--------|---------|----------|
| `[SECURITY ADVISORY]` | Vulnerability or threat notification | Filterable by IT teams |
| `[INCIDENT NOTIFICATION]` | Active or resolved security incident | Highest attention |
| `[POLICY UPDATE]` | Policy or standards change | Governance and compliance |
| `[ACTION REQUIRED]` | Recipient must take specific action | Add to any of the above when applicable |
| `[FYI]` | Informational, no action needed | Lower priority |

**Severity in subject**: Always include `[SEV: CRITICAL]`, `[SEV: HIGH]`, etc. for vulnerability advisories. This enables inbox rules and prioritization.

## Distribution Lists

Maintain curated distribution lists rather than ad hoc recipient selection:

| List | Members | Use Case |
|------|---------|----------|
| `security-advisories-all` | All IT and security staff | General vulnerability advisories |
| `security-advisories-critical` | System owners, IT leadership, CISO | Critical/High advisories only |
| `incident-notification-internal` | IT, security, legal, communications | Internal incident notifications |
| `incident-notification-executive` | C-suite, board (if applicable) | SEV-1 incidents only |
| `security-policy-updates` | All employees | Policy changes |
| `[system]-owners` | Specific system/application owners | Targeted vulnerability notifications |

## Email Formatting Standards

- **Plain text preferred** for security advisories — HTML emails can be flagged by security tools and may render inconsistently
- **Consistent structure**: Recipients should know exactly where to find the action items in every advisory
- **No attachments with IOCs**: Use secure sharing platforms for IOC lists, detection rules, or sensitive technical details. Reference via link.
- **Reply-to address**: Set to a monitored security mailbox, not an individual
- **Digital signatures**: Sign advisories with S/MIME or PGP where supported to prevent spoofing

## Tracking and Metrics

Track the following for continuous improvement:
- Advisory distribution time (vulnerability published to advisory sent)
- Open rates and click-through on remediation links
- Remediation compliance rates by deadline
- False advisory rate (advisories sent for non-applicable vulnerabilities)

## Cross-References

- See `voice/tone-profiles/executive-advisory.md` for executive notification tone
- See `voice/language-guides/incident-communication-language.md` for incident notification language
- See `voice/language-guides/vulnerability-severity-language.md` for severity description
- See `voice/calibration/urgency-calibration.md` for SLA-aligned deadlines
