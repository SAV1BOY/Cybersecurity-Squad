# Risk Heat Map Component

## Purpose

Provide a visual risk assessment tool that maps identified risks onto a likelihood-versus-impact matrix with color-coded severity zones. Risk heat maps enable rapid communication of risk posture to technical and non-technical stakeholders, facilitate prioritization discussions, and track risk trends over time.

## When to Use
- Risk assessment presentations to executive leadership and boards
- Security program status reporting
- Prioritization workshops for remediation planning
- Audit and compliance reporting
- Vendor risk portfolio visualization

---

## Heat Map Structure

### Standard 5x5 Matrix

```
                          IMPACT
            Negligible  Minor  Moderate  Major  Severe
            (1)        (2)    (3)       (4)    (5)
          +----------+------+--------+-------+--------+
Almost    |          |      |        |       |        |
Certain(5)|  Medium  | High |Critical|Critical|Critical|
          +----------+------+--------+-------+--------+
Likely    |          |      |        |       |        |
       (4)|   Low    |Medium|  High  |Critical|Critical|
          +----------+------+--------+-------+--------+
Possible  |          |      |        |       |        |
       (3)|   Low    | Low  | Medium | High  |Critical|
          +----------+------+--------+-------+--------+
Unlikely  |          |      |        |       |        |
       (2)|   Low    | Low  |  Low   |Medium | High   |
          +----------+------+--------+-------+--------+
Rare      |          |      |        |       |        |
       (1)|   Low    | Low  |  Low   | Low   | Medium |
          +----------+------+--------+-------+--------+
```

### Color Coding

| Zone | Color | Risk Score | Action Required |
|------|-------|-----------|-----------------|
| Critical | Red | 15-25 | Immediate executive attention; remediate within 30 days |
| High | Orange | 10-14 | Senior management attention; remediate within 90 days |
| Medium | Yellow | 5-9 | Management awareness; remediate within 180 days |
| Low | Green | 1-4 | Accept and monitor; address in normal planning cycles |

## Likelihood Assessment Scale

| Level | Score | Definition | Frequency Estimate |
|-------|-------|-----------|-------------------|
| Almost Certain | 5 | Expected to occur; has occurred recently | Multiple times per year |
| Likely | 4 | Will probably occur; strong evidence of targeting | At least once per year |
| Possible | 3 | Could occur; some evidence or historical precedent | Once every 1-3 years |
| Unlikely | 2 | Not expected; would require unusual circumstances | Once every 3-5 years |
| Rare | 1 | Highly unlikely; only in exceptional circumstances | Less than once every 5 years |

### Likelihood Factors
When assessing likelihood, consider:
- [ ] Threat actor capability and motivation (see `tasks/threat-intel/threat-actor-profiling.md`)
- [ ] Vulnerability exploitability (CVSS exploitability metrics, public exploit availability)
- [ ] Existing control effectiveness (how well do current controls reduce likelihood?)
- [ ] Historical incident data (has this type of event occurred before?)
- [ ] Industry benchmarks (how frequently does this affect peer organizations?)
- [ ] Attack surface exposure (internet-facing vs. internal-only)

## Impact Assessment Scale

| Level | Score | Financial | Operational | Reputational | Regulatory |
|-------|-------|----------|-------------|-------------|------------|
| Severe | 5 | > $10M | Core business functions down > 1 week | International media; lasting customer loss | Major fine; consent order; license risk |
| Major | 4 | $1M-$10M | Critical systems down 1-7 days | National media; significant customer impact | Significant fine; formal investigation |
| Moderate | 3 | $100K-$1M | Important systems impaired 1-3 days | Industry/trade media; manageable customer impact | Moderate fine; audit findings |
| Minor | 2 | $10K-$100K | Non-critical disruption < 24 hours | Minimal external awareness | Minor finding; warning |
| Negligible | 1 | < $10K | Minimal operational impact | No external awareness | No regulatory impact |

### Impact Factors
When assessing impact, consider the worst reasonable outcome across:
- [ ] **Financial**: Direct costs, lost revenue, legal/regulatory penalties, remediation costs
- [ ] **Operational**: Business process disruption, recovery time, productivity loss
- [ ] **Reputational**: Media attention, customer trust, brand damage, competitive impact
- [ ] **Regulatory**: Notification obligations, fines, investigations, consent orders
- [ ] **Safety**: Physical safety implications (relevant for OT/healthcare/transportation)

