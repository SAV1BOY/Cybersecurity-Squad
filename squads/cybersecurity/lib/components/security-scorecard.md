# Security Posture Scorecard

## Purpose

Provide a structured security posture scorecard that quantifies organizational security across key domains, tracks trends over time, and enables benchmark comparison. The scorecard transforms complex security data into an executive-friendly format that communicates posture, progress, and areas requiring investment.

## When to Use
- Monthly security leadership reporting
- Quarterly board/executive presentations
- Annual security program review
- Budget justification and resource allocation
- Peer benchmarking and maturity comparison

---

## Scorecard Structure

### Overall Security Score
```
+============================================+
|     ORGANIZATIONAL SECURITY SCORE          |
|                                            |
|              [76 / 100]                    |
|              GOOD                          |
|                                            |
|  Trend: +4 from last quarter              |
|  Industry Average: 68                      |
+============================================+
```

### Score Ranges

| Range | Rating | Color | Interpretation |
|-------|--------|-------|---------------|
| 90-100 | Excellent | Dark Green | Industry-leading security posture |
| 80-89 | Very Good | Green | Strong posture with minor improvement areas |
| 70-79 | Good | Light Green | Solid foundation; known gaps being addressed |
| 60-69 | Fair | Yellow | Notable gaps requiring attention and investment |
| 50-59 | Poor | Orange | Significant weaknesses; increased risk exposure |
| 0-49 | Critical | Red | Fundamental deficiencies requiring urgent action |

## Domain Scores

### Scorecard Domain Grid

```
Domain                    Score   Trend   Target  Status
==========================================================
1. Identity & Access       78      +3      85     [=====---]
2. Endpoint Security       82      +5      85     [=======-]
3. Network Security        71      -2      80     [====----]
4. Application Security    65      +7      80     [===-----]
5. Data Protection         73      +1      80     [====----]
6. Cloud Security          69      +8      85     [===-----]
7. Incident Response       81      +2      85     [=======-]
8. Vulnerability Mgmt      74      +3      80     [====----]
9. Governance & Risk       80      0       85     [======--]
10. Security Operations    77      +4      85     [=====---]
==========================================================
Composite Score:           76      +3      83
```

## Domain Definitions and Metrics

### Domain 1: Identity and Access Management (Weight: 12%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| MFA adoption (all users) | 25% | 100% | 94% | 94 |
| Phishing-resistant MFA (admin) | 20% | 100% | 72% | 72 |
| Privileged access with JIT | 20% | 100% | 60% | 60 |
| Access review completion | 15% | 100% | 88% | 88 |
| Orphaned accounts | 10% | 0 | 12 | 70 |
| Password policy compliance | 10% | 100% | 95% | 95 |
| **Domain Score** | | | | **78** |

### Domain 2: Endpoint Security (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| EDR coverage | 30% | 100% | 98% | 98 |
| OS patch compliance (30-day) | 25% | 95% | 89% | 89 |
| Endpoint encryption | 20% | 100% | 99% | 99 |
| Application allowlisting (critical) | 15% | 100% | 45% | 45 |
| USB device control | 10% | 100% | 92% | 92 |
| **Domain Score** | | | | **82** |

### Domain 3: Network Security (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| Network segmentation maturity | 25% | Tier 3 | Tier 2 | 67 |
| Firewall rule review currency | 20% | < 12 months | 8 months | 85 |
| DNS security (DNSSEC, filtering) | 15% | 100% | 80% | 80 |
| TLS enforcement (internal) | 15% | 100% | 68% | 68 |
| IDS/IPS coverage | 15% | 100% | 75% | 75 |
| Wireless security compliance | 10% | 100% | 60% | 60 |
| **Domain Score** | | | | **71** |

### Domain 4: Application Security (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| SAST pipeline coverage | 25% | 100% | 72% | 72 |
| SCA pipeline coverage | 20% | 100% | 68% | 68 |
| Critical app pentest frequency | 20% | Annual | 60% on schedule | 60 |
| Secret detection in pipeline | 15% | 100% | 85% | 85 |
| OWASP Top 10 vuln density | 20% | < 1 per app | 2.3 per app | 43 |
| **Domain Score** | | | | **65** |

### Domain 5: Data Protection (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| Data classification coverage | 25% | 100% | 70% | 70 |
| Encryption at rest (sensitive) | 25% | 100% | 92% | 92 |
| DLP coverage | 20% | 100% | 55% | 55 |
| Backup recovery tested | 20% | Quarterly | Semi-annual | 75 |
| Data retention compliance | 10% | 100% | 80% | 80 |
| **Domain Score** | | | | **73** |

### Domain 6: Cloud Security (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| CSPM compliance score | 25% | > 90% | 78% | 78 |
| IMDSv2 enforcement | 15% | 100% | 60% | 60 |
| Public resource exposure | 20% | 0 critical | 3 | 55 |
| Cloud audit log coverage | 20% | 100% | 95% | 95 |
| IAM least privilege score | 20% | > 85% | 62% | 62 |
| **Domain Score** | | | | **69** |

