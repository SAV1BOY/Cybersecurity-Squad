# Healthcare Security

## Purpose

Industry-specific security reference for healthcare organizations. Covers HIPAA compliance, medical device security, electronic health record (EHR) protection, telehealth security, and HITRUST CSF alignment for protecting patient data and clinical systems.

## HIPAA Security Rule Requirements

### Administrative Safeguards (45 CFR 164.308)

| Standard | Key Requirements |
|----------|-----------------|
| Security Management | Risk analysis, risk management, sanctions, activity review |
| Assigned Security Responsibility | Designated security officer |
| Workforce Security | Authorization, clearance, termination procedures |
| Information Access Management | Access authorization, establishment, modification |
| Security Awareness Training | Reminders, malware protection, login monitoring, password management |
| Security Incident Procedures | Response and reporting |
| Contingency Plan | Data backup, disaster recovery, emergency operations |
| Evaluation | Periodic technical and non-technical evaluation |

### Technical Safeguards (45 CFR 164.312)

| Standard | Implementation |
|----------|---------------|
| Access Control | Unique user ID, emergency access, automatic logoff, encryption |
| Audit Controls | Hardware/software/procedural mechanisms for recording access |
| Integrity Controls | Mechanisms to verify ePHI not improperly altered |
| Authentication | Verify identity of person seeking access |
| Transmission Security | Integrity controls, encryption for ePHI in transit |

### Breach Notification Requirements

| Breach Size | Notification Timeline | Notify |
|------------|----------------------|--------|
| 500+ individuals | Within 60 days | HHS, individuals, media |
| <500 individuals | Within 60 days to individuals; annual log to HHS | Individuals, HHS |
| Business associate breach | Report to covered entity "without unreasonable delay" | Covered entity |

### PHI De-identification Methods

**Safe Harbor**: Remove 18 specified identifiers (name, geographic data, dates, phone, email, SSN, MRN, etc.)

**Expert Determination**: Statistical expert certifies risk of identification is "very small."

## Medical Device Security

### FDA Pre-Market Cybersecurity Guidance

| Requirement | Description |
|-------------|-------------|
| Threat modeling | Device-specific threat assessment required |
| SBOM | Software Bill of Materials mandatory |
| Secure development | Evidence of secure development practices |
| Authentication | Multi-factor where appropriate |
| Encryption | Data at rest and in transit |
| Update capability | Ability to patch and update securely |
| Vulnerability disclosure | Coordinated disclosure program required |

### Medical Device Risk Categories

| Category | Examples | Security Considerations |
|----------|---------|----------------------|
| Class I (low risk) | Bandages, tongue depressors | Minimal cybersecurity concern |
| Class II (moderate risk) | Insulin pumps, imaging systems | Network isolation, access control, patching |
| Class III (high risk) | Pacemakers, ventilators | Air-gapped where possible, integrity verification, safety-critical |

### Medical IoT (IoMT) Security Framework

```
1. Asset Inventory
   - Discover all connected medical devices
   - Map communication patterns
   - Identify legacy/unpatchable devices

2. Network Segmentation
   - Dedicated VLAN for medical devices
   - Microsegmentation between device types
   - Firewall rules limiting device communication to required endpoints

3. Monitoring
   - Passive network monitoring (avoid active scanning of medical devices)
   - Anomaly detection on device communication baselines
   - Integration with clinical engineering for maintenance windows

4. Vulnerability Management
   - Coordinated with device manufacturer
   - Risk-based prioritization (patient safety first)
   - Compensating controls for unpatchable devices
   - FDA MedWatch reporting for safety-relevant vulnerabilities

5. Incident Response
   - Clinical impact assessment (patient safety evaluation)
   - Device quarantine procedures that maintain clinical capability
   - Manufacturer notification requirements
   - FDA adverse event reporting when applicable
```

## EHR Security

### EHR Access Control Requirements

| Control | Implementation |
|---------|---------------|
| Role-based access | Clinical role determines data access scope |
| Break-the-glass | Emergency access with mandatory justification and audit |
| Minimum necessary | Access limited to data needed for treatment/operations |
| Patient consent | Patient authorization tracking for disclosures |
| Audit trail | Complete access log with user, time, action, data accessed |
| Automatic logoff | Session timeout after inactivity (15 minutes maximum) |

### EHR Integration Security

- HL7 FHIR API access must be authenticated and authorized
- OAuth 2.0 with SMART on FHIR for third-party app access
- Audit all API access with patient identifier logging
- Rate limiting on bulk data export endpoints
- Consent management for patient-facing apps

## Telehealth Security

| Requirement | Implementation |
|-------------|---------------|
| Platform selection | HIPAA-compliant vendors with BAA |
| Encryption | End-to-end encryption for video/audio |
| Authentication | Provider and patient identity verification |
| Session security | No recording without consent, screen share controls |
| Documentation | Session logs maintained per retention requirements |
| Patient education | Guidance on secure connection practices |

## HITRUST CSF

### Framework Structure

HITRUST CSF maps to 44 control objectives across 14 categories, incorporating:
- HIPAA Security Rule
- NIST Cybersecurity Framework
- PCI-DSS (where applicable)
- ISO 27001/27002
- COBIT
- State regulations

### Certification Levels

| Level | Assessment Type | Validity |
|-------|----------------|----------|
| e1 | Essential, 1 year | Foundational cybersecurity |
| i1 | Implemented, 1 year | Industry best practices |
| r2 | Risk-based, 2 year | Comprehensive, highest assurance |

## Cross-References

- See `reference/industries/government-security.md` for government healthcare overlap
- See `reference/industries/critical-infrastructure-security.md` for healthcare as CI
- See `lib/patterns/authentication-patterns.md` for clinical authentication design
- See `lib/patterns/logging-security-patterns.md` for audit logging requirements
- See `frameworks/governance-layer.md` for compliance program structure
