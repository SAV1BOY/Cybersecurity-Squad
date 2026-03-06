# Security Metrics Collection, Analysis, and Reporting Workflow

## Purpose

Define a structured process for collecting, analyzing, and reporting security metrics to different stakeholder audiences. Effective metrics drive data-informed decision-making, demonstrate security program value, justify budget, and track improvement over time. Bad metrics create noise. This workflow ensures every metric reported is actionable and audience-appropriate.

## Scope

Covers operational security metrics, risk metrics, compliance metrics, and executive-level key risk indicators (KRIs). Spans vulnerability management, incident response, detection engineering, access management, and security program maturity.

---

## Phase 1: Metric Definition and Classification

### 1.1 Metric Categories

| Category | Purpose | Examples |
|----------|---------|---------|
| Operational | Measure day-to-day security operations effectiveness | Alert volume, MTTR, patching SLA compliance |
| Risk | Quantify organizational risk posture | Open critical vulns, risk score trends, exception count |
| Compliance | Track adherence to regulatory and policy requirements | Control implementation %, audit finding closure rate |
| Program Maturity | Measure security program capability growth | CMMI-style maturity levels, ATT&CK coverage % |
| Investment | Justify security spending and demonstrate ROI | Cost per incident, cost avoidance, tool utilization |

### 1.2 Metric Quality Criteria (SMART-S)
Every metric must be:
- **S**pecific: Clearly defined with no ambiguity
- **M**easurable: Quantifiable from available data sources
- **A**ctionable: Drives a decision or behavior change
- **R**elevant: Matters to the audience receiving it
- **T**ime-bound: Measured over a defined period
- **S**ourceable: Can be collected reliably and repeatedly

### 1.3 Anti-Patterns to Avoid
- Vanity metrics (attacks blocked: billions!) that impress but inform nothing
- Metrics without context (100 critical vulns: is that good or bad?)
- Metrics that punish reporting (incident count as negative KPI discourages detection)
- Lagging-only metrics with no leading indicators
- Metrics that cannot be influenced by the security team

## Phase 2: Data Collection Architecture

### 2.1 Data Sources

| Source | Metrics Derived | Collection Method |
|--------|----------------|-------------------|
| SIEM | Alert volume, MTTD, MTTR, detection coverage | API/scheduled reports |
| Vulnerability Scanner | Vuln counts by severity, patching SLA, risk scores | API integration |
| EDR | Endpoint coverage, malware detection, isolation events | Dashboard API |
| IAM/IdP | MFA adoption, access review completion, privilege creep | IdP reporting |
| Ticketing System | Incident counts, resolution times, SLA compliance | API/database query |
| CSPM | Cloud misconfigurations, compliance scores | Platform API |
| Code Scanning | SAST/SCA findings, fix rates, mean time to remediate | CI/CD pipeline data |
| Training Platform | Phishing simulation results, training completion | LMS reporting |

### 2.2 Collection Automation
- [ ] Build automated data collection pipelines (scripts, APIs, scheduled exports)
- [ ] Normalize data into common schema for cross-source analysis
- [ ] Store historical data for trend analysis (minimum 24 months)
- [ ] Validate data quality with automated checks (completeness, freshness)
- [ ] Schedule collection: operational metrics daily, risk metrics weekly, compliance monthly

### 2.3 Data Quality Assurance
- [ ] Define data owners for each metric source
- [ ] Implement anomaly detection on metric values (sudden drops may indicate collection failure)
- [ ] Cross-validate metrics between sources where possible
- [ ] Document calculation methodology for each metric to ensure consistency

## Phase 3: Metric Definitions by Audience

### 3.1 Board / Executive Leadership (Quarterly)
High-level risk posture and program effectiveness:

| Metric | Definition | Target | Visualization |
|--------|-----------|--------|--------------|
| Cyber Risk Score | Composite score across all risk domains (1-100) | > 75 | Gauge chart with trend |
| Material Incidents | Count of incidents with business impact > $X | 0 | Count with YoY comparison |
| Mean Time to Contain | Average time from detection to containment | < 4 hours | Trend line |
| Regulatory Compliance | % of applicable controls implemented | > 95% | Compliance heat map |
| Third-Party Risk | % of critical vendors meeting security requirements | > 90% | Vendor risk summary |
| Security Investment | Security spend as % of IT budget with industry benchmark | 8-12% | Benchmark comparison |

### 3.2 CISO / Security Leadership (Monthly)
Program performance and operational trends:

