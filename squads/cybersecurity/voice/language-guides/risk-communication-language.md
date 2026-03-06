# Risk Communication Language Guide

## Purpose

This guide provides frameworks for translating technical security risks into business language that drives executive decision-making. Security teams that cannot articulate risk in business terms get ignored. This guide bridges the gap between "we found a SQL injection" and "we have a $2.4M exposure on our e-commerce revenue stream."

## The Translation Framework

### Technical Finding to Business Risk Pipeline

```
Technical Finding
  --> Threat Scenario (what could happen)
    --> Business Impact (what it costs)
      --> Risk Statement (likelihood x impact)
        --> Recommendation (what to do, what it costs, what it saves)
```

### Example Translation

| Layer | Content |
|-------|---------|
| Technical Finding | Unauthenticated SQL injection in /api/v2/orders endpoint |
| Threat Scenario | Attacker extracts customer database including payment tokens |
| Business Impact | PCI-DSS non-compliance, breach notification costs, customer churn, regulatory fines |
| Risk Statement | High likelihood (public exploit, internet-facing) with estimated $1.8-3.2M total impact based on record count and industry benchmarks |
| Recommendation | Remediate within 7 days. Engineering cost: 40 hours. Alternative: WAF virtual patch in 4 hours as interim measure |

## Risk Quantification Approaches

### FAIR (Factor Analysis of Information Risk)

Use FAIR-aligned language when presenting to risk-literate executives:

- **Loss Event Frequency (LEF)**: "Based on threat intelligence and our exposure profile, we estimate [N] attempts per [time period], with [X]% probability of a successful compromise within [timeframe]."
- **Loss Magnitude**: Break into primary (response costs, fines, remediation) and secondary (reputation, customer loss, stock impact) loss categories.
- **Annualized Loss Expectancy (ALE)**: "The annualized expected loss from this risk is approximately $[X], derived from [frequency] x [magnitude]."

### Benchmark-Based Quantification

When FAIR analysis is not feasible, use industry benchmarks:

- **IBM/Ponemon Cost of a Data Breach Report**: Average cost per record, average total breach cost by industry
- **Verizon DBIR**: Incident frequency by attack pattern and industry vertical
- **Cyber insurance actuarial data**: If available, use the organization's own cyber insurance underwriting data

### Language for Quantified Risk

**Use**:
- "Based on [data source], we estimate the financial exposure at $[range], comprising [breakdown]."
- "Organizations of comparable size and industry have experienced average breach costs of $[X] for incidents involving [data type]."
- "The proposed $[X] investment reduces this exposure by approximately [Y]%, yielding a risk reduction ROI of [ratio]."

**Avoid**:
- False precision: "$4,237,891.23" — use ranges ($4-5M) unless you have actuarial data
- Unbounded estimates: "This could cost millions" — specify the basis and range
- Comparing unlike risks: do not equate a DDoS risk to a data breach risk without acknowledging they have fundamentally different loss profiles

## Risk Appetite and Tolerance Language

### Defining Appetite

- **Risk Appetite**: "The organization is willing to accept up to $[X] in annualized cyber risk exposure to pursue [business objective]."
- **Risk Tolerance**: "For individual risk scenarios, the maximum acceptable exposure without board approval is $[X] or [severity level]."

### Communicating Against Appetite

- "This risk falls within our stated risk appetite. Recommend monitoring with quarterly reassessment."
- "This risk exceeds our tolerance threshold by [amount/percentage]. Escalation to [authority] is required per the risk management framework."
- "Accepting this risk requires a documented risk acceptance signed by [authority level] per policy [reference]."

## Cost-Benefit Analysis Template

```
RISK: [Brief description]
CURRENT EXPOSURE: $[X] annualized (based on [methodology])

OPTION A: [Remediation approach]
  Cost: $[X] (implementation) + $[Y]/year (ongoing)
  Risk Reduction: [X]%
  Residual Exposure: $[X]
  ROI: [X]:1

OPTION B: [Alternative approach]
  Cost: $[X] (implementation) + $[Y]/year (ongoing)
  Risk Reduction: [X]%
  Residual Exposure: $[X]
  ROI: [X]:1

OPTION C: Risk Acceptance
  Cost: $0 implementation
  Risk Reduction: 0%
  Residual Exposure: $[X] (unchanged)
  Acceptance Authority Required: [Role]

RECOMMENDATION: [Option] based on [rationale]
```

## Common Business Impact Categories

When quantifying impact, address each applicable category:

1. **Direct Financial Loss**: Fraud, theft, ransomware payment, system restoration
2. **Regulatory Fines**: GDPR (up to 4% global revenue), HIPAA ($50K-$1.5M per violation category), PCI-DSS (up to $500K/month)
3. **Legal Costs**: Litigation, settlements, legal counsel, class action defense
4. **Operational Disruption**: Revenue lost during downtime, SLA penalties, overtime labor
5. **Notification Costs**: Per-record notification, credit monitoring, call center support
6. **Reputational Impact**: Customer churn, brand value decline, stock price impact (for public companies)
7. **Competitive Impact**: Loss of intellectual property, loss of competitive advantage, contract losses

## Presenting Risk to Different Audiences

| Audience | Lead With | Support With | Avoid |
|----------|----------|-------------|-------|
| Board of Directors | Dollar exposure, strategic risk | Industry benchmarks, peer comparison | Technical details, jargon |
| CFO | Financial impact, ROI of controls | Cost-benefit analysis, insurance implications | Attack chain details |
| CTO/CIO | Technical risk with business context | Architecture impact, technical debt | Pure dollar figures without technical grounding |
| Business Unit Leaders | Impact to their revenue/operations | Customer impact, SLA exposure | Enterprise-wide statistics that feel abstract |

## Cross-References

- See `voice/tone-profiles/executive-advisory.md` for executive communication tone
- See `voice/calibration/technical-depth-calibration.md` for audience-appropriate depth
- See `voice/language-guides/vulnerability-severity-language.md` for severity-specific language
- See `voice/channel-adaptation/presentation-delivery.md` for presenting risk in meetings
