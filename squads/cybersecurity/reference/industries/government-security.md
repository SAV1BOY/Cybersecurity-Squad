# Government and Defense Security

## Purpose

Industry-specific security reference for government and defense organizations. Covers FedRAMP, CMMC, ITAR, classified system requirements, and the federal zero trust mandate (OMB M-22-09) for securing government information systems and defense supply chains.

## FedRAMP (Federal Risk and Authorization Management Program)

### Impact Levels

| Level | Data Types | Examples |
|-------|-----------|---------|
| Low | Public, non-sensitive | Public websites, open data |
| Moderate | CUI, PII, law enforcement sensitive | Most federal workloads (~80%) |
| High | Controlled unclassified, financial, health, law enforcement | DoD, intelligence adjacent, critical systems |

### Authorization Process

```
1. Preparation Phase
   - System categorization (FIPS 199)
   - Security control selection (NIST 800-53)
   - System Security Plan (SSP) development

2. Authorization Phase
   - Security Assessment (3PAO assessment)
   - Security Assessment Report (SAR)
   - Plan of Action and Milestones (POA&M)
   - Authorization decision (JAB or Agency)

3. Continuous Monitoring Phase
   - Monthly vulnerability scanning
   - Annual assessment of subset of controls
   - Significant change management
   - Incident reporting to US-CERT
   - Monthly POA&M updates
```

### FedRAMP Control Counts

| Baseline | Control Families | Total Controls |
|----------|-----------------|---------------|
| Low | 17 | 156 |
| Moderate | 17 | 325 |
| High | 17 | 421 |

## CMMC (Cybersecurity Maturity Model Certification)

### CMMC 2.0 Levels

| Level | Description | Assessment | Requirements |
|-------|-------------|-----------|--------------|
| Level 1 | Foundational | Annual self-assessment | 17 practices (basic cyber hygiene) |
| Level 2 | Advanced | Triennial third-party or self (depends on data) | 110 practices (NIST SP 800-171 aligned) |
| Level 3 | Expert | Government-led assessment | 110+ practices with additional NIST 800-172 |

### CUI (Controlled Unclassified Information) Protection

| Requirement | Implementation |
|-------------|---------------|
| Access Control | Limit system access to authorized users |
| Awareness & Training | Security awareness for all personnel |
| Audit & Accountability | Create, protect, retain system audit logs |
| Configuration Management | Establish and maintain baseline configurations |
| Identification & Authentication | Identify and authenticate users, devices, processes |
| Incident Response | Establish operational IR capability |
| Maintenance | Perform maintenance on organizational systems |
| Media Protection | Protect, sanitize, destroy media containing CUI |
| Personnel Security | Screen individuals prior to CUI access |
| Physical Protection | Limit physical access to systems and equipment |
| Risk Assessment | Periodically assess risk to operations and assets |
| Security Assessment | Assess, monitor, correct security controls |
| System & Communications Protection | Monitor and protect communications at boundaries |
| System & Information Integrity | Identify, report, correct system flaws timely |

## ITAR (International Traffic in Arms Regulations)

### Key Requirements for IT Systems

| Requirement | Implementation |
|-------------|---------------|
| Access control | Only U.S. persons may access ITAR data |
| Cloud hosting | Must be in U.S. data centers with U.S. person administration |
| Encryption | FIPS 140-2/3 validated encryption required |
| Visitor control | Foreign national access logging and restrictions |
| Data marking | All ITAR-controlled documents must be clearly marked |
| Transmission | Encrypted channels only, no foreign routing |
| Incident reporting | Unauthorized disclosure must be reported to DDTC |

### Cloud Compliance for ITAR

- AWS GovCloud, Azure Government, Google Cloud with Assured Workloads
- All personnel with access must be U.S. persons
- Data residency must remain within U.S. borders
- Encryption key management under U.S. person control

## Classified Systems (Overview)

### Classification Levels

| Level | Compromise Impact | Handling |
|-------|------------------|---------|
| Confidential | Damage to national security | Controlled but less restrictive |
| Secret | Serious damage to national security | SIPR network, SCIF for processing |
| Top Secret | Exceptionally grave damage | JWICS, TS/SCI compartments, SCIF required |

### Security Controls for Classified Systems

- Air-gapped networks (no internet connectivity)
- TEMPEST shielding (prevent electromagnetic emanation)
- Continuous monitoring with security-cleared SOC analysts
- Two-person integrity for certain operations
- Destruction standards for media (degaussing, incineration)
- Cross-domain solutions (CDS) for controlled data transfer between classification levels
- Insider threat programs (mandatory per EO 13587)

## Zero Trust Mandate (OMB M-22-09)

### Federal Zero Trust Strategy Pillars

| Pillar | Objective | Key Actions |
|--------|-----------|-------------|
| Identity | Agency staff use enterprise-managed identity with phishing-resistant MFA | Deploy FIDO2/WebAuthn, eliminate SMS/OTP |
| Devices | Maintain complete inventory, detect and respond to incidents on all devices | EDR on all endpoints, device health attestation |
| Networks | Encrypt all DNS, HTTP traffic; segment networks around applications | Encrypted DNS (DoH/DoT), microsegmentation |
| Applications | Treat all applications as internet-connected; routine testing | Internet-accessible app testing, WAF deployment |
| Data | Categorize data, deploy protections, enable secure sharing | Data classification, DLP, automated labeling |

### Implementation Timeline

```
FY22: Strategy publication, agency planning
FY23: Begin MFA rollout, encrypt DNS, initial data categorization
FY24: Complete phishing-resistant MFA, device compliance, network encryption
FY25: Application testing program, data protection automation
FY26+: Continuous maturity improvement, zero trust as default posture
```

### CISA Zero Trust Maturity Model

| Maturity | Description |
|----------|-------------|
| Traditional | Perimeter-based, static policies, manual processes |
| Initial | Some automation, visibility into assets, MFA adoption begins |
| Advanced | Centralized identity, automated policy enforcement, continuous monitoring |
| Optimal | Dynamic policies, real-time risk-based access, full automation |

## Cross-References

- See `reference/industries/financial-services-security.md` for overlapping financial regulations
- See `reference/industries/critical-infrastructure-security.md` for CI protection requirements
- See `frameworks/nist-800-53-controls.md` for control framework details
- See `frameworks/nist-csf.md` for cybersecurity framework alignment
- See `lib/patterns/authentication-patterns.md` for phishing-resistant MFA implementation
