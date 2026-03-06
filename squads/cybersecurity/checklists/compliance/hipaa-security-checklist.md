# HIPAA Security Rule Compliance Checklist

## Purpose / When to Use

Execute this checklist when assessing, implementing, or auditing compliance with the HIPAA Security Rule (45 CFR Part 164, Subpart C). This covers all required and addressable implementation specifications across administrative, physical, and technical safeguards for electronic Protected Health Information (ePHI). Use for internal audits, OCR audit preparation, and risk management programs.

## Prerequisites

- [ ] HIPAA Security Rule text available (45 CFR 164.302-164.318)
- [ ] Inventory of all systems creating, receiving, maintaining, or transmitting ePHI
- [ ] Previous risk assessment and management plan available for review
- [ ] Business Associate Agreements (BAAs) compiled for all third parties with ePHI access
- [ ] Designated Security Officer identified (required under the rule)
- [ ] Understanding of "Required" vs. "Addressable" implementation specifications

---

## Phase 1 -- Risk Analysis (Section 164.308(a)(1))

- [ ] Comprehensive risk analysis performed covering all ePHI:
  - [ ] All ePHI repositories identified (EHR, databases, file shares, email, mobile devices, paper-to-digital)
  - [ ] ePHI data flows mapped (creation, receipt, maintenance, transmission)
  - [ ] Threats and vulnerabilities identified for each ePHI repository
  - [ ] Likelihood and impact assessed for each threat-vulnerability pair
  - [ ] Risk levels assigned and documented
- [ ] Risk analysis is current (performed when significant environment changes occur)
- [ ] Risk management plan documents how each identified risk is addressed:
  - Mitigated: control implemented to reduce risk
  - Accepted: risk formally accepted by management with justification
  - Transferred: risk transferred via insurance or BAA
  - Avoided: activity discontinued to eliminate risk
- [ ] Sanction policy exists for workforce members who violate security policies
- [ ] Information system activity review performed regularly (log review)

## Phase 2 -- Administrative Safeguards (Section 164.308)

### Workforce Security (a)(3)
- [ ] Authorization procedures for workforce access to ePHI based on role
- [ ] Workforce clearance procedures implemented (background checks where appropriate)
- [ ] Termination procedures ensure access revocation within 24 hours of departure
  ```
  Termination checklist: disable account, revoke VPN, collect devices,
  remove from distribution lists, revoke badge access
  ```

### Information Access Management (a)(4)
- [ ] Access authorization policies define who approves ePHI access
- [ ] Access establishment and modification procedures documented
- [ ] Healthcare clearinghouse isolation (if applicable): ePHI isolated from larger organization

### Security Awareness and Training (a)(5)
- [ ] Security reminders provided to workforce (newsletters, alerts, posters)
- [ ] Protection from malicious software training provided
- [ ] Login monitoring training: workforce knows how to identify unauthorized access
- [ ] Password management training: creation, protection, and change requirements

### Security Incident Procedures (a)(6)
- [ ] Security incident response plan documented
- [ ] Incident identification, reporting, and response procedures defined
- [ ] Incidents documented with outcomes and follow-up actions
- [ ] Integration with Breach Notification Rule (164.400-414):
  - Breach risk assessment methodology defined
  - Notification timelines documented (60 days for individuals, annual for HHS)
  - Notification templates prepared

### Contingency Plan (a)(7)
- [ ] Data backup plan: ePHI backup frequency, retention, and verification
  ```bash
  # Verify backup integrity
  sha256sum /backup/ephi_database_$(date +%Y%m%d).bak
  # Test restoration quarterly
  ```
- [ ] Disaster recovery plan: procedures to restore ePHI access after emergency
- [ ] Emergency mode operation plan: critical business processes during crisis
- [ ] Testing and revision: contingency plan tested annually and updated
- [ ] Applications and data criticality analysis completed (prioritization for recovery)

### Evaluation (a)(8)
- [ ] Technical and non-technical evaluation performed periodically
- [ ] Evaluation triggered by environmental or operational changes
- [ ] Evaluation results documented with remediation tracking

### Business Associate Contracts (b)(1)
- [ ] All business associates identified and documented
- [ ] BAA in place with each business associate
- [ ] BAAs include required provisions:
  - Use/disclosure limitations
  - Appropriate safeguards requirement
  - Reporting obligations (breaches, security incidents)
  - Subcontractor obligations (downstream BAAs)
  - Return/destruction of ePHI at termination
- [ ] Business associate compliance monitoring procedures in place

## Phase 3 -- Physical Safeguards (Section 164.310)

