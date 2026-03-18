# Third-Party Vendor Security Review Task

## Purpose

Execute individual vendor security assessments as part of the broader third-party risk management program. This task covers the tactical steps for evaluating a single vendor's security posture, from initial questionnaire through final risk determination and ongoing monitoring setup.

## Task Owner
Third-party risk analyst, with support from security engineering for technical reviews.

## Trigger
New vendor onboarding, annual vendor reassessment, vendor risk re-tier due to scope change, or incident at vendor.

---

## Pre-Review Setup

### 1.1 Vendor Information Collection
- [ ] Vendor name, primary contact, security contact
- [ ] Services provided and data types involved
- [ ] Integration type: network, API, data sharing, physical access
- [ ] Contract status: new vendor, renewal, or existing review
- [ ] Assigned risk tier (per `workflows/third-party-risk-assessment.md`)

### 1.2 Data Mapping
- [ ] What organizational data will the vendor access, process, or store?
- [ ] Data classification: public, internal, confidential, restricted
- [ ] Data volume: approximate records or data size
- [ ] Data flow direction: inbound, outbound, bidirectional
- [ ] Data residency: where will data be stored geographically?
- [ ] Retention: how long will the vendor retain data?

## Security Assessment Execution

### 2.1 Questionnaire Review
- [ ] Distribute appropriate questionnaire (SIG/SIG Lite based on tier)
- [ ] Set response deadline (typically 2-3 weeks)
- [ ] Review completed questionnaire for completeness
- [ ] Identify areas requiring follow-up or additional evidence
- [ ] Schedule clarification call if needed

### 2.2 Documentation Review
Request and review the following (based on tier):

| Document | Tier 1 | Tier 2 | Tier 3 |
|----------|--------|--------|--------|
| SOC 2 Type II Report | Required | Required | Optional |
| Penetration Test Summary | Required | Recommended | N/A |
| ISO 27001 Certificate | If applicable | If applicable | N/A |
| Insurance Certificate | Required | Required | N/A |
| BC/DR Test Results | Required | Optional | N/A |
| Security Architecture Diagram | Required | Optional | N/A |
| Data Processing Agreement | Required | Required | Required |
| Privacy Policy | Required | Required | Required |
| Incident Response Plan | Required | Optional | N/A |

### 2.3 SOC 2 Report Analysis
When reviewing SOC 2 Type II reports, focus on:
- [ ] Report period: ensure it covers current/recent period
- [ ] Qualified vs. unqualified opinion
- [ ] Exceptions noted: are they relevant to our use case?
- [ ] Control descriptions: do they meet our requirements?
- [ ] Complementary user entity controls (CUECs): are we responsible for any?
- [ ] Sub-service organizations: who does the vendor rely on?

### 2.4 Technical Assessment (Tier 1)
For critical vendors with direct integration:
- [ ] External attack surface scan (passive, non-intrusive)
- [ ] SSL/TLS configuration assessment of vendor endpoints
- [ ] DNS security validation (SPF, DKIM, DMARC)
- [ ] Review vendor's security rating (BitSight, SecurityScorecard)
- [ ] Assess API security: authentication, rate limiting, encryption
- [ ] Review network connectivity architecture for integration points
- [ ] Validate that vendor access to our systems is least-privilege

## Risk Scoring

### 3.1 Domain Scoring
Score each domain on a 1-5 scale (1=strong, 5=deficient):

| Domain | Score | Notes |
|--------|-------|-------|
| Governance and program maturity | ___ | ___ |
| Access control and identity management | ___ | ___ |
| Data protection and encryption | ___ | ___ |
| Network security | ___ | ___ |
| Application security | ___ | ___ |
| Incident response readiness | ___ | ___ |
| Business continuity and DR | ___ | ___ |
| Compliance and certification | ___ | ___ |
| Personnel security | ___ | ___ |
| Physical security (if applicable) | ___ | ___ |

### 3.2 Overall Risk Rating
```
Weighted Average Score -> Risk Rating:
  1.0 - 2.0: Low Risk
  2.1 - 3.0: Medium Risk
  3.1 - 4.0: High Risk
  4.1 - 5.0: Critical Risk
```

### 3.3 Risk Findings
Document specific findings requiring attention:
```
Finding ID: VR-[Vendor]-001
Domain: Data Protection
Finding: Vendor does not encrypt data at rest in their database
Risk: Unauthorized access to our data if vendor systems are compromised
Severity: High
Recommendation: Require encryption at rest with customer-managed or vendor-managed keys
Remediation Timeline: Must be addressed within 90 days of contract signing
```

## Decision and Documentation

### 4.1 Review Decision

| Decision | Criteria | Required Approval |
|----------|----------|-------------------|
| Approve | Low/Medium risk, no critical findings | Risk analyst |
| Approve with Conditions | Medium risk with manageable findings + remediation plan | Security manager |
| Approve with Risk Acceptance | High risk with compensating controls | CISO |
| Reject | Critical risk, unacceptable findings, no remediation path | Security manager |

### 4.2 Conditions and Compensating Controls
If approved with conditions:
- [ ] Document required compensating controls
- [ ] Set remediation deadlines for vendor findings
- [ ] Define monitoring requirements
- [ ] Include security requirements in contract addendum
- [ ] Schedule follow-up assessment to validate remediation

### 4.3 Documentation
- [ ] Complete vendor risk assessment report
- [ ] File all evidence and questionnaire responses
- [ ] Update vendor risk registry
- [ ] Communicate decision to procurement and business owner
- [ ] Set calendar reminders for reassessment date

## Post-Assessment Monitoring

### 5.1 Ongoing Activities
- [ ] Enable automated security rating monitoring for Tier 1-2 vendors
- [ ] Subscribe to vendor security advisories and breach notifications
- [ ] Schedule annual reassessment
- [ ] Monitor for vendor-related threat intelligence
- [ ] Review vendor access logs quarterly

### 5.2 Reassessment Triggers
Reassess outside normal cycle when:
- Vendor experiences a security breach
- Scope of vendor engagement changes significantly
- Vendor undergoes M&A activity
- Vendor's security rating drops significantly
- New regulatory requirements apply

## Cross-References

- `workflows/third-party-risk-assessment.md` — Overarching vendor risk workflow
- `workflows/data-breach-response.md` — If vendor breach affects organization
- `tasks/governance/compliance-gap-analysis.md` — Compliance requirements for vendors
- `archive/notable-breaches/kaseya-2021.md` — MSP vendor compromise case study
- `archive/notable-breaches/target-2013.md` — Vendor-initiated breach case study

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer, cloudsec-layer |
| Checklists | cloud-security-assessment-quality, compliance-audit-quality |
| Templates | reports/risk-assessment-report-template |
| Registry | data/registries/risk-register |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: cyber-chief + omar-santos
