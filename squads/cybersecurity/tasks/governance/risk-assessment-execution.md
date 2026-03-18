# Organizational Risk Assessment Execution Task

## Purpose

Conduct a comprehensive cybersecurity risk assessment to identify, analyze, and prioritize risks to organizational assets, operations, and objectives. This task produces a risk register that drives security investment decisions, control implementation priorities, and executive risk acceptance decisions.

## Task Owner
Risk management lead, supported by security architects, business unit representatives, and compliance team.

## Frequency
Full assessment annually; targeted assessments quarterly or triggered by significant changes.

## Methodology
Based on NIST SP 800-30 (Guide for Conducting Risk Assessments) with elements from ISO 27005 and FAIR (Factor Analysis of Information Risk) for quantitative analysis.

---

## Phase 1: Scope and Context (Week 1)

### 1.1 Define Assessment Scope
- [ ] Identify organizational units, systems, and processes in scope
- [ ] Determine assessment depth: strategic (enterprise-level) or tactical (system-specific)
- [ ] Confirm assessment methodology with stakeholders
- [ ] Identify subject matter experts for each business area
- [ ] Schedule interviews and workshops

### 1.2 Establish Context
- [ ] Document business objectives and strategic priorities
- [ ] Identify critical business processes and their technology dependencies
- [ ] Map data assets by classification and regulatory requirements
- [ ] Review recent threat intelligence relevant to the organization's sector
- [ ] Document existing security controls and their effectiveness ratings
- [ ] Compile previous risk assessment findings and remediation status

## Phase 2: Asset and Threat Identification (Weeks 2-3)

### 2.1 Asset Identification
- [ ] Enumerate critical assets: data, systems, applications, infrastructure
- [ ] Assign asset owners and custodians
- [ ] Classify assets by confidentiality, integrity, and availability requirements
- [ ] Estimate asset value (replacement cost, revenue impact, regulatory penalty)
- [ ] Reference: `data/registries/asset-registry.md`

### 2.2 Threat Identification
- [ ] Identify relevant threat sources:
  - Nation-state actors (targeted espionage, destructive attacks)
  - Cybercriminal organizations (ransomware, financial fraud)
  - Hacktivists (defacement, DDoS, data leaks)
  - Insider threats (malicious and negligent)
  - Natural disasters (affecting availability)
  - Supply chain threats (vendor compromise)
- [ ] Map threat sources to specific threat events (attack scenarios)
- [ ] Assess threat capability and intent for each source
- [ ] Reference industry threat reports (Verizon DBIR, Mandiant M-Trends)

### 2.3 Vulnerability Identification
- [ ] Review vulnerability scan results for technical vulnerabilities
- [ ] Identify process and procedural weaknesses
- [ ] Assess personnel vulnerabilities (training gaps, social engineering susceptibility)
- [ ] Evaluate physical security weaknesses
- [ ] Identify configuration and architecture weaknesses
- [ ] Reference: `data/registries/findings-registry.md`

## Phase 3: Risk Analysis (Weeks 4-5)

### 3.1 Likelihood Assessment
For each threat-vulnerability pair, assess likelihood on a 5-point scale:

| Level | Likelihood | Criteria |
|-------|-----------|----------|
| 5 | Almost Certain | Expected to occur multiple times per year |
| 4 | Likely | Expected to occur at least once per year |
| 3 | Possible | Could occur within 1-3 years |
| 2 | Unlikely | Could occur within 3-5 years |
| 1 | Rare | Could occur but not expected within 5 years |

Factors: threat actor capability, motivation, attack complexity, existing controls.

### 3.2 Impact Assessment
Assess impact across multiple dimensions:

| Dimension | Score 1 (Low) | Score 3 (Medium) | Score 5 (High) |
|-----------|--------------|-------------------|-----------------|
| Financial | < $100K | $100K - $1M | > $1M |
| Operational | Minor disruption, < 4 hours | Significant disruption, 4-24 hours | Critical failure, > 24 hours |
| Reputational | Internal awareness only | Local media coverage | National/international coverage |
| Regulatory | Minor finding, no fine | Formal finding, moderate fine | Major violation, significant fine |
| Safety | No safety impact | Potential for minor injury | Potential for serious harm |

### 3.3 Risk Calculation
```
Risk Score = Likelihood x Impact (maximum impact dimension)

Risk Rating:
  1-5:   Low Risk    (Green)  - Accept and monitor
  6-12:  Medium Risk (Yellow) - Mitigate within 6 months
  13-19: High Risk   (Orange) - Mitigate within 90 days
  20-25: Critical    (Red)    - Immediate action required
```

### 3.4 Quantitative Analysis (FAIR) for Top Risks
For the top 10 risks, perform FAIR analysis:
- [ ] Estimate loss event frequency (threat event frequency x vulnerability)
- [ ] Estimate loss magnitude (primary + secondary losses)
- [ ] Calculate annualized loss expectancy (ALE) range
- [ ] Use Monte Carlo simulation for confidence intervals
- [ ] Express risk in financial terms for executive communication

## Phase 4: Risk Evaluation and Treatment (Week 6)

### 4.1 Risk Prioritization
- [ ] Rank all identified risks by risk score
- [ ] Group risks by domain for treatment planning
- [ ] Identify risks that exceed organizational risk appetite
- [ ] Flag risks with regulatory compliance implications

### 4.2 Treatment Options
For each risk above acceptable threshold:

| Treatment | When to Apply | Documentation |
|-----------|--------------|---------------|
| Mitigate | Control can reduce risk to acceptable level | Control implementation plan with timeline |
| Transfer | Insurance or contractual transfer is cost-effective | Insurance policy or contract clause |
| Avoid | Eliminate the risk by removing the activity | Business decision documentation |
| Accept | Cost of mitigation exceeds risk value | Formal risk acceptance signed by owner |

### 4.3 Control Recommendations
For risks designated for mitigation:
- [ ] Identify specific controls to reduce likelihood or impact
- [ ] Estimate implementation cost and timeline
- [ ] Calculate residual risk after control implementation
- [ ] Prioritize controls by risk reduction per dollar invested

## Phase 5: Reporting and Tracking (Week 7)

### 5.1 Risk Register Update
Update `data/registries/risk-register.md` with:
- [ ] All identified risks with unique IDs
- [ ] Likelihood and impact scores with justification
- [ ] Treatment decisions and responsible owners
- [ ] Remediation timelines and milestones
- [ ] Residual risk after planned treatment

### 5.2 Executive Risk Report
- [ ] Risk heat map (likelihood vs. impact matrix)
- [ ] Top 10 risks with business context
- [ ] Year-over-year risk trend analysis
- [ ] Resource requirements for risk treatment
- [ ] Risk acceptance requests requiring executive approval

### 5.3 Ongoing Monitoring
- [ ] Schedule quarterly risk register reviews
- [ ] Track treatment plan progress monthly
- [ ] Trigger reassessment on significant organizational changes
- [ ] Update risk scores based on new threat intelligence or incidents

## Cross-References

- `data/registries/risk-register.md` — Risk register documentation
- `frameworks/risk-scoring-model.md` — Risk scoring methodology
- `tasks/governance/compliance-gap-analysis.md` — Compliance integration
- `tasks/governance/security-policy-review.md` — Policy alignment
- `workflows/security-metrics-reporting.md` — Risk metric reporting
- `frameworks/nist-csf.md` — NIST CSF risk management functions

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | fair-risk-quantification, governance-layer |
| Checklists | compliance-audit-quality |
| Templates | reports/risk-assessment-report-template |
| Registry | data/registries/risk-register |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: cyber-chief + omar-santos
