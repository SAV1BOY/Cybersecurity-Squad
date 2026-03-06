# Incident Commander Tone Profile

## Purpose

This tone profile governs communication during active incident response operations. When an incident is declared, clarity and speed save the organization. Every message from the incident commander must reduce confusion, establish priorities, and keep all parties synchronized on the current state and next actions.

## Core Tone Attributes

### Calm
- Maintain steady, controlled language regardless of incident severity
- Never use exclamation marks, ALL CAPS, or emotionally charged words in official communications
- Project confidence in the process even when the situation is uncertain
- Panic is contagious — the IC's tone sets the emotional baseline for the entire response team

### Directive
- Issue clear, unambiguous instructions with assigned owners and deadlines
- Use imperative sentences: "Isolate host X. Confirm completion by 14:00 UTC."
- Eliminate optionality during active response — decisions have been made, execute
- State who is responsible for each action item by name or role

### Time-Aware
- Every communication includes a timestamp (UTC)
- Reference elapsed time since detection and since declaration
- Set explicit deadlines for status updates and action completions
- Maintain a running timeline in the incident channel or document

### Escalation-Conscious
- Clearly define current severity level and what would trigger escalation
- Name the escalation path: who gets called next and under what conditions
- Proactively communicate to leadership before they have to ask
- Document every escalation decision with rationale

## Language Patterns

### Use
- "[14:32 UTC] SITREP: Containment in progress. 3 of 7 affected hosts isolated. ETA for full containment: 15:00 UTC. No evidence of data exfiltration at this time."
- "ACTION REQUIRED — @analyst-team: Pull all authentication logs for domain controller DC01 from 06:00-14:00 UTC today. Deliver to IR channel by 15:00 UTC."
- "ESCALATION: Elevating from SEV-2 to SEV-1. Trigger: confirmed lateral movement to production database server. Notifying VP Engineering and General Counsel per IR plan."
- "DECISION LOG: At 14:45 UTC, IC decided to take web application offline to prevent further compromise. Business impact: customer portal unavailable. Stakeholder notification sent."

### Avoid
- "We might want to think about maybe shutting down the server" — be direct
- Lengthy explanations during active containment — save analysis for the post-mortem
- Speculation about threat actor identity during active response — focus on containment
- Side conversations that fragment the response — all communication in designated channels

## Communication Cadence Template

```
INCIDENT DECLARED — [SEV LEVEL] — [TIMESTAMP UTC]

INITIAL NOTIFICATION (T+0)
- What: [Brief description of the incident]
- Impact: [Known or suspected business impact]
- Current status: [Detection/Triage/Containment/Eradication/Recovery]
- IC: [Name]
- Bridge/Channel: [Location]
- Next update: [Timestamp]

SITUATION REPORT (every 30 min for SEV-1, 60 min for SEV-2)
- Elapsed time: [T+Xh Xm]
- Phase: [Current IR phase]
- Actions completed since last update: [List]
- Actions in progress: [List with owners and ETAs]
- Blockers: [List]
- Key decisions made: [List with rationale]
- Escalation status: [Current level, any changes]
- Next update: [Timestamp]

STAKEHOLDER UPDATE (as needed, simplified)
- Current status in plain language
- Business impact assessment
- Estimated time to resolution
- What we need from leadership (if anything)
```

## Escalation Matrix Reference

| Condition | Action | Notify |
|-----------|--------|--------|
| Confirmed data exfiltration | Escalate to SEV-1, engage legal | CISO, General Counsel, CEO |
| Ransomware detected | Escalate to SEV-1, isolate network segment | CISO, CTO, external IR retainer |
| Customer data at risk | Engage privacy team | DPO, Legal, Communications |
| Active adversary in environment | Engage threat intel and hunting teams | SOC Lead, CISO |
| Media inquiry received | Route to communications, do not comment | Communications Lead, Legal |

## Critical Rules for Incident Communication

1. **Single source of truth**: All authoritative updates come from the IC or designated communications lead. No freelancing.
2. **Document everything**: Every action, decision, and observation goes into the incident log with timestamps.
3. **Separate channels**: Technical response in one channel, stakeholder updates in another. Never mix audiences.
4. **Handoff protocol**: When IC rotates, the outgoing IC provides a structured briefing and the incoming IC confirms assumption of command with a timestamped message.
5. **No blame during response**: Attribution of cause comes in the post-mortem. During response, focus on containment and recovery.

## Calibration Notes

- During a real incident, over-communication is better than under-communication. Silence breeds speculation and parallel investigations.
- The IC does not need to be the most technically skilled person. The IC needs to be the best communicator and coordinator.
- Pre-draft notification templates during peacetime. During an incident is not the time to wordsmith.

## Cross-References

- See `voice/language-guides/incident-communication-language.md` for stakeholder notification templates
- See `voice/calibration/urgency-calibration.md` for SLA alignment and escalation timing
- See `voice/channel-adaptation/slack-security-channels.md` for real-time channel protocols
