# PCI DSS v4.0 Compliance Audit Checklist

## Purpose / When to Use

Execute this checklist when preparing for, conducting, or validating PCI DSS v4.0 compliance. This covers the 12 requirements across scope definition, network segmentation, cardholder data protection, access controls, monitoring, and testing. Use for self-assessment questionnaires (SAQ), internal audits, and QSA-led assessments.

## Prerequisites

- [ ] PCI DSS v4.0 standard document available (published March 2022, mandatory March 31, 2025)
- [ ] Qualified Security Assessor (QSA) or Internal Security Assessor (ISA) identified
- [ ] Previous Report on Compliance (ROC) or SAQ available for delta assessment
- [ ] Network diagrams and data flow diagrams current
- [ ] Asset inventory of all systems storing, processing, or transmitting cardholder data (CHD)
- [ ] Understanding of applicable SAQ type or ROC requirement based on merchant/service provider level

---

## Phase 1 -- Scope Definition

- [ ] Identify all cardholder data (CHD) and sensitive authentication data (SAD) flows:
  - Card number (PAN), cardholder name, expiration date, service code
  - Full track data, CVV2/CVC2, PIN/PIN block
- [ ] Map the Cardholder Data Environment (CDE): all systems that store, process, or transmit CHD
- [ ] Identify connected-to systems: systems with network connectivity to the CDE
- [ ] Identify security-impacting systems: systems that could affect CDE security (DNS, AD, SIEM, NTP)
- [ ] Document and validate network segmentation that reduces scope:
  ```
  Segmentation validation: Can non-CDE systems reach CDE systems?
  Test: Attempt connections from out-of-scope to in-scope segments on all ports
  Tool: nmap -sS -p- -Pn <CDE_subnet> from out-of-scope host
  ```
- [ ] Verify P2PE (Point-to-Point Encryption) or tokenization is properly scoping out systems
- [ ] Confirm cloud shared responsibility boundaries are documented (IaaS, PaaS, SaaS delineation)
- [ ] Scope diagram reviewed and signed off by QSA/ISA

## Phase 2 -- Requirement 1-2: Network Security Controls

- [ ] **Req 1**: Network security controls (firewalls, NSGs) installed and maintained
  - [ ] Firewall rules reviewed every 6 months; unused rules removed
  - [ ] Default deny rule on all inbound and outbound CDE traffic
  - [ ] DMZ implemented between public-facing systems and CDE
  - [ ] Personal firewall/endpoint protection on mobile devices accessing CDE
  - [ ] Network security control configurations backed up and change-controlled
- [ ] **Req 2**: Secure configurations applied to all system components
  - [ ] Vendor defaults changed (passwords, SNMP community strings, certificates)
  - [ ] Unnecessary services, protocols, and ports disabled
  - [ ] System hardening standards applied (CIS Benchmarks or equivalent)
  - [ ] Wireless environments: WPA3 or WPA2 with AES; WEP prohibited
  - [ ] Configuration standards documented for all system types in CDE
  - [ ] Primary function per server enforced (no web server + database on same host)

## Phase 3 -- Requirement 3-4: Protect Cardholder Data

- [ ] **Req 3**: Protect stored account data
  - [ ] Data retention policy defined; CHD not stored beyond business need
  - [ ] PAN rendered unreadable wherever stored (truncation, tokenization, hashing, encryption)
  - [ ] SAD never stored after authorization (full track, CVV2, PIN)
  - [ ] Encryption key management procedures implemented per Req 3.6/3.7
  - [ ] Disk-level encryption not sole protection mechanism (must also have logical access controls)
  - [ ] PAN discovery scan conducted to find unprotected CHD:
    ```bash
    # Example: search for PAN patterns in file systems
    grep -rn "[0-9]\{13,19\}" /path/to/data --include="*.csv" --include="*.log" --include="*.txt" | grep -v "masked"
    ```
- [ ] **Req 4**: Protect cardholder data in transit over open/public networks
  - [ ] Strong cryptography (TLS 1.2+) for all CHD transmission
  - [ ] PAN never sent via unencrypted messaging (email, SMS, chat)
  - [ ] Wireless networks transmitting CHD use strong encryption
  - [ ] Certificate validation enforced (no self-signed certificates in production)
  - [ ] Refer to `checklists/crypto/tls-ssl-audit-checklist.md` for TLS configuration details

## Phase 4 -- Requirement 5-6: Vulnerability Management

- [ ] **Req 5**: Protect all systems against malware
  - [ ] Anti-malware deployed on all systems commonly affected by malware
  - [ ] Anti-malware kept current with automatic updates
  - [ ] Anti-malware generates audit logs and logs are retained
  - [ ] Anti-malware cannot be disabled by users (or disabling generates alert)
  - [ ] Phishing defense mechanisms in place (v4.0 new: Req 5.4.1)
