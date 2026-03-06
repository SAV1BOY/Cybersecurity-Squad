# Executive Order 14028: Improving the Nation's Cybersecurity (2021)

## Overview

| Field | Details |
|-------|---------|
| Title | Executive Order on Improving the Nation's Cybersecurity |
| Number | EO 14028 |
| Signed | May 12, 2021 |
| President | Joseph R. Biden Jr. |
| Context | Issued following SolarWinds (Dec 2020), Microsoft Exchange (Jan 2021), and Colonial Pipeline (May 2021) attacks |
| Scope | Federal government agencies; significant implications for federal contractors and the broader software industry |

---

## Key Provisions

### Section 2: Removing Barriers to Sharing Threat Information
- Requires IT service providers to share cyber threat and incident information with the government
- Removes contractual barriers that prevent sharing
- Establishes timelines for incident notification to CISA and FBI
- Applies to any service provider contracted by federal agencies

**Impact on organizations:**
- Federal contractors must update contracts to include threat information sharing
- Incident notification requirements become contractual obligations
- Coordination with CISA becomes mandatory, not optional

### Section 3: Modernizing Federal Government Cybersecurity
Key mandates for federal agencies:
- [ ] **Zero Trust Architecture**: Agencies must develop plans to adopt zero trust within 60 days and implement within defined timelines
- [ ] **Cloud Migration**: Accelerate migration to secure cloud services
- [ ] **MFA**: Deploy multi-factor authentication within 180 days for all systems
- [ ] **Encryption**: Encrypt data at rest and in transit
- [ ] **EDR**: Adopt endpoint detection and response capabilities
- [ ] **Centralized Logging**: Implement centralized log management with defined retention

**Industry implications:**
- Zero trust products and services see accelerated demand
- Cloud security becomes a procurement requirement
- MFA becomes non-negotiable for any federal-facing system

### Section 4: Enhancing Software Supply Chain Security

**The most transformative section of the EO:**

**SBOM (Software Bill of Materials) Requirement:**
- Software vendors selling to the federal government must provide an SBOM
- SBOM must list all components, libraries, and dependencies
- Must use standard formats (SPDX, CycloneDX)
- Enables rapid vulnerability assessment when new CVEs are disclosed

**Secure Software Development Practices:**
- NIST directed to publish secure software development guidance (resulted in NIST SSDF, SP 800-218)
- Vendors must attest to secure development practices
- Requirements include:
  - [ ] Maintaining separate build environments
  - [ ] Employing automated tools for source code analysis
  - [ ] Auditing and enforcing trust relationships in the development chain
  - [ ] Maintaining provenance data for code and components
  - [ ] Using build processes that detect tampering
  - [ ] Performing regular vulnerability scanning and remediation

**Software Testing Requirements:**
- Automated testing including SAST, DAST, SCA
- Fuzz testing for software accepting structured input
- Regular security testing throughout the development lifecycle
- Remediation of discovered vulnerabilities before release

### Section 5: Establishing a Cyber Safety Review Board (CSRB)
- Created a board modeled after the National Transportation Safety Board (NTSB)
- Reviews significant cyber incidents affecting federal systems
- Produces reports with lessons learned and recommendations
- First review: Log4Shell vulnerability and response
- Subsequent review: Lapsus$ threat group activities

### Section 6: Standardizing the Federal Government's Playbook for Responding to Cybersecurity Vulnerabilities and Incidents
- CISA directed to develop standard incident response playbook
- Resulted in CISA Federal Incident Response Playbook
- Defines standard procedures for identification, containment, eradication, recovery
- Establishes common terminology and reporting requirements

### Section 7: Improving Detection of Cybersecurity Vulnerabilities and Incidents on Federal Government Networks
- Government-wide endpoint detection and response (EDR) deployment
- Centralized visibility into cybersecurity events across agencies
- CISA given authority to conduct threat hunting across federal networks
- Information sharing between agencies improved

### Section 8: Improving the Federal Government's Investigative and Remediation Capabilities
- **Log retention requirements**: Network and system logs must be retained for specified periods
- Defined minimum logging requirements including:
  - [ ] DNS query logs
  - [ ] Proxy and firewall logs
  - [ ] Authentication logs (success and failure)
  - [ ] Endpoint process and command logs
  - [ ] Cloud API activity logs
- Logs must be collected centrally and accessible to CISA for threat hunting

## Impact Beyond Federal Government

### Software Industry
The EO effectively set new baseline expectations for the entire software industry:
- **SBOM becomes industry norm**: Even non-federal customers now expect SBOMs
- **Secure development attestation**: Self-attestation requirement creates documentation burden
- **Third-party testing**: Expectation for independent security testing
- **Vulnerability disclosure**: Formal vulnerability disclosure programs expected

### Supply Chain Security
- Organizations across sectors adopt supply chain risk management practices
- SBOM tooling and processes become standard in CI/CD pipelines
- Open source dependency tracking becomes critical capability
- Software composition analysis (SCA) tools see widespread adoption

### Cloud Security
- FedRAMP modernization accelerated
- Cloud-first security architectures become the standard
- CSPM (Cloud Security Posture Management) becomes essential
- Zero trust cloud architectures drive market demand

## Implementation Timeline

| Deadline | Requirement |
|----------|-------------|
| 30 days | Remove contractual barriers to threat information sharing |
| 60 days | Agencies develop zero trust implementation plans |
| 90 days | NIST publish preliminary SBOM guidelines |
| 120 days | NIST publish secure software development guidelines |
| 180 days | Agencies deploy MFA and encryption |
| 180 days | Agencies adopt EDR capabilities |
| 360 days | Agencies implement zero trust architecture per plans |

## Practical Checklist for Security Teams

### If You Sell Software to the Federal Government
- [ ] Generate SBOM for all products (SPDX or CycloneDX format)
- [ ] Document secure development practices per NIST SSDF
- [ ] Implement SAST, DAST, SCA in CI/CD pipeline
- [ ] Prepare self-attestation of compliance with EO requirements
- [ ] Establish vulnerability disclosure program
- [ ] Maintain build provenance and integrity

### If You Are a Federal Contractor
- [ ] Review and update contracts for information sharing requirements
- [ ] Implement incident notification procedures to CISA
- [ ] Deploy MFA on all systems accessible to federal data
- [ ] Implement encryption for federal data at rest and in transit
- [ ] Establish logging per NIST/CISA requirements

### For All Organizations (Best Practice Adoption)
- [ ] Adopt zero trust principles (see `workflows/zero-trust-implementation.md`)
- [ ] Implement SBOM generation in software development
- [ ] Deploy EDR across all endpoints
- [ ] Centralize security logging with adequate retention
- [ ] Conduct regular supply chain risk assessments
- [ ] Implement secure software development practices

## Cross-References

- `workflows/zero-trust-implementation.md` — Zero trust implementation
- `workflows/devsecops-pipeline-setup.md` — Secure development pipeline
- `frameworks/nist-ssdf.md` — Secure Software Development Framework
- `workflows/third-party-risk-assessment.md` — Supply chain risk management
- `archive/notable-breaches/kaseya-2021.md` — Supply chain attack context
- `archive/regulatory-milestones/nist-csf-2-0-2024.md` — CSF 2.0 supply chain focus
