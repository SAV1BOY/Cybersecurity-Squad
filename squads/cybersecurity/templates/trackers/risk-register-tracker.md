# Organizational Risk Register Template

## Purpose

Template for maintaining an organizational cybersecurity risk register. Provides structured tracking of identified risks, risk scoring, treatment decisions, and residual risk monitoring for risk management programs.

---

## [TEMPLATE BEGINS]

# Cybersecurity Risk Register

**Organization**: [Name]
**Last Updated**: [YYYY-MM-DD]
**Risk Owner**: [CISO / Risk Manager]
**Review Cadence**: Quarterly
**Next Review**: [YYYY-MM-DD]

---

## Risk Scoring Methodology

### Likelihood Scale

| Score | Level | Description | Frequency |
|-------|-------|-------------|-----------|
| 5 | Almost Certain | Expected to occur in most circumstances | >90% within 12 months |
| 4 | Likely | Will probably occur in most circumstances | 60-90% within 12 months |
| 3 | Possible | Could occur at some time | 30-60% within 12 months |
| 2 | Unlikely | Could occur but not expected | 10-30% within 12 months |
| 1 | Rare | May occur only in exceptional circumstances | <10% within 12 months |

### Impact Scale

| Score | Level | Financial | Operational | Reputational | Regulatory |
|-------|-------|-----------|-------------|-------------|------------|
| 5 | Critical | >$10M | Business shutdown >1 week | National media, customer exodus | License revocation, criminal |
| 4 | Major | $1M-$10M | Critical services down >24h | Industry media, major customer loss | Significant fines, consent decree |
| 3 | Moderate | $100K-$1M | Non-critical services down >24h | Local media, some customer loss | Minor fines, mandatory remediation |
| 2 | Minor | $10K-$100K | Degraded service <24h | Social media, complaints | Warning, voluntary remediation |
| 1 | Insignificant | <$10K | No noticeable disruption | No external awareness | No regulatory action |

### Risk Rating Matrix

| | Impact 1 | Impact 2 | Impact 3 | Impact 4 | Impact 5 |
|---|---------|---------|---------|---------|---------|
| **Likelihood 5** | 5 (M) | 10 (H) | 15 (H) | 20 (C) | 25 (C) |
| **Likelihood 4** | 4 (L) | 8 (M) | 12 (H) | 16 (H) | 20 (C) |
| **Likelihood 3** | 3 (L) | 6 (M) | 9 (M) | 12 (H) | 15 (H) |
| **Likelihood 2** | 2 (L) | 4 (L) | 6 (M) | 8 (M) | 10 (H) |
| **Likelihood 1** | 1 (L) | 2 (L) | 3 (L) | 4 (L) | 5 (M) |

**C** = Critical (immediate action) | **H** = High (priority treatment) | **M** = Medium (planned treatment) | **L** = Low (monitor)

---

## Risk Register

### Risk Entry Template

| Field | Value |
|-------|-------|
| **Risk ID** | RISK-[NNN] |
| **Risk Title** | [Concise risk statement] |
| **Risk Description** | [Detailed description: threat, vulnerability, and consequence] |
| **Risk Category** | [Technical / Operational / Compliance / Strategic / Third-Party] |
| **Threat Source** | [External attacker / Insider / Natural / Systemic] |
| **Affected Assets** | [Systems, data, processes affected] |
| **Inherent Likelihood** | [1-5] |
| **Inherent Impact** | [1-5] |
| **Inherent Risk Score** | [L x I] |
| **Inherent Risk Rating** | [Critical / High / Medium / Low] |
| **Current Controls** | [Existing mitigations] |
| **Control Effectiveness** | [Effective / Partially Effective / Ineffective] |
| **Residual Likelihood** | [1-5] |
| **Residual Impact** | [1-5] |
| **Residual Risk Score** | [L x I] |
| **Residual Risk Rating** | [Critical / High / Medium / Low] |
| **Treatment Decision** | [Mitigate / Accept / Transfer / Avoid] |
| **Treatment Plan** | [Specific actions to further reduce risk] |
| **Treatment Owner** | [Name / Team] |
| **Treatment Deadline** | [YYYY-MM-DD] |
| **Treatment Status** | [Not Started / In Progress / Complete / Overdue] |
| **Risk Appetite** | [Within / Exceeds] organizational risk appetite |
| **Last Reviewed** | [YYYY-MM-DD] |
| **Reviewer** | [Name] |

---

## Example Risk Entries

### RISK-001: Ransomware Attack

| Field | Value |
|-------|-------|
| Risk Title | Ransomware encrypts critical business systems |
| Risk Category | Technical |
| Inherent Likelihood | 4 (Likely) |
| Inherent Impact | 5 (Critical) |
| Inherent Risk Score | 20 (Critical) |
| Current Controls | EDR, network segmentation, daily backups, email filtering |
| Control Effectiveness | Partially Effective |
| Residual Likelihood | 3 (Possible) |
| Residual Impact | 4 (Major) |
| Residual Risk Score | 12 (High) |
| Treatment Decision | Mitigate |
| Treatment Plan | 1) Implement immutable backups 2) Deploy MFA on all admin access 3) Conduct ransomware tabletop exercise |
| Treatment Owner | SOC Manager |
| Treatment Deadline | [Date] |

### RISK-002: Third-Party Data Breach

| Field | Value |
|-------|-------|
| Risk Title | Critical vendor suffers breach exposing our data |
| Risk Category | Third-Party |
| Inherent Likelihood | 3 (Possible) |
| Inherent Impact | 4 (Major) |
| Inherent Risk Score | 12 (High) |
| Current Controls | Vendor risk assessments, contractual requirements, data minimization |
| Residual Likelihood | 3 (Possible) |
| Residual Impact | 3 (Moderate) |
| Residual Risk Score | 9 (Medium) |
| Treatment Decision | Transfer + Mitigate |
| Treatment Plan | 1) Cyber insurance coverage 2) Quarterly vendor security reviews 3) Data minimization audit |

---

## Risk Treatment Summary Dashboard

| Risk ID | Title | Inherent | Residual | Treatment | Status |
|---------|-------|----------|----------|-----------|--------|
| RISK-001 | [Title] | [Score] | [Score] | [Decision] | [Status] |
| RISK-002 | [Title] | [Score] | [Score] | [Decision] | [Status] |

---

## Risk Acceptance Log

| Risk ID | Accepted By | Date | Expiration | Justification |
|---------|-----------|------|-----------|---------------|
| [ID] | [Executive name + title] | [Date] | [Review date] | [Why risk is accepted] |

## [TEMPLATE ENDS]

---

## Cross-References

- See `frameworks/risk-scoring-model.md` for risk scoring methodology
- See `frameworks/governance-layer.md` for risk governance
- See `templates/briefs/threat-landscape-brief.md` for threat context
- See `templates/briefs/security-budget-brief.md` for risk-based budget justification
- See `data/registries/risk-register.md` for operational risk data
