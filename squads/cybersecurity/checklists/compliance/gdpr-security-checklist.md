# GDPR Security Requirements Checklist

## Purpose / When to Use

Execute this checklist when assessing compliance with the security requirements of the General Data Protection Regulation (EU 2016/679). While GDPR covers broad data protection principles, this checklist focuses on the security-specific obligations: Article 5(1)(f) integrity and confidentiality, Article 25 data protection by design, Article 32 security of processing, Article 33-34 breach notification, and Articles 35-36 DPIAs. Use for internal audits, DPO assessments, and supervisory authority inspection preparation.

## Prerequisites

- [ ] Data Protection Officer (DPO) designated (if required under Article 37)
- [ ] Records of Processing Activities (ROPA) established (Article 30)
- [ ] Lawful basis determined for each processing activity
- [ ] Data flow mapping completed for personal data
- [ ] Understanding of roles: controller, processor, joint controller
- [ ] Relevant supervisory authority guidelines reviewed (EDPB, national DPAs)

---

## Phase 1 -- Data Mapping and Classification

- [ ] Complete inventory of personal data processing activities:
  - What personal data is collected (categories and specific data elements)
  - Data subjects (employees, customers, patients, children, etc.)
  - Processing purposes and lawful basis for each
  - Data recipients (internal departments, processors, third countries)
  - Retention periods per category
  - Technical and organizational security measures per processing activity
- [ ] Identify special category data (Article 9) requiring enhanced protection:
  - Racial or ethnic origin, political opinions, religious beliefs
  - Trade union membership, genetic data, biometric data
  - Health data, sex life or sexual orientation
- [ ] Map personal data flows across systems, departments, and borders:
  ```
  Source -> Processing System -> Storage -> Recipients -> Deletion
  Include: backups, logs, analytics, archives, third-party integrations
  ```
- [ ] Identify personal data in unstructured sources (email, documents, chat logs, backups)
- [ ] Classify data by sensitivity and volume to determine proportionate security measures

## Phase 2 -- Data Protection Impact Assessments (Article 35)

- [ ] Identify processing activities requiring DPIA:
  - Systematic and extensive profiling with significant effects
  - Large-scale processing of special categories or criminal data
  - Systematic monitoring of publicly accessible areas
  - New technologies with high risk to rights and freedoms
  - Automated decision-making with legal or significant effects
- [ ] For each required DPIA, document:
  - [ ] Description of processing operations and purposes
  - [ ] Assessment of necessity and proportionality
  - [ ] Assessment of risks to data subjects
  - [ ] Measures to address risks (security controls, safeguards)
  - [ ] DPO opinion (if applicable)
  - [ ] Data subject views (if appropriate and feasible)
- [ ] If residual risk remains high after mitigation: consult supervisory authority (Article 36)
- [ ] DPIAs reviewed when processing changes materially
- [ ] DPIA process integrated into project/product development lifecycle

## Phase 3 -- Security of Processing (Article 32)

- [ ] Implement appropriate technical measures based on risk assessment:
  - [ ] **Pseudonymization**: personal identifiers replaced with tokens
    ```
    Database: customer_id (token) -> PII lookup table (restricted access, encrypted)
    Analytics: use pseudonymized data; re-identification requires separate authorization
    ```
  - [ ] **Encryption**: personal data encrypted at rest and in transit
    - At rest: database encryption, full disk encryption on endpoints and servers
    - In transit: TLS 1.2+ for all data transmission
    - Key management per `checklists/crypto/key-management-checklist.md`
  - [ ] **Confidentiality**: access controls, authentication, authorization
    - Role-based access control with least privilege
    - Multi-factor authentication for systems processing personal data
    - Segregation of duties for high-risk processing
  - [ ] **Integrity**: data validation, checksums, audit trails
    - Input validation on all data entry points
    - Database audit logs for personal data modifications
    - File integrity monitoring on systems storing personal data
  - [ ] **Availability**: backup, redundancy, disaster recovery
    - Regular backups with tested restoration procedures
    - System redundancy for critical processing systems
    - Documented RTO and RPO aligned with processing requirements
  - [ ] **Resilience**: ability to restore availability and access following incidents
    - Business continuity planning for personal data processing
    - Incident response procedures tested regularly

- [ ] Implement appropriate organizational measures:
  - [ ] Data protection policies communicated to all staff
  - [ ] Staff training on data protection obligations (role-appropriate)
  - [ ] Confidentiality agreements for employees and contractors
  - [ ] Data processing agreements with all processors (Article 28)
  - [ ] Regular review of security measures for continued appropriateness

- [ ] Security measure selection considers:
  - State of the art (current technology and best practices)
  - Cost of implementation (proportionality)
  - Nature, scope, context, and purposes of processing
  - Risk of varying likelihood and severity to data subject rights

## Phase 4 -- Breach Notification Readiness (Articles 33-34)

