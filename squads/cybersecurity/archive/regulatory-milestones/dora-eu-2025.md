# DORA: EU Digital Operational Resilience Act (2025)

## Overview

| Field | Details |
|-------|---------|
| Title | Regulation (EU) 2022/2554 on Digital Operational Resilience for the Financial Sector |
| Common Name | DORA (Digital Operational Resilience Act) |
| Adopted | November 28, 2022 |
| Enforcement Date | January 17, 2025 |
| Scope | Financial entities operating in the EU and their critical ICT third-party service providers |
| Enforced By | European Supervisory Authorities (EBA, EIOPA, ESMA) and national competent authorities |

---

## Scope and Applicability

### Financial Entities Covered
DORA applies to virtually all regulated financial entities in the EU:
- Credit institutions (banks)
- Payment institutions and electronic money institutions
- Investment firms and trading venues
- Insurance and reinsurance undertakings
- Central securities depositories
- Central counterparties
- Crypto-asset service providers (MiCA-authorized)
- Crowdfunding service providers
- Credit rating agencies
- Pension funds
- Management companies (UCITS, AIFMs)

### Critical ICT Third-Party Service Providers
DORA extends regulatory oversight to third parties:
- Cloud service providers deemed critical to the financial sector
- Data analytics providers
- Core banking platform providers
- Other ICT providers designated by ESAs as critical
- These providers will be subject to direct regulatory oversight framework

## Five Pillars of DORA

### Pillar 1: ICT Risk Management (Articles 5-16)

Financial entities must implement comprehensive ICT risk management:

**Governance Requirements:**
- [ ] Management body must define, approve, and oversee ICT risk management framework
- [ ] Board members must maintain adequate knowledge of ICT risks
- [ ] Specific ICT risk management function must be established
- [ ] Adequate budget allocation for ICT security

**Framework Requirements:**
- [ ] Identify all ICT-supported business functions and assets
- [ ] Classify assets by criticality and map interdependencies
- [ ] Continuous risk assessment process
- [ ] Protection and prevention measures commensurate with risk
- [ ] Detection mechanisms for anomalous activities
- [ ] Business continuity and disaster recovery plans
- [ ] Learning and evolving processes (lessons learned)

**Technical Requirements:**
- [ ] Network security and infrastructure protection
- [ ] Access control and authentication (strong authentication for critical systems)
- [ ] Data integrity, confidentiality, and availability controls
- [ ] Cryptographic controls and key management
- [ ] Patch management and vulnerability remediation
- [ ] Logging, monitoring, and alerting capabilities
- [ ] Physical security of ICT assets

### Pillar 2: ICT-Related Incident Management (Articles 17-23)

**Incident Classification:**
DORA defines criteria for classifying ICT incidents:
- Number of clients/counterparts affected
- Duration of the incident
- Geographic spread
- Data losses (integrity, confidentiality, availability)
- Criticality of affected services
- Economic impact

**Reporting Requirements:**

| Report Type | Timing | Content |
|-------------|--------|---------|
| Initial Notification | Within 4 hours of classification as major; within 24 hours of detection | Nature, classification, impact assessment |
| Intermediate Report | Within 72 hours (or when status materially changes) | Updated information, root cause analysis progress |
| Final Report | Within 1 month of incident resolution | Full root cause, timeline, losses, remediation |

**Incident Management Process:**
- [ ] Implement incident detection and monitoring mechanisms
- [ ] Establish classification process aligned with DORA criteria
- [ ] Define roles and responsibilities for incident response
- [ ] Create communication procedures (internal, regulatory, client)
- [ ] Conduct post-incident reviews and lessons learned
- [ ] Maintain incident register for all ICT-related incidents

### Pillar 3: Digital Operational Resilience Testing (Articles 24-27)

**Basic Testing (All Entities):**
- [ ] Vulnerability assessments and scans
- [ ] Open source analysis
- [ ] Network security assessments
- [ ] Gap analyses
- [ ] Physical security reviews
- [ ] Questionnaires and scanning software solutions
- [ ] Source code reviews (where feasible)
- [ ] Scenario-based tests
- [ ] Compatibility testing
- [ ] Performance testing
- [ ] End-to-end testing
- [ ] Penetration testing

