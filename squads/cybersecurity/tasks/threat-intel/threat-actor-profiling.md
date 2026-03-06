# Threat Actor Profiling and Tracking Task

## Purpose

Build and maintain intelligence profiles on threat actors relevant to the organization, enabling threat-informed defense strategies, proactive threat hunting, and risk-based security investment decisions. Knowing your adversary transforms reactive security into anticipatory defense.

## Task Owner
Senior threat intelligence analyst with support from threat hunting and incident response teams.

## Frequency
Profile creation: as new actors are identified. Updates: quarterly or upon significant new intelligence.

---

## Actor Identification and Relevance

### 1.1 Threat Actor Categories

| Category | Motivation | Examples | Relevance Signals |
|----------|-----------|---------|-------------------|
| Nation-State (APT) | Espionage, sabotage, geopolitical | APT28, APT41, Lazarus Group, Sandworm | Sector targeting, geopolitical context |
| Cybercriminal | Financial gain | LockBit, ALPHV/BlackCat, FIN7 | Ransomware/fraud targeting our sector |
| Hacktivist | Ideological, political | Anonymous, KillNet, IT Army of Ukraine | Public statements targeting our sector |
| Insider | Financial, revenge, ideology | N/A (individual profiles) | Behavioral indicators, HR data |
| Competitor | Competitive advantage | N/A (sector-specific) | Espionage targeting our IP |

### 1.2 Relevance Assessment
An actor warrants profiling if:
- [ ] Known to target our industry sector
- [ ] Known to target our geographic region of operations
- [ ] Has capability to exploit technologies in our environment
- [ ] Has been attributed to incidents at peer organizations
- [ ] Threat intelligence indicates active campaigns against our sector
- [ ] Law enforcement or government advisory specifically warns about them

## Profile Template

### 2.1 Actor Profile Structure

```
THREAT ACTOR PROFILE
====================
Name: [Primary name]
Aliases: [Known alternative names across vendors]
Type: [APT/Criminal/Hacktivist/Insider]
Origin: [Attributed country/region, if known]
First Observed: [Date of earliest known activity]
Last Observed: [Date of most recent known activity]
Status: [Active/Dormant/Disbanded]
Confidence in Attribution: [High/Medium/Low]

MOTIVATION AND OBJECTIVES
- Primary motivation: [Espionage/Financial/Destructive/Political]
- Known objectives: [Data theft, ransomware deployment, disruption, etc.]
- Target sectors: [Finance, Healthcare, Government, Tech, etc.]
- Target geographies: [Countries/regions]
- Target data types: [PII, IP, financial, credentials, etc.]

CAPABILITY ASSESSMENT
- Technical sophistication: [Low/Medium/High/Advanced]
- Custom tooling: [Yes/No - list known custom tools]
- Zero-day usage: [Known to use/develop zero-days]
- Operational security: [Level of OPSEC discipline]
- Persistence: [Typical dwell time before detection]
- Scale: [Number of operations/targets typically concurrent]

TACTICS, TECHNIQUES, AND PROCEDURES (TTPs)
[Map to MITRE ATT&CK framework]

Initial Access:
- [T1566 - Phishing: specific methods]
- [T1190 - Exploit Public-Facing Application: preferred targets]
- [T1195 - Supply Chain Compromise: known instances]

Execution:
- [Techniques with specifics]

Persistence:
- [Preferred persistence mechanisms]

Privilege Escalation:
- [Common escalation paths]

Defense Evasion:
- [Notable evasion techniques]

Credential Access:
- [Credential harvesting methods]

Discovery:
- [Internal reconnaissance patterns]

Lateral Movement:
- [Movement techniques]

Collection:
- [Data staging and collection methods]

Exfiltration:
- [Preferred exfiltration channels]

KNOWN TOOLING
- [Tool name]: [Description, detection signatures]
- [Custom malware families]
- [Legitimate tools abused (LOLBins)]

KNOWN INFRASTRUCTURE
- [Infrastructure patterns: hosting preferences, domain registration]
- [C2 protocols and patterns]
- [Current known IOCs: reference IOC enrichment task]

HISTORICAL CAMPAIGNS
1. [Campaign name/date]: [Brief description, targets, outcome]
2. [Campaign name/date]: [Brief description, targets, outcome]

DETECTION OPPORTUNITIES
- [Specific detection rules mapped to actor TTPs]
- [Behavioral analytics that would identify this actor]
- [Network signatures for known infrastructure]

INTELLIGENCE GAPS
- [What we do not know about this actor]
- [Collection requirements to fill gaps]
```