- [ ] Breach detection capabilities in place:
  - [ ] SIEM monitoring for unauthorized access to personal data systems
  - [ ] DLP controls detecting unauthorized personal data transfers
  - [ ] Endpoint detection for malware targeting personal data
  - [ ] Database activity monitoring for anomalous queries on personal data tables
  - [ ] Email monitoring for accidental data exposure
- [ ] Breach assessment procedure documented:
  - [ ] Determine if personal data breach occurred (definition: Article 4(12))
  - [ ] Assess risk to rights and freedoms of data subjects:
    - Type of breach (confidentiality, integrity, availability)
    - Nature and sensitivity of personal data affected
    - Number of data subjects affected
    - Severity of consequences for data subjects
  - [ ] Determine if notification thresholds are met
- [ ] Supervisory authority notification (Article 33):
  - [ ] Process to notify within 72 hours of becoming aware
  - [ ] Notification template prepared containing:
    - Nature of breach, categories and approximate number of data subjects
    - Categories and approximate number of records
    - DPO or other contact point
    - Likely consequences
    - Measures taken or proposed to address the breach
  - [ ] Designated personnel authorized to submit notification
  - [ ] Process for phased notification if full information not available within 72 hours
- [ ] Data subject notification (Article 34):
  - [ ] Criteria for notification: breach likely to result in high risk to rights and freedoms
  - [ ] Clear, plain language communication template prepared
  - [ ] Channel for notification identified (email, letter, public communication if direct not feasible)
  - [ ] Exceptions documented: encryption rendering data unintelligible, subsequent measures eliminating risk
- [ ] Breach register maintained (Article 33(5)):
  - All breaches recorded regardless of notification requirement
  - Facts, effects, and remedial actions documented
  - Register available for supervisory authority inspection

## Phase 5 -- Data Subject Rights (Security Aspects)

- [ ] Identity verification for data subject requests:
  - [ ] Process to authenticate data subject before fulfilling requests
  - [ ] Prevent unauthorized disclosure through access requests
  - [ ] Document verification method used for each request
- [ ] Right of access (Article 15): systems can export personal data for a specific individual
  ```
  Capability: query all systems by data subject identifier
  Format: machine-readable, commonly used format
  Timeline: response within 1 month (extendable by 2 months for complex requests)
  ```
- [ ] Right to erasure (Article 17): systems can delete personal data per individual
  - [ ] Deletion cascades to all systems including backups (or backup retention documented)
  - [ ] Verification that deletion is complete (including logs, caches, replicas)
  - [ ] Crypto-shredding capability for encrypted data stores
- [ ] Right to data portability (Article 20): export in structured, machine-readable format
- [ ] Security controls prevent unauthorized modification during rectification requests
- [ ] Automated decision-making (Article 22): ability to provide human review on request

## Phase 6 -- Cross-Border Transfers (Chapter V)

- [ ] Identify all transfers of personal data outside the EEA
- [ ] Verify transfer mechanism for each cross-border flow:
  - [ ] Adequacy decision (Article 45): destination country deemed adequate by EC
  - [ ] Standard Contractual Clauses (Article 46(2)(c)): current version (2021 SCCs) implemented
  - [ ] Binding Corporate Rules (Article 47): approved by lead supervisory authority
  - [ ] Derogations (Article 49): explicit consent, contractual necessity (limited scope)
- [ ] Transfer Impact Assessment (TIA) completed for each transfer relying on SCCs:
  - Laws and practices of destination country assessed
  - Supplementary measures identified if needed (encryption, pseudonymization, access controls)
  - Risk of government access in destination country evaluated
- [ ] Technical supplementary measures for high-risk transfers:
  - [ ] End-to-end encryption where processor in third country does not need plaintext access
  - [ ] Pseudonymization with mapping table retained in EEA
  - [ ] Split processing across jurisdictions so no single location has complete personal data
- [ ] Transfer records maintained and updated when mechanisms change

## Phase 7 -- Documentation and Audit Evidence

- [ ] Records of Processing Activities (Article 30) are current and complete
- [ ] DPIAs documented for all required processing activities
- [ ] Breach register maintained with all incidents documented
- [ ] Data subject request log with response times and outcomes
- [ ] Processor agreements (Article 28) compiled with security annexes
- [ ] Training records for all staff processing personal data
- [ ] Security measure documentation sufficient to demonstrate compliance (Article 5(2) accountability)
- [ ] Policies reviewed annually and updated to reflect regulatory guidance changes
- [ ] Evidence retention: maintain documentation for supervisory authority inspection

---

## Cross-References

- Encryption: `checklists/crypto/cryptographic-implementation-checklist.md`
- Key management: `checklists/crypto/key-management-checklist.md`
- Incident response: `checklists/incident-response/initial-triage-checklist.md`
- Access controls: `checklists/cloud/cloud-iam-least-privilege.md`
- ISO 27001 (common framework): `checklists/compliance/iso27001-audit-checklist.md`
- EDPB Guidelines: https://edpb.europa.eu/our-work-tools/our-documents/guidelines_en
- GDPR Full Text: https://gdpr-info.eu/
