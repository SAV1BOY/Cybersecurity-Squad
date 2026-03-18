# Daily Threat Intelligence Collection and Briefing Preparation

## Purpose

Produce a concise, actionable daily threat intelligence briefing that informs security operations, leadership, and relevant stakeholders about threats that could impact the organization. This task transforms raw intelligence into decisions: what to hunt for, what to block, what to watch.

## Task Owner
Threat intelligence analyst. Rotation schedule recommended to prevent burnout and maintain coverage.

## Frequency
Daily, delivered by 09:00 local time. Weekend/holiday abbreviated version.

---

## Morning Collection Routine (06:00 - 08:00)

### 1.1 Open Source Intelligence (OSINT) Sources
Check the following sources daily and extract relevant items:

**Government and CERT Advisories**
- [ ] CISA Alerts and Advisories (cisa.gov/alerts)
- [ ] US-CERT Current Activity
- [ ] National vulnerability advisories relevant to our stack
- [ ] Sector-specific ISACs (FS-ISAC, H-ISAC, IT-ISAC as applicable)

**Vendor Security Advisories**
- [ ] Microsoft Security Response Center
- [ ] Google Project Zero / Threat Analysis Group
- [ ] Apple Security Updates
- [ ] Vendor advisories for technologies in our stack (check asset registry)

**Threat Intelligence Feeds**
- [ ] Commercial TI platform dashboard (Recorded Future, Mandiant, CrowdStrike)
- [ ] MISP instance: new events and IOCs from sharing partners
- [ ] AlienVault OTX pulses relevant to our sector
- [ ] Abuse.ch feeds (Feodo Tracker, URLhaus, MalwareBazaar)

**Community and Research**
- [ ] Security researcher Twitter/Mastodon lists (curated, not firehose)
- [ ] Reddit r/netsec, r/cybersecurity for emerging discussions
- [ ] Security vendor blogs (Mandiant, Secureworks, Unit 42, Talos)
- [ ] Dark web monitoring alerts (if capability exists)

### 1.2 Internal Intelligence Sources
- [ ] SOC overnight incident summary
- [ ] EDR alert trends from past 24 hours
- [ ] SIEM notable events and correlation alerts
- [ ] Phishing reports from employees
- [ ] Vulnerability scan results (new critical/high findings)
- [ ] Threat hunting findings from active hunts

## Analysis and Prioritization (08:00 - 08:30)

### 2.1 Relevance Filtering
For each collected item, assess organizational relevance:

| Factor | Question | Weight |
|--------|----------|--------|
| Technology match | Does our environment use the affected technology? | High |
| Sector targeting | Is our industry/sector being specifically targeted? | High |
| Exploit availability | Is there a public exploit or active exploitation? | Critical |
| Geographic relevance | Are attacks targeting our operational regions? | Medium |
| Threat actor overlap | Are known adversaries relevant to our organization involved? | High |
| Data type match | Could the attack target data types we hold? | Medium |

### 2.2 Priority Classification

| Priority | Criteria | Action Required |
|----------|----------|----------------|
| FLASH | Active exploitation of our technology stack; sector-targeted campaign in progress | Immediate distribution + action |
| HIGH | New critical vulnerability with exploit in our stack; emerging campaign targeting our sector | Same-day briefing + action planning |
| MEDIUM | Relevant threat with no immediate exploitation evidence; trend worth monitoring | Include in daily briefing |
| LOW | General awareness; affects other sectors or technologies not in our stack | Weekly summary only |

## Briefing Production (08:30 - 09:00)

### 3.1 Briefing Format

```
DAILY THREAT INTELLIGENCE BRIEFING
Date: [DATE] | Classification: [INTERNAL/CONFIDENTIAL]
Prepared by: [Analyst Name]

FLASH ITEMS (Immediate Action Required)
[If any -- these go to SOC and leadership immediately]

HIGH PRIORITY
1. [Title]
   Impact: [What does this mean for us?]
   Action: [What should we do?]
   IOCs: [If applicable, reference IOC enrichment task]

MEDIUM PRIORITY
1. [Title]
   Relevance: [Why this matters to us]
   Monitoring: [What to watch for]

THREAT LANDSCAPE SUMMARY
- [2-3 sentence summary of overall threat activity level]
- [Key trends: ransomware, phishing, APT activity]

VULNERABILITY SPOTLIGHT
- [Notable new CVEs relevant to our stack]
- [Patch status and recommendations]

INTERNAL OBSERVATIONS
- [Notable SOC findings from past 24 hours]
- [Active threat hunts and preliminary findings]

IOC UPDATE
- [New IOCs added to blocklists]
- [IOCs expiring or being deprecated]
```

### 3.2 Distribution
- FLASH items: Immediate Slack/Teams alert to SOC, security leadership, and affected system owners
- Daily briefing: Email to security team, IT leadership, CISO by 09:00
- Weekly digest: Compiled and sent to broader IT and business leadership every Monday

### 3.3 Action Item Tracking
For each action item generated:
- [ ] Assign owner (SOC analyst, vuln management, security engineering)
- [ ] Set deadline (FLASH: 4 hours, HIGH: 24 hours, MEDIUM: 1 week)
- [ ] Track completion in threat intel tracking system
- [ ] Follow up on overdue items in next day's briefing

## Weekly Synthesis (Friday)

### 4.1 Weekly Summary Production
- [ ] Compile the week's most significant intelligence
- [ ] Identify trends and patterns across the week
- [ ] Assess whether threat landscape has materially changed
- [ ] Provide 1-2 strategic observations for leadership
- [ ] Recommend threat hunting hypotheses based on weekly trends
- [ ] Update threat actor tracking if new campaigns emerged

### 4.2 Source Evaluation
- [ ] Assess which sources provided the most actionable intelligence this week
- [ ] Identify gaps in collection (technologies not covered, blind spots)
- [ ] Recommend new sources or feeds to add
- [ ] Remove sources that consistently provide noise without signal

## Tools and Automation

### 5.1 Recommended Tooling
- TI platform for aggregation and enrichment (Recorded Future, ThreatConnect, MISP)
- RSS/Atom feed aggregator for advisory monitoring
- Automated IOC extraction and SIEM integration
- Briefing template system for consistent formatting
- Slack/Teams bot for FLASH distribution

### 5.2 Automation Opportunities
- [ ] Auto-ingest IOCs from trusted feeds into SIEM watchlists
- [ ] Auto-match new CVEs against asset inventory (see `tasks/threat-intel/vulnerability-intelligence.md`)
- [ ] Auto-generate draft briefing from aggregated sources
- [ ] Alert on keyword matches in dark web monitoring

## Cross-References

- `tasks/threat-intel/ioc-enrichment.md` — IOC processing and enrichment
- `tasks/threat-intel/threat-actor-profiling.md` — Threat actor tracking
- `tasks/threat-intel/vulnerability-intelligence.md` — Vulnerability prioritization
- `tasks/threat-intel/campaign-tracking.md` — Campaign tracking
- `workflows/threat-hunting-sprint-workflow.md` — Hunt hypothesis generation
- `workflows/detection-engineering-workflow.md` — Detection rule creation from TI

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | threat-intelligence-framework, mitre-att-ck |
| Checklists | threat-hunt-quality |
| Templates | reports/technical-report-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: rogue + shannon-runner