| Metric | Definition | Target |
|--------|-----------|--------|
| Vulnerability SLA Compliance | % of vulns remediated within SLA by severity | Critical: 95%, High: 90% |
| Detection Coverage | % of ATT&CK techniques with active detections | > 70% |
| Alert-to-Incident Ratio | % of alerts that become confirmed incidents | 5-15% (tuning indicator) |
| Phishing Resilience | Click rate on simulated phishing campaigns | < 5% |
| Cloud Security Posture | CSPM compliance score across all accounts | > 90% |
| Security Debt | Count of overdue vulnerability remediations | Trending downward |
| Privileged Access | Count of standing admin accounts vs JIT-enabled | JIT > 80% |

### 3.3 SOC / Security Operations (Weekly)
Operational performance and workload:

| Metric | Definition | Target |
|--------|-----------|--------|
| Alert Volume | Total alerts by source and severity | Trending stable/down |
| MTTD (Mean Time to Detect) | Time from adversary action to alert generation | < 30 minutes |
| MTTR (Mean Time to Respond) | Time from alert to analyst triage | < 15 minutes |
| MTTC (Mean Time to Contain) | Time from triage to containment | < 2 hours |
| False Positive Rate | % of alerts closed as false positive | < 30% |
| Escalation Rate | % of L1 alerts escalated to L2/L3 | 10-20% |
| Analyst Workload | Alerts per analyst per shift | < 25 |
| Threat Hunt Findings | New detections generated from hunt activities | > 2/month |

### 3.4 Engineering / DevSecOps (Biweekly)
Application and pipeline security:

| Metric | Definition | Target |
|--------|-----------|--------|
| SAST Finding Density | Critical/High findings per 1000 LOC | < 1.0 |
| Dependency Vulnerabilities | Critical/High SCA findings in production | 0 critical, < 10 high |
| Secret Detection | Secrets caught in pipeline vs. committed | 100% catch rate |
| Mean Time to Remediate | Avg days from vuln discovery to fix in code | < 5 days (critical) |
| Pipeline Coverage | % of repos with security scanning enabled | 100% |
| Container Image Risk | % of production images with critical vulns | < 5% |

## Phase 4: Dashboard and Reporting

### 4.1 Dashboard Design Principles
- Lead with the most important metric for the audience
- Show trends over time, not just point-in-time snapshots
- Include targets/thresholds for context (red/yellow/green)
- Enable drill-down from summary to detail
- Update frequency matches audience cadence

### 4.2 Reporting Cadence

| Report | Audience | Frequency | Format |
|--------|----------|-----------|--------|
| Security Operations Dashboard | SOC team | Real-time | Live dashboard |
| Weekly Security Brief | Security leadership | Weekly | 2-page summary |
| Monthly Security Report | CISO, IT leadership | Monthly | 10-page report + dashboard |
| Quarterly Board Report | Board, executives | Quarterly | Executive presentation (10 slides) |
| Annual Security Report | All stakeholders | Annually | Comprehensive program review |

### 4.3 Report Structure (Monthly)
1. Executive Summary (1 paragraph: posture, key changes, top risks)
2. Key Metrics Dashboard (visual, trend-based)
3. Notable Incidents Summary
4. Vulnerability Management Status
5. Compliance Status
6. Project/Initiative Progress
7. Emerging Threats and Recommendations
8. Resource and Budget Status

## Phase 5: Analysis and Action

### 5.1 Trend Analysis
- [ ] Compare metrics month-over-month and quarter-over-quarter
- [ ] Identify statistically significant changes (not just noise)
- [ ] Correlate changes with events (new tool deployment, policy change, incident)
- [ ] Benchmark against industry peers where data is available

### 5.2 Metric-Driven Actions
Every metric should have a defined response when thresholds are breached:
- Green (within target): Continue current operations
- Yellow (approaching threshold): Investigate root cause, adjust resources
- Red (threshold breached): Escalate, implement remediation plan, report to leadership

### 5.3 Continuous Improvement
- [ ] Review metric relevance quarterly (retire stale metrics, add emerging ones)
- [ ] Solicit feedback from report consumers on usefulness
- [ ] Mature from lagging to leading indicators over time
- [ ] Automate manual collection processes
- [ ] Validate that metrics are driving the intended behaviors

## Cross-References

- `frameworks/security-kpi-dashboard.md` — KPI definitions and targets
- `frameworks/risk-scoring-model.md` — Risk score calculation
- `frameworks/detection-coverage-matrix.md` — ATT&CK coverage tracking
- `workflows/red-team-purple-team-cycle.md` — Red/purple team metrics
- `data/registries/findings-registry.md` — Vulnerability data source
- `data/registries/incident-registry.md` — Incident data source