- [ ] **Req 6**: Develop and maintain secure systems and software
  - [ ] Security patches applied within defined timeframes:
    - Critical: within 1 month of release
    - High/Medium: risk-ranked and scheduled
  - [ ] Custom software developed per secure coding guidelines (OWASP Top 10)
  - [ ] Code review or application security testing before production release
  - [ ] Web applications protected by WAF or automated technical solution (Req 6.4.2)
  - [ ] Public-facing web application vulnerability assessment or automated scanning
  - [ ] Change management process followed for all CDE system changes
  - [ ] Payment page script management: inventory, integrity monitoring (v4.0 Req 6.4.3)

## Phase 5 -- Requirement 7-9: Access Control Measures

- [ ] **Req 7**: Restrict access to cardholder data by business need-to-know
  - [ ] Access control system in place (RBAC or equivalent)
  - [ ] Access rights granted based on job function and least privilege
  - [ ] Access reviews conducted at least every 6 months
  - [ ] Default deny on all access to CDE resources
- [ ] **Req 8**: Identify users and authenticate access
  - [ ] Unique ID assigned to each person with access
  - [ ] MFA required for all access into the CDE (v4.0: all access, not just remote)
  - [ ] MFA required for all remote network access
  - [ ] Password policy: minimum 12 characters (v4.0 increase from 7), complexity required
  - [ ] Account lockout after 10 failed attempts; lockout duration at least 30 minutes
  - [ ] Idle session timeout at 15 minutes
  - [ ] Shared/generic accounts prohibited (or if unavoidable, individually trackable)
  - [ ] Service account passwords/keys are managed per policy
- [ ] **Req 9**: Restrict physical access to cardholder data
  - [ ] Physical access controls to CDE facilities (badges, locks, cameras)
  - [ ] Visitor identification and escorting procedures
  - [ ] Media containing CHD is physically secured, inventoried, and destroyed when no longer needed
  - [ ] POI (Point of Interaction) device inspection program for tampering detection

## Phase 6 -- Requirement 10-11: Monitoring and Testing

- [ ] **Req 10**: Log and monitor all access to system components and cardholder data
  - [ ] Audit logging enabled on all CDE systems
  - [ ] Logs capture: user ID, event type, date/time, success/failure, affected data/resource
  - [ ] Logs protected from tampering (write-once storage, FIM on log files)
  - [ ] Logs reviewed daily (automated alerting acceptable)
  - [ ] Log retention: online availability for 3 months, total retention for 12 months
  - [ ] Time synchronization across all CDE systems (NTP, < 1 second drift)
  - [ ] Automated detection mechanisms for security events (Req 10.7 -- v4.0 new)
- [ ] **Req 11**: Test security of systems and networks regularly
  - [ ] Wireless access point detection quarterly (rogue AP scanning)
  - [ ] Internal vulnerability scanning quarterly (and after significant changes)
  - [ ] External vulnerability scanning quarterly by ASV (Approved Scanning Vendor)
  - [ ] Internal penetration testing annually (and after significant changes)
  - [ ] External penetration testing annually (and after significant changes)
  - [ ] Segmentation testing: every 6 months for service providers, annually for merchants
  - [ ] File integrity monitoring (FIM) on critical files:
    ```
    Monitor: system files, configuration files, content files
    Alert: on unauthorized modification
    Comparison: at least weekly (daily preferred)
    ```
  - [ ] IDS/IPS deployed at CDE perimeter and critical points
  - [ ] Change detection mechanism on payment pages (v4.0 Req 11.6.1)

## Phase 7 -- Requirement 12: Organizational Policies

- [ ] **Req 12**: Support information security with organizational policies and programs
  - [ ] Information security policy reviewed annually and communicated to all personnel
  - [ ] Risk assessment performed annually and upon significant changes
  - [ ] Security awareness training for all personnel annually
  - [ ] Incident response plan documented, tested annually, and includes notification procedures
  - [ ] Service provider management: written agreements, monitoring of compliance status
  - [ ] Targeted risk analysis for flexible requirements (v4.0 customized approach)
  - [ ] PCI DSS scope confirmed at least annually (every 6 months for service providers)

## Phase 8 -- Evidence Collection and Documentation

- [ ] Compile evidence for each requirement:
  - Configuration screenshots/exports
  - Policy and procedure documents
  - Scan reports (ASV, internal vulnerability, penetration test)
  - Interview notes with key personnel
  - Observation records (physical security walkthrough)
  - Log samples demonstrating monitoring effectiveness
- [ ] Complete applicable SAQ or prepare ROC documentation
- [ ] Submit ASV scan attestation with passing results
- [ ] File Attestation of Compliance (AOC) with acquiring bank or card brand
- [ ] Schedule quarterly ASV scans and annual reassessment

---

## Cross-References

- TLS/SSL audit: `checklists/crypto/tls-ssl-audit-checklist.md`
- Key management: `checklists/crypto/key-management-checklist.md`
- Penetration testing: `checklists/pentest-execution-quality.md`
- Secure coding: `checklists/manico/manico-secure-coding-review.md`
- Logging coverage: `checklists/blue-team/blueteam-logging-coverage.md`
- PCI DSS v4.0: https://www.pcisecuritystandards.org/document_library/
