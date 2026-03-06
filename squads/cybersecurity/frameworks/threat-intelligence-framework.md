# Threat Intelligence Framework

## Purpose

Structured methodology for the threat intelligence lifecycle, enabling intelligence-driven security operations. This framework transforms raw data into actionable intelligence through disciplined collection, analysis, and dissemination processes.

## Intelligence Lifecycle

### Phase 1: Planning & Direction

| Activity | Description | Output |
|----------|-------------|--------|
| Requirements gathering | Identify stakeholder intelligence needs | Priority Intelligence Requirements (PIRs) |
| Collection planning | Define sources, methods, frequency | Collection Management Framework (CMF) |
| Scope definition | Set geographic, industry, threat boundaries | Intelligence scope document |
| Resource allocation | Assign analysts, tools, budgets | Staffing and tooling plan |

**Priority Intelligence Requirements (PIRs):**
- What threat actors are targeting our industry vertical?
- What TTPs are actively used against our technology stack?
- What vulnerabilities are being weaponized in the wild?
- What infrastructure overlaps exist with known adversary campaigns?

### Phase 2: Collection

**Source Categories:**

| Source Type | Examples | Reliability | Timeliness |
|-------------|----------|-------------|------------|
| OSINT | Threat feeds, paste sites, forums | Variable (B-E) | Near real-time |
| HUMINT | Industry contacts, ISACs, law enforcement | High (A-B) | Variable |
| SIGINT | Network telemetry, DNS logs, honeypots | High (A-B) | Real-time |
| TECHINT | Malware samples, exploit kits, C2 infra | High (A-B) | Hours to days |
| SOCMINT | Social media, dark web forums | Variable (C-E) | Near real-time |

### Phase 3: Processing

- Normalization: Convert data to STIX 2.1 format
- Deduplication: Merge overlapping indicators
- Enrichment: Add context (geolocation, WHOIS, passive DNS)
- Correlation: Link indicators to campaigns and actors
- Storage: Ingest into Threat Intelligence Platform (TIP)

### Phase 4: Analysis

**Diamond Model Integration:**

```
         Adversary
            |
   Capability --- Infrastructure
            |
          Victim
```

Each intrusion event maps to these four vertices. Analysis explores:
- **Adversary-Capability axis:** What tools does this actor prefer?
- **Adversary-Infrastructure axis:** What hosting, domains, C2 patterns?
- **Capability-Victim axis:** Which capabilities target which victim profiles?
- **Infrastructure-Victim axis:** How does infrastructure relate to targeting?

**Analytic Techniques:**
- Structured Analytic Techniques (SATs): ACH, key assumptions check, red hat analysis
- Kill chain mapping: Map intelligence to Cyber Kill Chain or MITRE ATT&CK phases
- Campaign tracking: Link discrete events into coherent campaigns
- Trend analysis: Identify shifts in adversary behavior over time

### Phase 5: Dissemination

| Product Type | Audience | Frequency | Format |
|-------------|----------|-----------|--------|
| Strategic brief | Executives, board | Quarterly | PDF/presentation |
| Tactical report | SOC, IR teams | Weekly/ad-hoc | TIP/wiki |
| Operational alert | Defenders | Real-time | SIEM/SOAR integration |
| Technical indicators | Security tools | Continuous | STIX/TAXII, CSV |

### Phase 6: Feedback

- Consumer satisfaction surveys (quarterly)
- Intelligence product effectiveness metrics
- PIR relevance review (bi-annual)
- Collection gap identification
- Analyst skill development tracking

## Confidence Levels

| Level | Label | Description |
|-------|-------|-------------|
| 1 | Confirmed | Corroborated by multiple independent, reliable sources |
| 2 | Probable | Logical inference from reliable source(s) |
| 3 | Possible | Some evidence supports, but not fully corroborated |
| 4 | Doubtful | Limited evidence, significant uncertainty |
| 5 | Improbable | Contradicted by reliable information |

## Traffic Light Protocol (TLP) Handling

| TLP Level | Sharing Scope | Handling Rules |
|-----------|---------------|----------------|
| TLP:RED | Named recipients only | No further sharing, verbal/in-person only |
| TLP:AMBER+STRICT | Organization only | No sharing outside organization |
| TLP:AMBER | Organization + need-to-know partners | Limited sharing with trusted partners |
| TLP:GREEN | Community | Shareable within sector/community, not public |
| TLP:CLEAR | Unrestricted | Public sharing permitted |

## Cross-References

- [Detection Coverage Matrix](detection-coverage-matrix.md) -- map intelligence to detection rules
- [Adversary Simulation Framework](adversary-simulation-framework.md) -- use intelligence to drive red team scenarios
- [Incident Severity Classification](incident-severity-classification.md) -- intelligence context informs severity
- [MITRE ATT&CK Technique Taxonomy](../lib/taxonomies/attack-technique-taxonomy.md) -- TTP classification
