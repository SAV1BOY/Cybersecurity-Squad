# Threat Campaign Tracking and Attribution Task

## Purpose

Track, analyze, and document threat campaigns targeting the organization or its sector, connecting individual indicators and incidents into coherent campaign narratives. Campaign tracking transforms isolated alerts into strategic intelligence, enabling predictive defense and informed risk decisions.

## Task Owner
Senior threat intelligence analyst, collaborating with SOC, incident response, and threat hunting teams.

## Frequency
Continuous tracking; campaign reports updated as new intelligence emerges; quarterly campaign landscape review.

---

## Campaign Identification

### 1.1 Campaign Indicators
A campaign is a coordinated set of adversary activities sharing common objectives, infrastructure, or TTPs. Indicators that multiple events may constitute a campaign:
- [ ] Multiple incidents sharing common IOCs (C2 infrastructure, malware hashes)
- [ ] Similar attack patterns across different targets within the same timeframe
- [ ] Common TTP signatures across incidents (same initial access, same tools)
- [ ] Shared infrastructure (overlapping IP ranges, registrar, SSL certificates)
- [ ] Threat actor attribution linking disparate activities
- [ ] Vendor or ISAC reporting linking events to coordinated activity

### 1.2 Campaign Sources
- Internal incident data and SOC observations
- ISAC advisories and peer sharing
- Commercial threat intelligence reports
- Government advisories (CISA, FBI, NSA joint advisories)
- Open source reporting from security researchers and journalists
- Dark web monitoring (actor communications, marketplace listings)

## Campaign Profile Template

### 2.1 Campaign Record Structure

```
CAMPAIGN PROFILE
=================
Campaign ID: CAMP-[YYYY]-[NNN]
Campaign Name: [Descriptive name or industry name if established]
Status: [Active/Monitoring/Concluded]
First Observed: [Date]
Last Observed: [Date]
Confidence: [High/Medium/Low]
TLP: [Classification level]

ATTRIBUTION
- Attributed Actor: [Threat actor name or "Unattributed"]
- Attribution Confidence: [High/Medium/Low]
- Attribution Basis: [Infrastructure overlap, TTP matching, SIGINT, etc.]

TARGETING
- Sectors: [Industries targeted]
- Geographies: [Regions/countries targeted]
- Organization Types: [Company size, type]
- Targeting Method: [Opportunistic/Targeted/Supply chain]

OBJECTIVE
- Assessed Goal: [Espionage, financial, disruption, access brokering]
- Data Sought: [If data theft: type of data targeted]
- Impact Observed: [Ransomware deployment, data exfiltration, persistence, etc.]

KILL CHAIN
Document the attack progression observed across the campaign:

1. Reconnaissance: [Methods used to identify targets]
2. Weaponization: [Exploit/payload preparation]
3. Delivery: [Phishing, watering hole, supply chain, exploitation]
4. Exploitation: [CVEs exploited, zero-days used]
5. Installation: [Malware deployed, persistence established]
6. C2: [Command and control infrastructure and protocols]
7. Actions on Objectives: [Data theft, ransomware, destruction]

TTP MAPPING (MITRE ATT&CK)
[ATT&CK technique IDs with specific implementation details]

INFRASTRUCTURE
- C2 Servers: [IP addresses, domains]
- Delivery Infrastructure: [Phishing domains, watering hole sites]
- Staging: [Data staging infrastructure]
- Exfiltration: [Exfiltration endpoints]
- Infrastructure Patterns: [Hosting providers, registrars, SSL patterns]

MALWARE AND TOOLS
- [Tool/Malware name]: [Description, hashes, capabilities]
- [Legitimate tools abused]: [Description of use]

IOC SUMMARY
- [Reference to full IOC list in TI platform]
- [Key distinguishing IOCs]

TIMELINE
[Chronological list of campaign events]
- [Date]: [Event description]
- [Date]: [Event description]

DETECTION
- [Detection rules deployed for this campaign]
- [Hunt queries that would identify campaign activity]
- [Network signatures]

ORGANIZATIONAL IMPACT
- [Have we been targeted by this campaign?]
- [Evidence of targeting/compromise]
- [Actions taken in response]

INTELLIGENCE GAPS
- [What remains unknown]
- [Collection requirements]
```

## Campaign Analysis Process