Use the highest impact dimension to determine the overall impact score.

## Building the Heat Map

### Step 1: Identify Risks
Source risks from:
- Organizational risk assessment (see `tasks/governance/risk-assessment-execution.md`)
- Vulnerability scan results and penetration test findings
- Threat intelligence assessments
- Audit findings and compliance gaps
- Incident post-mortem recommendations
- Architecture review findings

### Step 2: Assess Each Risk

| Risk ID | Risk Description | Likelihood | Impact | Score | Zone | Owner |
|---------|-----------------|-----------|--------|-------|------|-------|
| R-001 | Ransomware via phishing | 4 (Likely) | 5 (Severe) | 20 | Critical | CISO |
| R-002 | Cloud misconfiguration data exposure | 3 (Possible) | 4 (Major) | 12 | High | Cloud Sec |
| R-003 | Insider data theft | 2 (Unlikely) | 4 (Major) | 8 | Medium | Security Ops |
| R-004 | DDoS against public website | 3 (Possible) | 2 (Minor) | 6 | Medium | Infrastructure |
| R-005 | Third-party vendor breach | 3 (Possible) | 5 (Severe) | 15 | Critical | GRC |
| R-006 | Unpatched critical CVE exploitation | 4 (Likely) | 3 (Moderate) | 12 | High | Vuln Mgmt |

### Step 3: Plot on Heat Map
Place risk identifiers on the matrix at their assessed coordinates. Multiple risks in the same cell indicate concentration of risk at that level.

### Step 4: Analyze Distribution
Healthy risk distribution characteristics:
- Most risks in green/yellow zones (indicates effective control environment)
- Few risks in red zone (those that exist have active remediation plans)
- No risks in red zone without executive-approved remediation or acceptance

Concerning patterns:
- Clustering in red/orange zones indicates systemic control weakness
- Many risks in same category suggests a common root cause
- No risks in red zone may indicate under-assessment rather than good security

## Trend Analysis

### Tracking Changes Over Time
Maintain quarterly snapshots of the heat map to show:
- Risks that moved from higher to lower zones (remediation success)
- Risks that moved from lower to higher zones (increased threat or degraded controls)
- New risks added to the map
- Risks removed from the map (retired or accepted)

### Trend Visualization
```
Quarter   | Critical | High | Medium | Low | Total
----------|----------|------|--------|-----|------
Q1 2026   |    3     |  7   |   12   |  8  |  30
Q2 2026   |    2     |  5   |   14   |  9  |  30
Q3 2026   |    1     |  4   |   12   | 11  |  28
Q4 2026   |    1     |  3   |   10   | 12  |  26
```

Target: Continuous reduction in critical/high risks; overall risk trending downward.

## Presentation Guidance

### For Board/Executive Audience
- Show the heat map as a visual overview (one slide)
- Highlight critical and high risks only (3-5 maximum)
- Express impact in business terms (revenue, customers, regulatory)
- Show trend comparison to previous quarter
- Include specific ask: budget, authority, or risk acceptance decision

### For Security Leadership
- Full heat map with all risks plotted
- Detailed risk descriptions for critical and high items
- Remediation status and timeline for each
- Resource requirements for risk reduction
- Comparison to industry benchmarks

### For Technical Teams
- Supplement heat map with detailed risk descriptions
- Include specific vulnerabilities and affected systems
- Provide remediation guidance and priority
- Link to relevant playbooks and procedures

## Interactive Elements (Digital Implementation)

For dashboard implementations:
- [ ] Clickable risk items revealing detailed risk description
- [ ] Filter by risk category (technical, operational, compliance, third-party)
- [ ] Filter by risk owner or business unit
- [ ] Toggle between inherent risk (before controls) and residual risk (after controls)
- [ ] Time slider showing risk trend over quarters
- [ ] Drill-down to specific findings and remediation tasks

## Cross-References

- `tasks/governance/risk-assessment-execution.md` — Risk assessment methodology
- `frameworks/risk-scoring-model.md` — Risk scoring framework
- `workflows/security-metrics-reporting.md` — Metrics reporting integration
- `lib/components/security-scorecard.md` — Scorecard component
- `data/registries/risk-register.md` — Risk documentation
