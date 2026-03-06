# Privacy Impact Assessment (DPIA) Checklist

## Purpose

Checklist for conducting Data Protection Impact Assessments covering data mapping, risk analysis, safeguard identification, and documentation requirements. Aligned with GDPR Article 35, CCPA, and general privacy best practices.

## When to Conduct a DPIA

### Mandatory Triggers (GDPR Article 35)

- [ ] Systematic and extensive profiling with significant effects
- [ ] Large-scale processing of special category data (health, biometric, genetic)
- [ ] Systematic monitoring of a publicly accessible area (CCTV)
- [ ] New technology deployment processing personal data
- [ ] Automated decision-making with legal or significant effects
- [ ] Large-scale processing of personal data
- [ ] Matching or combining datasets from different sources
- [ ] Data concerning vulnerable subjects (children, employees, patients)
- [ ] Innovative use of personal data or technology

### Recommended Triggers (Best Practice)

- [ ] New system or application processing personal data
- [ ] Change in data processing purpose or scope
- [ ] New third-party data sharing arrangement
- [ ] Cross-border data transfer
- [ ] Deployment of tracking/monitoring technology (UEBA, DLP, employee monitoring)
- [ ] Merger or acquisition involving personal data
- [ ] Migration to new platform or cloud provider
- [ ] Implementation of AI/ML processing personal data

## Phase 1: Data Mapping

### Data Inventory

| Question | Answer | Documented |
|----------|--------|-----------|
| What personal data is collected? | [List all data elements] | [ ] |
| Data subjects: whose data? | [Employees, customers, partners, public] | [ ] |
| Purpose: why is data collected? | [Specific, explicit, legitimate purpose] | [ ] |
| Legal basis for processing? | [Consent, contract, legitimate interest, legal obligation, vital interest, public task] | [ ] |
| Source of data? | [Directly from subject, third party, public source] | [ ] |
| How is data collected? | [Form, API, automated, manual] | [ ] |
| Where is data stored? | [Systems, locations, jurisdictions] | [ ] |
| Who accesses data? | [Roles, teams, third parties] | [ ] |
| How long is data retained? | [Retention periods per data type] | [ ] |
| How is data destroyed? | [Deletion method, verification] | [ ] |

### Data Flow Diagram

- [ ] Data flow diagram created showing collection, processing, storage, sharing, and deletion
- [ ] All systems processing personal data identified on diagram
- [ ] Third-party data flows identified and documented
- [ ] Cross-border data transfers identified with legal mechanisms
- [ ] Data at rest and in transit identified

### Special Category Data

- [ ] Identified if special category data is processed:
  - [ ] Racial or ethnic origin
  - [ ] Political opinions
  - [ ] Religious or philosophical beliefs
  - [ ] Trade union membership
  - [ ] Genetic data
  - [ ] Biometric data (for identification)
  - [ ] Health data
  - [ ] Sex life or sexual orientation
  - [ ] Criminal convictions and offenses
- [ ] Additional legal basis confirmed for special category processing (Article 9)
- [ ] Enhanced safeguards documented for special category data

## Phase 2: Risk Analysis

### Risk Identification

| Risk Category | Potential Risks | Likelihood | Impact | Risk Level |
|--------------|----------------|------------|--------|-----------|
| Unauthorized access | Data breach, hacking, insider threat | [H/M/L] | [H/M/L] | [Score] |
| Excessive collection | Collecting more data than needed | [H/M/L] | [H/M/L] | [Score] |
| Purpose limitation | Data used for incompatible purpose | [H/M/L] | [H/M/L] | [Score] |
| Data quality | Inaccurate or outdated personal data | [H/M/L] | [H/M/L] | [Score] |
| Retention | Keeping data longer than necessary | [H/M/L] | [H/M/L] | [Score] |
| Data sharing | Unauthorized sharing with third parties | [H/M/L] | [H/M/L] | [Score] |
| Cross-border transfer | Data transferred without legal basis | [H/M/L] | [H/M/L] | [Score] |
| Subject rights | Inability to fulfill data subject requests | [H/M/L] | [H/M/L] | [Score] |
| Re-identification | Pseudonymized data re-identified | [H/M/L] | [H/M/L] | [Score] |
| Discrimination | Processing leads to discriminatory outcomes | [H/M/L] | [H/M/L] | [Score] |
| Function creep | System usage expands beyond original purpose | [H/M/L] | [H/M/L] | [Score] |
| Loss of control | Data subject loses control over their data | [H/M/L] | [H/M/L] | [Score] |

### Impact Assessment for Data Subjects