### Facility Access Controls (a)
- [ ] Contingency operations: procedures for facility access during disaster recovery
- [ ] Facility security plan: physical access controls documented
  - Badge/key card access to ePHI processing areas
  - Visitor sign-in and escort procedures
  - Security cameras at entry points
- [ ] Access control and validation procedures for areas containing ePHI systems
- [ ] Maintenance records: documentation of physical security repairs and modifications

### Workstation Use (b)
- [ ] Policies specify proper workstation use when accessing ePHI:
  - Screen positioning to prevent unauthorized viewing
  - Auto-lock timeout (15 minutes maximum)
  - Clean desk policy for printed ePHI
  - Restrictions on ePHI access from public areas

### Workstation Security (c)
- [ ] Physical safeguards for workstations accessing ePHI:
  - Cable locks for laptops
  - Secured areas for desktop workstations
  - Encrypted hard drives on all portable devices

### Device and Media Controls (d)
- [ ] Disposal procedures: ePHI media sanitized before disposal
  ```bash
  # NIST SP 800-88 compliant media sanitization
  # For HDDs: DoD 5220.22-M or physical destruction
  # For SSDs: manufacturer secure erase or physical destruction
  shred -vfz -n 3 /dev/sdX  # Not sufficient for SSDs
  ```
- [ ] Media re-use procedures: ePHI removed before media re-use
- [ ] Accountability: records of hardware and media movements
- [ ] Data backup and storage: copies of ePHI before equipment movement

## Phase 4 -- Technical Safeguards (Section 164.312)

### Access Control (a)
- [ ] Unique user identification: each user has a unique ID
  ```
  No shared accounts for ePHI systems
  Service accounts individually trackable
  ```
- [ ] Emergency access procedure: mechanism for ePHI access during emergencies
  - Break-glass accounts configured and monitored
  - Emergency access logged and reviewed post-event
- [ ] Automatic logoff: sessions terminate after period of inactivity (15 minutes)
- [ ] Encryption and decryption: ePHI encrypted at rest
  - Database-level encryption (TDE or field-level)
  - Full disk encryption on all endpoints (BitLocker, FileVault, LUKS)
  - Encryption key management per `checklists/crypto/key-management-checklist.md`

### Audit Controls (b)
- [ ] Hardware, software, and procedural mechanisms to record and examine access to ePHI
- [ ] Audit logs capture: user, action, date/time, resource, outcome
- [ ] Audit logs reviewed regularly (at least monthly)
- [ ] Log retention defined (minimum 6 years for HIPAA documentation)
- [ ] Logs protected from unauthorized modification

### Integrity Controls (c)
- [ ] Mechanisms to protect ePHI from improper alteration or destruction
  - File integrity monitoring on ePHI databases
  - Database audit trails for record modification
  - Version control on clinical documents
- [ ] Authentication of ePHI: verify data has not been altered in transit or storage

### Person or Entity Authentication (d)
- [ ] Procedures to verify identity of persons seeking access to ePHI
  - Multi-factor authentication for remote access
  - Strong password requirements (length, complexity)
  - Biometric or token-based authentication for high-sensitivity systems

### Transmission Security (e)
- [ ] Integrity controls: mechanisms to protect ePHI during transmission (checksums, digital signatures)
- [ ] Encryption: ePHI encrypted during transmission over electronic networks
  - TLS 1.2+ for all web and API communication
  - Encrypted email (TLS, S/MIME, or secure messaging platform)
  - VPN for remote network access
  - Refer to `checklists/crypto/tls-ssl-audit-checklist.md`

## Phase 5 -- Documentation and Evidence

- [ ] All policies and procedures documented and dated
- [ ] Documentation retained for 6 years from date of creation or last effective date
- [ ] Policies reviewed and updated periodically (at least annually)
- [ ] Training records maintained for all workforce members
- [ ] Risk assessment documentation current and accessible
- [ ] Incident response records maintained with resolution documentation
- [ ] BAA inventory current with copies of all agreements
- [ ] Compile evidence portfolio for OCR audit readiness:
  - Risk analysis report
  - Risk management plan with status tracking
  - Policies and procedures with version history
  - Training completion records
  - Audit log samples and review documentation
  - Incident response records
  - BAA copies and monitoring evidence

---

## Cross-References

- Encryption implementation: `checklists/crypto/cryptographic-implementation-checklist.md`
- Key management: `checklists/crypto/key-management-checklist.md`
- TLS audit: `checklists/crypto/tls-ssl-audit-checklist.md`
- Incident response: `checklists/incident-response/initial-triage-checklist.md`
- Access control: `checklists/cloud/cloud-iam-least-privilege.md`
- NIST SP 800-66r2: Implementing the HIPAA Security Rule
- HHS Security Rule Guidance: https://www.hhs.gov/hipaa/for-professionals/security/guidance/