### Domain 7: Incident Response (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| Mean time to detect (MTTD) | 25% | < 1 hour | 45 min | 90 |
| Mean time to contain (MTTC) | 25% | < 4 hours | 3.5 hours | 85 |
| IR plan tested (tabletop) | 20% | Quarterly | Quarterly | 100 |
| Forensic readiness | 15% | Full capability | 70% ready | 70 |
| Post-incident review completion | 15% | 100% | 90% | 90 |
| **Domain Score** | | | | **81** |

### Domain 8: Vulnerability Management (Weight: 8%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| Scan coverage (assets scanned) | 20% | 100% | 92% | 92 |
| Critical vuln remediation SLA | 30% | 95% within 7 days | 78% | 78 |
| High vuln remediation SLA | 25% | 90% within 30 days | 72% | 72 |
| CISA KEV remediation | 15% | 100% within 48 hours | 85% | 85 |
| Vulnerability trend | 10% | Decreasing | Stable | 50 |
| **Domain Score** | | | | **74** |

### Domain 9: Governance and Risk (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| Policy review currency | 20% | 100% < 12 months | 90% | 90 |
| Risk assessment completion | 20% | Annual | Completed | 100 |
| Compliance framework coverage | 20% | > 90% controls | 85% | 85 |
| Security awareness training | 15% | > 95% completion | 92% | 92 |
| Third-party risk assessments | 15% | 100% Tier 1-2 | 70% | 70 |
| Board reporting cadence | 10% | Quarterly | Quarterly | 100 |
| **Domain Score** | | | | **80** |

### Domain 10: Security Operations (Weight: 10%)

| Metric | Weight | Target | Current | Score |
|--------|--------|--------|---------|-------|
| 24/7 monitoring coverage | 20% | 100% | 100% | 100 |
| Alert-to-incident ratio | 15% | 5-15% | 12% | 85 |
| Detection rule coverage (ATT&CK) | 25% | > 70% | 58% | 58 |
| Threat hunt frequency | 20% | Monthly | Monthly | 100 |
| Log source coverage | 20% | > 95% | 82% | 82 |
| **Domain Score** | | | | **77** |

## Composite Score Calculation

```
Composite Score = SUM(Domain Score x Domain Weight)

= (78 x 0.12) + (82 x 0.10) + (71 x 0.10) + (65 x 0.10) +
  (73 x 0.10) + (69 x 0.10) + (81 x 0.10) + (74 x 0.08) +
  (80 x 0.10) + (77 x 0.10)

= 9.36 + 8.2 + 7.1 + 6.5 + 7.3 + 6.9 + 8.1 + 5.92 + 8.0 + 7.7

= 75.08 ~ 75
```

## Trend Tracking

### Quarterly Trend Chart
```
Score
100 |
 90 |
 80 |          *---*---*---*
 70 |    *---*
 60 |  *
 50 |
    +---+---+---+---+---+---+
     Q1  Q2  Q3  Q4  Q1  Q2
     2025              2026
```

### Domain Trend Table
Track each domain quarterly to identify improvement or degradation:
- Arrow up: improved > 3 points
- Arrow flat: changed < 3 points
- Arrow down: degraded > 3 points

## Benchmark Comparison

Compare against industry peers (use Gartner, ISF, or ISC2 benchmarks):
- Organizational score vs. industry average
- Domain-level comparison to identify relative strengths and weaknesses
- Track closing of gaps against industry leaders

## Presentation Format

### Executive Summary Slide
```
SECURITY POSTURE SCORECARD - Q1 2026

Overall Score: 76/100 (GOOD) [+4 from Q4 2025]

Strongest Domains:         Weakest Domains:
  Endpoint Security: 82      Application Security: 65
  Incident Response: 81      Cloud Security: 69
  Governance & Risk: 80      Network Security: 71

Key Improvements This Quarter:
  + Cloud security +8 (CSPM deployment completed)
  + Application security +7 (pipeline scanning expanded)
  + Endpoint security +5 (EDR deployment completed)

Key Risks:
  - Application security below target (65 vs 80 target)
  - 3 public cloud resources identified
  - Critical vuln SLA compliance at 78% (target 95%)

Recommended Investment:
  1. Application security pipeline completion ($XXK)
  2. Network segmentation project Phase 2 ($XXK)
  3. Cloud IAM remediation project ($XXK)
```

## Cross-References

- `lib/components/risk-heat-map.md` — Risk visualization
- `workflows/security-metrics-reporting.md` — Metrics methodology
- `frameworks/security-kpi-dashboard.md` — KPI definitions
- `tasks/governance/risk-assessment-execution.md` — Risk assessment input
- `tasks/governance/compliance-gap-analysis.md` — Compliance domain input
