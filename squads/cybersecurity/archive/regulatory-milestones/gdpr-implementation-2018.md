# GDPR Implementation and Early Enforcement (2018)

## Overview

| Field | Details |
|-------|---------|
| Regulation | General Data Protection Regulation (EU) 2016/679 |
| Adopted | April 14, 2016 |
| Enforcement Date | May 25, 2018 |
| Scope | Any organization processing personal data of EU/EEA residents |
| Supervisory Authority | National Data Protection Authorities (DPAs) in each EU member state |
| Maximum Fine | 4% of annual global turnover or 20 million EUR, whichever is greater |

---

## Core Requirements for Security Teams

### Data Protection Principles (Article 5)
1. **Lawfulness, fairness, transparency**: Legal basis required for all personal data processing
2. **Purpose limitation**: Data collected for specific, explicit, and legitimate purposes only
3. **Data minimization**: Only collect data that is necessary for the stated purpose
4. **Accuracy**: Personal data must be kept accurate and up to date
5. **Storage limitation**: Data retained only as long as necessary
6. **Integrity and confidentiality**: Appropriate security measures to protect data
7. **Accountability**: Organization must demonstrate compliance

### Security-Specific Obligations

**Article 32: Security of Processing**
Implement appropriate technical and organizational measures including:
- [ ] Pseudonymization and encryption of personal data
- [ ] Ability to ensure ongoing confidentiality, integrity, availability, and resilience
- [ ] Ability to restore access to data in a timely manner after an incident
- [ ] Regular testing, assessing, and evaluating effectiveness of security measures

**Article 33: Breach Notification to Supervisory Authority**
- Notify DPA within **72 hours** of becoming aware of a personal data breach
- Notification must include: nature of breach, categories of data subjects, approximate numbers, likely consequences, measures taken
- If notification cannot be made within 72 hours, provide reasons for delay
- Document all breaches regardless of whether notification is required

**Article 34: Communication to Data Subjects**
- Required when breach is likely to result in "high risk to rights and freedoms"
- Must describe the breach in clear, plain language
- Not required if: data was encrypted, risk has been mitigated, or it would involve disproportionate effort (in which case public communication is acceptable)

**Article 35: Data Protection Impact Assessment (DPIA)**
Required when processing is likely to result in high risk:
- Systematic and extensive profiling with significant effects
- Large-scale processing of special category data
- Systematic monitoring of publicly accessible areas
- Security teams should be involved in DPIA technical assessment

**Article 25: Data Protection by Design and Default**
- Privacy must be built into systems from the start, not bolted on
- Default settings should be the most privacy-protective
- Security architecture reviews must include privacy considerations

### Data Subject Rights (Security Team Impact)
Security teams must support infrastructure for:
- [ ] **Right of access** (Article 15): Ability to locate and export all data related to an individual
- [ ] **Right to erasure** (Article 17): Ability to delete individual's data across all systems
- [ ] **Right to portability** (Article 20): Export data in machine-readable format
- [ ] **Breach notification**: Technical capability to detect, assess, and report breaches within 72 hours

## Key Enforcement Actions (Lessons Learned)

### Notable Fines and Decisions

| Organization | Fine | Year | Violation | Lesson |
|-------------|------|------|-----------|--------|
| Meta (Ireland) | 1.2B EUR | 2023 | Inadequate legal basis for EU-US data transfers | Data transfer mechanisms must be legally validated |
| Amazon (Luxembourg) | 746M EUR | 2021 | Non-compliant data processing for advertising | Consent mechanisms must be clear and specific |
| WhatsApp (Ireland) | 225M EUR | 2021 | Transparency failures in privacy notices | Privacy policies must be genuinely informative |
| Google (France) | 150M EUR | 2022 | Cookie consent mechanism made rejection difficult | Rejecting cookies must be as easy as accepting them |
| H&M (Germany) | 35.3M EUR | 2020 | Excessive employee surveillance | Employee monitoring must be proportionate |
| British Airways | 20M GBP | 2020 | Inadequate security measures leading to breach | Technical security controls must be appropriate |
| Marriott | 18.4M GBP | 2020 | Failure to perform adequate due diligence on acquired IT systems | M&A security assessment is critical |

### Key Enforcement Themes
1. **Security measures must be proportionate to risk**: Generic security is insufficient; risk-based approach required
2. **Breach notification timing is strict**: 72-hour clock starts when organization becomes "aware" of breach
3. **Accountability requires documentation**: Must demonstrate compliance, not just claim it
4. **International transfers require valid mechanisms**: Standard Contractual Clauses (SCCs) now the primary mechanism post-Privacy Shield invalidation
5. **Cookie consent fatigue does not excuse non-compliance**: Technical implementation of consent must be genuine

## Implementation Checklist for Security Teams

### Technical Controls
- [ ] Implement encryption at rest and in transit for all personal data
- [ ] Deploy access controls limiting personal data access to authorized personnel
- [ ] Implement logging and monitoring for personal data access
- [ ] Deploy DLP controls for personal data exfiltration prevention
- [ ] Implement data discovery and classification tools
- [ ] Enable audit trails for data subject request fulfillment

### Process Controls
- [ ] Establish 72-hour breach notification process and test it
- [ ] Integrate DPIA into security architecture review workflow
- [ ] Include privacy considerations in threat modeling
- [ ] Define data retention schedules with automated enforcement
- [ ] Create data processing inventory (Article 30 records)
- [ ] Establish cross-border data transfer risk assessment process

### Organizational Controls
- [ ] Appoint Data Protection Officer (DPO) if required
- [ ] Train all security staff on GDPR requirements relevant to their role
- [ ] Establish communication channel between security team and DPO
- [ ] Include GDPR impact assessment in incident response procedures
- [ ] Conduct regular security testing of systems processing personal data

## Cross-References

- `workflows/data-breach-response.md` — 72-hour notification workflow
- `tasks/governance/compliance-gap-analysis.md` — GDPR gap assessment
- `workflows/security-architecture-review.md` — Privacy by design integration
- `archive/regulatory-milestones/dora-eu-2025.md` — EU regulatory landscape
- `tasks/governance/security-policy-review.md` — Privacy policy requirements