| Impact Type | Description | Severity |
|------------|-------------|----------|
| Financial | Identity theft, fraud, financial loss | [H/M/L] |
| Physical | Safety risk, physical harm | [H/M/L] |
| Psychological | Distress, anxiety, reputational harm | [H/M/L] |
| Social | Discrimination, social exclusion | [H/M/L] |
| Loss of opportunity | Employment, insurance, credit impact | [H/M/L] |
| Loss of control | Inability to exercise rights | [H/M/L] |

## Phase 3: Safeguards and Mitigations

### Technical Safeguards

- [ ] Data minimization implemented (collect only what is needed)
- [ ] Pseudonymization applied where possible
- [ ] Anonymization applied where feasible (irreversible)
- [ ] Encryption at rest and in transit
- [ ] Access controls restrict access to authorized personnel only
- [ ] Audit logging of all personal data access
- [ ] Data masking in non-production environments
- [ ] Secure deletion capability implemented
- [ ] Backup and recovery includes personal data protection
- [ ] Vulnerability management covers systems processing personal data

### Organizational Safeguards

- [ ] Privacy by design principles applied in system design
- [ ] Privacy by default settings configured (minimum data, maximum protection)
- [ ] Data processing agreements (DPAs) in place with all processors
- [ ] Standard contractual clauses (SCCs) for cross-border transfers
- [ ] Staff training on data protection responsibilities
- [ ] Data protection officer (DPO) consulted
- [ ] Data subject rights procedures tested and functional
- [ ] Incident response plan covers personal data breach notification
- [ ] Regular privacy audits scheduled

### Data Subject Rights Support

| Right | Implementation | Verified |
|-------|---------------|----------|
| Right of access (SAR) | Process to retrieve all personal data for a subject | [ ] |
| Right to rectification | Process to correct inaccurate data | [ ] |
| Right to erasure (right to be forgotten) | Process to delete all personal data | [ ] |
| Right to restrict processing | Process to mark data as restricted | [ ] |
| Right to data portability | Process to export data in machine-readable format | [ ] |
| Right to object | Process to opt-out of processing | [ ] |
| Rights re: automated decision-making | Process for human review of automated decisions | [ ] |
| Right to withdraw consent | Process to revoke consent and stop processing | [ ] |

### Cross-Border Transfer Safeguards

- [ ] Transfer mechanism identified for each cross-border flow
  - [ ] Adequacy decision (if destination country has one)
  - [ ] Standard Contractual Clauses (SCCs) executed
  - [ ] Binding Corporate Rules (BCRs) in place
  - [ ] Explicit consent obtained (limited use)
  - [ ] Transfer Impact Assessment completed
- [ ] Supplementary measures implemented if required
- [ ] Transfer documentation maintained

## Phase 4: Documentation

### DPIA Report Structure

```
1. Project/System Description
   - Name, purpose, scope
   - Data controller and processor details
   - Project timeline and stakeholders

2. Data Processing Description
   - Data elements collected
   - Data subjects
   - Legal basis for each processing activity
   - Data flows and storage
   - Retention periods
   - Third-party sharing

3. Necessity and Proportionality Assessment
   - Is processing necessary for the stated purpose?
   - Is the amount of data proportionate?
   - Could the purpose be achieved with less data?

4. Risk Assessment
   - Risks to data subjects identified and scored
   - Risk treatment decisions (mitigate, accept, avoid, transfer)

5. Safeguards and Mitigations
   - Technical measures
   - Organizational measures
   - Residual risk after mitigations

6. Consultation
   - DPO opinion
   - Supervisory authority consultation (if high residual risk)
   - Data subject consultation (if appropriate)

7. Decision and Approval
   - Approval to proceed / proceed with conditions / do not proceed
   - Approver name, role, date
   - Review date
```

### DPIA Approval

- [ ] DPIA completed by project team
- [ ] DPIA reviewed by Data Protection Officer (DPO)
- [ ] DPIA approved by data controller (senior management)
- [ ] If high residual risk: supervisory authority consulted
- [ ] DPIA review date set (annual or on significant change)
- [ ] DPIA stored in DPIA register

## Ongoing Obligations

- [ ] DPIA reviewed when processing changes significantly
- [ ] DPIA reviewed at minimum annually
- [ ] Data processing register (Article 30) updated
- [ ] Privacy notice updated to reflect processing
- [ ] Third-party agreements reviewed for privacy compliance
- [ ] Monitoring effectiveness of safeguards
- [ ] Breach notification procedures tested

## Cross-References

- [Data Classification Framework](../../frameworks/data-classification-framework.md) -- data classification
- [Data Retention Checklist](data-retention-checklist.md) -- retention compliance
- [DLP Implementation Checklist](dlp-implementation-checklist.md) -- technical safeguards
- [Encryption Audit Checklist](encryption-audit-checklist.md) -- encryption controls