### 3.1 Diamond Model Analysis
For each campaign, apply the Diamond Model:
- **Adversary**: Who is conducting the campaign? (known or characterized)
- **Capability**: What tools, exploits, and techniques are being used?
- **Infrastructure**: What infrastructure supports the campaign?
- **Victim**: Who is being targeted and why?

Analyze relationships between vertices to identify patterns and predict future activity.

### 3.2 Kill Chain Analysis
- [ ] Map all observed campaign activity to kill chain phases
- [ ] Identify which phases have strong detection coverage
- [ ] Identify phases where detection is weak or absent
- [ ] Determine optimal disruption points (where can we break the chain?)
- [ ] Develop detection rules for each phase

### 3.3 Temporal Analysis
- [ ] Build timeline of all campaign events
- [ ] Identify operational patterns (time zones, working hours, holiday pauses)
- [ ] Detect infrastructure rotation patterns
- [ ] Predict likely next actions based on campaign progression
- [ ] Assess campaign lifecycle stage (early, active, winding down)

### 3.4 Infrastructure Pivoting
From known campaign infrastructure, pivot to discover additional elements:
- [ ] Passive DNS: what other domains resolve to known C2 IPs?
- [ ] WHOIS: what other domains share registration details?
- [ ] SSL certificates: what other IPs use the same certificate?
- [ ] Hosting: what other infrastructure uses the same hosting provider/ASN?
- [ ] Code similarity: do malware samples share code with other known tools?

## Operationalizing Campaign Intelligence

### 4.1 Defensive Actions
For active campaigns targeting our sector:
- [ ] Deploy all known IOCs to detection and prevention systems
- [ ] Create detection rules for campaign-specific TTPs
- [ ] Issue targeted threat advisory to affected business units
- [ ] Initiate proactive threat hunt for campaign indicators
- [ ] Brief SOC on campaign TTPs and detection expectations
- [ ] Validate existing controls against campaign kill chain

### 4.2 Proactive Measures
- [ ] Pre-position detection for likely next-phase TTPs
- [ ] Harden systems against known exploitation methods
- [ ] Increase monitoring sensitivity for targeted systems
- [ ] Prepare incident response procedures specific to campaign scenario
- [ ] Coordinate with ISAC peers for shared defense

### 4.3 Executive Briefing
For significant campaigns:
- [ ] Prepare executive-level campaign summary
- [ ] Quantify potential business impact if campaign succeeds
- [ ] Describe defensive posture and confidence level
- [ ] Recommend resource allocation for defense enhancement
- [ ] Provide context on peer organization impacts (if public)

## Campaign Lifecycle Management

### 5.1 Active Monitoring
- [ ] Continuously update campaign profile with new intelligence
- [ ] Track infrastructure changes and IOC evolution
- [ ] Monitor for campaign targeting expansion or pivot
- [ ] Share intelligence with trusted peers and ISACs
- [ ] Update detection rules as campaign TTPs evolve

### 5.2 Campaign Conclusion
When campaign activity ceases:
- [ ] Assess whether campaign concluded, paused, or pivoted
- [ ] Document final campaign scope and impact assessment
- [ ] Archive campaign profile with all collected intelligence
- [ ] Retain detection rules for potential campaign resurgence
- [ ] Produce lessons-learned report for defensive improvements

### 5.3 Quarterly Campaign Landscape Review
- [ ] Review all tracked campaigns: active, monitoring, concluded
- [ ] Assess overall threat landscape trends
- [ ] Identify emerging campaign patterns and new actor activity
- [ ] Update threat model based on campaign intelligence
- [ ] Inform security strategy and investment priorities

## Cross-References

- `tasks/threat-intel/threat-actor-profiling.md` — Actor attribution
- `tasks/threat-intel/ioc-enrichment.md` — IOC processing
- `tasks/threat-intel/daily-threat-briefing.md` — Briefing integration
- `tasks/threat-intel/vulnerability-intelligence.md` — CVE exploitation in campaigns
- `workflows/threat-hunting-sprint-workflow.md` — Hunt operations
- `workflows/incident-response-workflow.md` — Campaign-related incident handling

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | mitre-att-ck, mitre-atlas |
| Checklists | threat-hunt-quality |
| Templates | reports/technical-report-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: rogue + shannon-runner
