# Application Threat Modeling Methodology

## Purpose

Practical methodology for systematic identification of threats to applications and systems. Combines data flow diagramming, STRIDE analysis, attack tree construction, and control mapping to produce actionable security requirements.

## When to Threat Model

| Trigger | Scope | Depth |
|---------|-------|-------|
| New application/service | Full threat model | Comprehensive |
| Major architectural change | Delta threat model (changed components) | Focused |
| New integration/API | Integration-focused model | Moderate |
| Security incident (post-mortem) | Targeted reassessment | Deep |
| Annual review | Full model refresh | Comprehensive |
| Pre-pentest scoping | Attack surface validation | Moderate |

## Phase 1: Data Flow Diagram (DFD) Creation

### DFD Elements

| Symbol | Element | Description |
|--------|---------|-------------|
| Rectangle | External Entity | Users, third-party systems, external APIs |
| Rounded rectangle | Process | Application components that transform data |
| Open rectangle | Data Store | Databases, file systems, caches, queues |
| Arrow | Data Flow | Movement of data between elements |
| Dashed line | Trust Boundary | Separation between trust zones |

### Trust Boundary Examples
- Internet / DMZ boundary
- DMZ / internal network boundary
- Application tier / database tier boundary
- User context / admin context boundary
- Organization / third-party boundary
- Container / host boundary

### DFD Levels

| Level | Detail | Use Case |
|-------|--------|----------|
| Level 0 (Context) | Single process, all external entities | Executive overview, scope definition |
| Level 1 (System) | Major components and data stores | Architecture review, initial threat ID |
| Level 2 (Component) | Detailed processes, all data flows | Full threat analysis, control mapping |

## Phase 2: STRIDE per Element

### STRIDE Categories

| Threat | Property Violated | Description |
|--------|-------------------|-------------|
| **S**poofing | Authentication | Pretending to be another entity |
| **T**ampering | Integrity | Unauthorized modification of data |
| **R**epudiation | Non-repudiation | Denying having performed an action |
| **I**nformation Disclosure | Confidentiality | Exposing data to unauthorized parties |
| **D**enial of Service | Availability | Making a resource unavailable |
| **E**levation of Privilege | Authorization | Gaining unauthorized access level |

### STRIDE Applicability Matrix

| DFD Element | S | T | R | I | D | E |
|-------------|---|---|---|---|---|---|
| External Entity | X | | X | | | |
| Process | X | X | X | X | X | X |
| Data Store | | X | | X | X | |
| Data Flow | | X | | X | X | |

### STRIDE Analysis Template

For each applicable threat per element:

```
Element: [Name]
Threat Category: [STRIDE letter]
Threat Description: [Specific threat scenario]
Attack Vector: [How the attack is executed]
Likelihood: [High/Medium/Low]
Impact: [High/Medium/Low]
Risk Rating: [Critical/High/Medium/Low]
Existing Controls: [Current mitigations]
Recommended Controls: [Additional mitigations needed]
```

## Phase 3: Attack Trees

### Construction Method

1. Define root goal (e.g., "Exfiltrate customer PII")
2. Decompose into sub-goals using AND/OR nodes
3. Continue decomposition until leaf nodes are atomic attack steps
4. Annotate leaves with difficulty, cost, detectability
5. Identify cheapest/easiest paths (most likely attack paths)

### Example Attack Tree

```
Root: Steal customer credentials
├── OR: Exploit application vulnerability
│   ├── AND: SQL injection in login form
│   │   ├── Find injection point
│   │   └── Extract credential table
│   └── AND: Stored XSS to steal session
│       ├── Inject payload in user input
│       └── Capture session cookie via C2
├── OR: Compromise credential store
│   ├── AND: Access database directly
│   │   ├── Exploit exposed management port
│   │   └── Use default credentials
│   └── AND: Access backup files
│       ├── Find backup location
│       └── Download unencrypted backup
└── OR: Social engineering
    ├── Phish administrator credentials
    └── Insider threat (malicious admin)
```

## Phase 4: Risk Ranking

### Risk Matrix

| | Impact: Low | Impact: Medium | Impact: High | Impact: Critical |
|---|---|---|---|---|
| **Likelihood: High** | Medium | High | Critical | Critical |
| **Likelihood: Medium** | Low | Medium | High | Critical |
| **Likelihood: Low** | Low | Low | Medium | High |
| **Likelihood: Very Low** | Informational | Low | Low | Medium |

### Prioritization Factors
- Exploitability: Is there a known exploit? Is it trivial?
- Asset value: What data/function is at risk?
- Exposure: Internet-facing? Internal only?
- Existing controls: What mitigations are in place?
- Regulatory impact: Compliance implications?

## Phase 5: Control Mapping

### Control Selection by Threat

| Threat | Preventive Controls | Detective Controls |
|--------|--------------------|--------------------|
| Spoofing | Strong authentication, mutual TLS, API keys | Authentication anomaly detection, impossible travel |
| Tampering | Input validation, digital signatures, HMAC | Integrity monitoring, hash verification |
| Repudiation | Audit logging, digital signatures, timestamps | Log analysis, SIEM correlation |
| Info Disclosure | Encryption, access controls, data masking | DLP, access monitoring, anomaly detection |
| DoS | Rate limiting, auto-scaling, input validation | Traffic analysis, availability monitoring |
| Elevation of Privilege | RBAC, least privilege, input validation | Privilege usage monitoring, PAM |

## Deliverables

1. **DFD diagrams** (Level 0 and Level 1 minimum)
2. **Threat register** (all identified threats with STRIDE classification)
3. **Attack trees** for top 3-5 critical paths
4. **Risk-ranked findings** with severity and likelihood
5. **Control recommendations** mapped to each threat
6. **Residual risk assessment** after proposed controls

## Cross-References

- [Threat Model Brief Template](../templates/briefs/threat-model-brief.md) -- engagement template
- [STRIDE and ATT&CK Mapping](../lib/taxonomies/attack-technique-taxonomy.md) -- technique taxonomy
- [API Security Architecture](api-security-architecture.md) -- API-specific threat modeling
- [Threat Model to Controls Workflow](../workflows/threat-model-to-controls-workflow.md) -- operationalization