**Threat-Led Penetration Testing (TLPT) - Significant Entities:**
- Required for entities meeting significance criteria
- Based on TIBER-EU framework
- Must cover critical or important functions
- Performed by independent external testers
- At least every 3 years
- Must include threat intelligence phase
- Live production environment testing
- Red team engagement with defined scope
- Results reported to competent authority
- Remediation validated

### Pillar 4: ICT Third-Party Risk Management (Articles 28-44)

**Contractual Requirements:**
All contracts with ICT service providers must include:
- [ ] Clear description of functions and services provided
- [ ] Data protection obligations and locations
- [ ] Service level descriptions with quantitative targets
- [ ] Incident notification obligations
- [ ] Business continuity provisions
- [ ] Termination and transition rights
- [ ] Audit and access rights for the entity and regulators
- [ ] Cooperation with competent authorities
- [ ] Exit strategies and transition plans

**Concentration Risk:**
- [ ] Assess and manage ICT concentration risk
- [ ] Evaluate dependency on critical service providers
- [ ] Develop exit strategies for critical providers
- [ ] Consider substitutability of ICT services
- [ ] Document risk assessment of third-party dependencies

**Oversight Framework for Critical Providers:**
- ESAs designate critical ICT third-party service providers
- Lead Overseer assigned (EBA, EIOPA, or ESMA)
- Direct regulatory powers: information requests, inspections, recommendations
- Annual oversight plans and assessments
- Providers outside EU must establish subsidiary within EU

### Pillar 5: Information Sharing (Article 45)

- Financial entities may exchange cyber threat intelligence among themselves
- Sharing must protect personal data (GDPR compliance)
- Arrangements must define conditions and safeguards for participation
- Entities must notify competent authorities of participation in sharing arrangements

## Implementation Checklist for Security Teams

### Immediate Actions (If Not Already Completed)
- [ ] Conduct gap analysis against DORA requirements
- [ ] Brief board/management on DORA obligations and gaps
- [ ] Inventory all ICT third-party service providers
- [ ] Review existing incident response procedures against DORA classification criteria
- [ ] Assess current resilience testing program against DORA requirements

### ICT Risk Management Framework
- [ ] Document comprehensive ICT risk management framework
- [ ] Map all critical business functions to ICT dependencies
- [ ] Implement continuous monitoring and detection
- [ ] Establish ICT change management procedures
- [ ] Document ICT business continuity plans and test annually

### Incident Reporting
- [ ] Implement incident classification aligned with DORA criteria
- [ ] Build reporting workflows meeting 4-hour/72-hour/1-month timelines
- [ ] Prepare template reports for initial, intermediate, and final notifications
- [ ] Establish communication channel with national competent authority
- [ ] Maintain comprehensive incident register

### Third-Party Management
- [ ] Inventory all ICT third-party relationships
- [ ] Review contracts for DORA-required clauses
- [ ] Assess concentration risk across providers
- [ ] Develop exit strategies for critical providers
- [ ] Implement ongoing monitoring of third-party risk

### Resilience Testing
- [ ] Establish annual resilience testing program
- [ ] Plan TLPT (if entity meets significance thresholds)
- [ ] Engage external testers meeting DORA qualifications
- [ ] Document and remediate all test findings
- [ ] Report TLPT results to competent authority

## Cross-References

- `tasks/governance/compliance-gap-analysis.md` — DORA gap analysis
- `workflows/third-party-risk-assessment.md` — Third-party risk management
- `workflows/incident-response-workflow.md` — Incident response procedures
- `workflows/red-team-purple-team-cycle.md` — TLPT alignment
- `archive/regulatory-milestones/gdpr-implementation-2018.md` — EU regulatory context
- `tasks/governance/vendor-security-review.md` — Vendor assessment for DORA
