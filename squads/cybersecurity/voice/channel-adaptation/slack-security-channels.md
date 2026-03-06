# Slack Security Channel Communication Guide

## Purpose

This guide standardizes how the squad communicates in real-time messaging channels (Slack, Microsoft Teams, or equivalent). Security Slack channels are where triage happens, alerts escalate, and coordination occurs in real time. Poorly structured messages in these channels cause delayed response, missed context, and information overload. Well-structured messages accelerate detection and response.

## Channel Architecture

### Recommended Channel Structure

| Channel | Purpose | Audience | Posting Rules |
|---------|---------|----------|---------------|
| `#security-alerts` | Automated alert feed from SIEM/SOAR | SOC team | Automated only, no human chatter |
| `#security-triage` | Human discussion of alerts and triage decisions | SOC analysts, security engineers | Alert-related discussion only |
| `#security-incidents` | Active incident coordination | IR team, invited stakeholders | Only during declared incidents |
| `#security-general` | General security team discussion | All security staff | Open discussion, questions, knowledge sharing |
| `#security-intel` | Threat intelligence sharing | Threat intel, SOC, hunting teams | IOCs, advisories, threat reports |
| `#security-help` | User-facing security questions | All employees | Questions, phishing reports, support |
| `#security-leadership` | Security management coordination | Security managers, CISO | Strategy, budget, staffing, sensitive topics |

### Channel Discipline

- Post in the correct channel. Cross-posting the same message to multiple channels creates noise.
- Use threads for follow-up discussion. Keep the main channel feed scannable.
- Pin important messages: active incident bridges, on-call schedules, runbook links.
- Archive resolved incident channels with a final summary message.

## Alert Formatting

### Automated Alert Format
```
:rotating_light: [SEVERITY] — [ALERT TITLE]
Rule: [Detection rule name/ID]
Source: [SIEM/EDR/WAF/etc.]
Time: [UTC timestamp]
Host: [hostname/IP]
User: [associated user if applicable]
Summary: [One-line description]
Link: [Direct link to alert in SIEM/SOAR]
```

### Human Triage Update Format
```
[ALERT-ID] — TRIAGE UPDATE
Status: [Investigating / Escalated / False Positive / Resolved]
Analyst: @[name]
Findings: [Brief summary of triage outcome]
Action: [Next step or closure rationale]
```

## @Mention Protocols

### When to @mention

| Situation | Mention | Rationale |
|-----------|---------|-----------|
| New SEV-1/SEV-2 alert requiring immediate triage | @oncall-soc | On-call analyst must acknowledge |
| Escalation to senior analyst or team lead | @[specific person] | Named accountability |
| Incident declared | @security-team (group) | All hands awareness |
| Question for specific expertise | @[specific person] | Targeted, not broadcast |
| General FYI or knowledge sharing | No @mention | People will read at their own pace |

### When NOT to @mention

- Do not @channel or @here for informational posts — reserve for genuine urgency
- Do not @mention people who are off-shift unless it is a Tier 1 escalation
- Do not @mention the entire team for a false positive closure — post the update, no ping needed

## Incident Channel Protocols

When an incident is declared, create a dedicated channel: `#incident-[YYYY]-[NNN]-[brief-name]`

### Incident Channel Rules

1. **IC posts only** in the main channel flow for official status updates, decisions, and action items
2. **Threaded discussion** for technical analysis, questions, and coordination
3. **Pinned messages**: Incident summary, bridge/call info, timeline document link, IC identity
4. **Status update cadence**: Every 30 minutes for SEV-1, every 60 minutes for SEV-2
5. **Handoff protocol**: When IC rotates, outgoing IC posts handoff summary and incoming IC confirms with a timestamped message

### Incident Channel Message Format
```
SITREP — [TIMESTAMP UTC] — [IC NAME]
Phase: [Detection/Containment/Eradication/Recovery/Post-Incident]
Elapsed: T+[hours]:[minutes]

STATUS:
[2-3 sentences on current state]

COMPLETED SINCE LAST UPDATE:
- [Action] — [Owner]
- [Action] — [Owner]

IN PROGRESS:
- [Action] — [Owner] — ETA: [time]

BLOCKERS:
- [Blocker] — Need: [what is needed to unblock]

NEXT UPDATE: [timestamp]
```

## Threat Intelligence Sharing Format

```
INTEL — [SEVERITY/RELEVANCE] — [BRIEF TITLE]
Source: [Feed/vendor/ISAC/researcher]
Date: [Publication date]
Relevance: [Direct/Indirect/Awareness]

SUMMARY:
[2-3 sentences on the threat]

IOCs (if applicable):
- [Type]: [Value]
- [Type]: [Value]

ACTION REQUIRED:
- [Specific action: hunt query, detection rule, block list update]
- Owner: @[name or team]

REFERENCE: [Link to full report]
```

## Message Hygiene

### Do
- Use emoji reactions to acknowledge messages without adding noise (thumbs up for "seen," eyes for "looking into it," check mark for "done")
- Edit your messages to correct errors rather than posting corrections as new messages
- Use code blocks for IOCs, commands, log excerpts, and queries
- Set channel topics to reflect current state (e.g., "On-call: @analyst | Active Incidents: 0")

### Do Not
- Share sensitive IOCs, credentials, or PII in channels without appropriate access controls
- Use Slack as the system of record — always create a ticket for anything that needs tracking
- Have extended technical debates in the alert channel — move to a thread or dedicated channel
- Post animated GIFs or memes in operational channels during active incidents

## Integration Recommendations

- SIEM alerts to `#security-alerts` via webhook (structured format, not raw JSON)
- SOAR case creation linked from alert messages
- PagerDuty/Opsgenie integration for on-call escalation
- Ticket system integration showing status updates when Jira/ServiceNow tickets change state

## Cross-References

- See `voice/tone-profiles/incident-commander.md` for IC communication cadence
- See `voice/calibration/urgency-calibration.md` for when to escalate via Slack vs. phone
- See `voice/channel-adaptation/ticketing-systems.md` for creating tickets from Slack discussions
- See `voice/language-guides/incident-communication-language.md` for incident update language
