# Security Metrics Dashboards — Exemplary Models

## Purpose
Reference examples of security metrics dashboards that communicate risk effectively to different audiences.

## Dashboard Tiers

### Tier 1: Board/Executive Dashboard (Quarterly)

**Layout: Single page, 6 key metrics**
```
┌─────────────────────────────────────────────────┐
│  SECURITY POSTURE SUMMARY — Q4 2025             │
├──────────────┬──────────────┬───────────────────┤
│ Risk Score   │ Incidents    │ Compliance        │
│   72/100 ↑   │   3 SEV-1 ↓  │   94% controls ↑  │
│ (prev: 68)   │ (prev: 5)    │ (prev: 89%)       │
├──────────────┴──────────────┴───────────────────┤
│ Key Risks              │ Investment vs Risk      │
│ • Cloud misconfig (H)  │ [scatter plot:          │
│ • 3rd party access (H) │  spend vs risk          │
│ • Legacy systems (M)   │  reduction by area]     │
├────────────────────────┴────────────────────────┤
│ Trend: Mean Time to Remediate (Critical Vulns)  │
│ [line chart: 12-month trend, target line at 7d] │
└─────────────────────────────────────────────────┘
```

**Key metrics for executives:**
- Overall risk score (composite, trending)
- SEV-1/2 incident count (quarter-over-quarter)
- Compliance posture (% controls passing)
- Mean time to remediate critical vulnerabilities
- Security investment ROI (cost avoidance model)
- Top 3 risks requiring board attention

### Tier 2: CISO Operational Dashboard (Weekly)

**Key metrics:**
- Vulnerability backlog by severity (bar chart, aging)
- Detection coverage vs MITRE ATT&CK (heat map)
- Mean time to detect (MTTD) and respond (MTTR)
- Phishing simulation metrics (click rate, report rate)
- Patch compliance by environment (prod, staging, dev)
- Open findings by team and age
- Security tool health (uptime, coverage gaps)
- Threat intel alerts requiring action

### Tier 3: SOC Operational Dashboard (Real-time)

**Key metrics:**
- Alert volume (current vs baseline, by source)
- Alert queue depth and analyst utilization
- Active incidents (count, severity, status)
- Mean time to triage (target: <15 min for SEV-1)
- False positive rate by detection rule
- Endpoint coverage (% assets with EDR active)
- Network anomalies (current vs 30-day baseline)
- IOC match rate from threat feeds

### Tier 4: Engineering Security Dashboard (Sprint-level)

**Key metrics:**
- SAST/DAST findings by severity (new vs resolved)
- Dependency vulnerabilities (new advisories this sprint)
- Code review security coverage (% PRs with security review)
- Container image vulnerabilities (build pipeline)
- Secrets scanning alerts (count, resolved rate)
- Security debt (story points of security backlog)

## Metric Definitions & Formulas

| Metric | Formula | Target |
|--------|---------|--------|
| MTTD | Σ(detection_time - compromise_time) / incidents | <24h |
| MTTR | Σ(resolution_time - detection_time) / incidents | <4h (SEV-1) |
| Patch compliance | patched_systems / total_systems × 100 | >95% |
| Detection coverage | techniques_detected / total_ATT&CK_techniques × 100 | >70% |
| Alert fidelity | true_positives / total_alerts × 100 | >80% |
| Vuln remediation | vulns_fixed_in_SLA / total_vulns × 100 | >90% |

## Visualization Best Practices
- **Use traffic lights sparingly** — they oversimplify; use trend arrows instead
- **Show trends, not snapshots** — 12-month moving average reveals patterns
- **Benchmark against industry** — CISO peers care about relative performance
- **Avoid vanity metrics** — "blocked 1M attacks" means nothing without context
- **Automate data collection** — manual dashboards become stale and unreliable

## Cross-References
- `frameworks/security-kpi-dashboard.md` — KPI framework and definitions
- `templates/trackers/vulnerability-tracker.md` — Vulnerability tracking
- `agents/cyber-chief.md` — Governance and metrics orchestration