## Profile Development Process

### 3.1 Initial Research
- [ ] Aggregate reporting from multiple vendors on the same actor
- [ ] Reconcile naming conventions across vendors (use MITRE ATT&CK groups as baseline)
- [ ] Compile all known TTPs with specific technical details
- [ ] Map TTPs to MITRE ATT&CK Navigator for visual representation
- [ ] Collect all known IOCs and infrastructure patterns
- [ ] Review academic and government research papers

### 3.2 TTP Analysis
For each known technique:
- [ ] Document specific implementation details (not just technique ID)
- [ ] Identify variations and evolution over time
- [ ] Assess which techniques are signature vs. common/shared
- [ ] Map detection coverage for each technique in our environment
- [ ] Identify gaps where we would not detect this actor's techniques

### 3.3 Infrastructure Analysis
- [ ] Map known C2 infrastructure patterns (hosting, registrars, ASNs)
- [ ] Identify infrastructure reuse across campaigns
- [ ] Track infrastructure rotation patterns and timelines
- [ ] Document DNS patterns (DGA characteristics, domain naming conventions)
- [ ] Profile SSL certificate patterns used by the actor

## Operationalizing Profiles

### 4.1 Detection Engineering
For each profiled actor:
- [ ] Create detection rules for actor-specific TTPs (see `workflows/detection-engineering-workflow.md`)
- [ ] Deploy known IOCs to detection systems (see `tasks/threat-intel/ioc-enrichment.md`)
- [ ] Build threat hunting hypotheses based on actor behavior patterns
- [ ] Create ATT&CK Navigator layer showing detection coverage vs. actor TTPs

### 4.2 Threat Hunting
- [ ] Generate hunt hypotheses based on actor TTPs not covered by detection rules
- [ ] Prioritize hunts for TTPs of highest-relevance actors
- [ ] Use actor profiles to scope hunt investigations
- [ ] Reference: `workflows/threat-hunting-sprint-workflow.md`

### 4.3 Red Team Emulation
- [ ] Provide actor profiles to red team for adversary emulation exercises
- [ ] Prioritize emulation of actors most relevant to the organization
- [ ] Validate detection coverage through emulation
- [ ] Reference: `workflows/red-team-purple-team-cycle.md`

### 4.4 Executive Communication
- [ ] Prepare executive-level actor summaries for board briefings
- [ ] Contextualize threat landscape in terms of specific adversaries
- [ ] Justify security investments based on actor capabilities and targeting

## Profile Maintenance

### 5.1 Update Triggers
- New vendor reporting on the actor
- Actor attributed to new campaign or incident
- New tooling or TTPs observed
- Changes in actor targeting (new sectors, new geographies)
- Actor infrastructure changes
- Law enforcement action against the actor

### 5.2 Quarterly Review
- [ ] Review all active profiles for current relevance
- [ ] Update TTP mappings with new intelligence
- [ ] Refresh IOC sets and infrastructure tracking
- [ ] Reassess detection coverage against updated profiles
- [ ] Archive profiles for dormant/disbanded actors
- [ ] Identify newly relevant actors requiring profiling

## Cross-References

- `tasks/threat-intel/campaign-tracking.md` — Campaign-level tracking
- `tasks/threat-intel/ioc-enrichment.md` — IOC enrichment for actor infrastructure
- `tasks/threat-intel/daily-threat-briefing.md` — Incorporating actor intel into briefings
- `workflows/red-team-purple-team-cycle.md` — Adversary emulation
- `frameworks/detection-coverage-matrix.md` — ATT&CK detection coverage
- `workflows/threat-hunting-sprint-workflow.md` — Hunt hypothesis generation
