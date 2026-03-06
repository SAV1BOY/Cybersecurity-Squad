# NIST Cybersecurity Framework 2.0 (2024)

## Overview

| Field | Details |
|-------|---------|
| Title | NIST Cybersecurity Framework (CSF) 2.0 |
| Published | February 26, 2024 |
| Publisher | National Institute of Standards and Technology (NIST) |
| Previous Version | CSF 1.1 (April 2018) |
| Applicability | All organizations regardless of size, sector, or maturity (expanded from critical infrastructure focus) |
| Status | Voluntary framework (mandatory for US federal agencies via EO 13800) |

---

## Key Changes from CSF 1.1 to 2.0

### 1. New GOVERN Function
The most significant structural change: addition of a sixth core function.

**CSF 1.1 Functions**: Identify, Protect, Detect, Respond, Recover
**CSF 2.0 Functions**: **Govern**, Identify, Protect, Detect, Respond, Recover

The GOVERN function establishes cybersecurity as an enterprise risk management concern, not just a technical issue. It encompasses:
- **GV.OC**: Organizational Context (understanding the organization's mission, stakeholders, legal requirements)
- **GV.RM**: Risk Management Strategy (risk appetite, risk tolerance, risk-informed decision making)
- **GV.RR**: Roles, Responsibilities, and Authorities (accountability structure)
- **GV.PO**: Policy (security policies aligned with strategy)
- **GV.OV**: Oversight (monitoring and adjustment of cybersecurity strategy)
- **GV.SC**: Cybersecurity Supply Chain Risk Management (elevated from subcategory to full category)

### 2. Expanded Scope
CSF 1.1 was primarily targeted at critical infrastructure. CSF 2.0 explicitly serves:
- Small and medium businesses
- Schools and educational institutions
- Non-profit organizations
- State, local, tribal, and territorial governments
- International organizations
- Large enterprises and critical infrastructure (existing audience)

### 3. Supply Chain Risk Management
Supply chain risk management (C-SCRM) elevated from a subcategory to a dedicated category within GOVERN:
- [ ] GV.SC-01: Establish supply chain risk management program
- [ ] GV.SC-02: Identify and prioritize suppliers and third parties
- [ ] GV.SC-03: Integrate supply chain risk into broader risk management
- [ ] GV.SC-04: Assess suppliers based on risk criteria
- [ ] GV.SC-05: Plan for supply chain incidents
- [ ] GV.SC-06: Include supply chain requirements in contracts
- [ ] GV.SC-07: Manage risks from technology providers throughout lifecycle

### 4. Improved Guidance and Resources
- **CSF 2.0 Profiles**: Enhanced guidance for creating organizational profiles (current state and target state)
- **Implementation Examples**: Practical examples for each subcategory
- **Quick Start Guides**: Simplified guides for small businesses and specific use cases
- **Informative References**: Online catalog mapping CSF to other frameworks and standards
- **CSF Tiers**: Refined maturity tiers (Partial, Risk Informed, Repeatable, Adaptive)

## CSF 2.0 Core Structure

### GOVERN (GV) — NEW
Establish and monitor cybersecurity risk management strategy, expectations, and policy.

| Category | Description | Security Team Responsibility |
|----------|-------------|------------------------------|
| GV.OC | Organizational Context | Document mission, stakeholders, requirements |
| GV.RM | Risk Management Strategy | Define risk appetite and tolerance |
| GV.RR | Roles and Responsibilities | Define security team RACI matrix |
| GV.PO | Policy | Maintain security policy framework |
| GV.OV | Oversight | Report to leadership, adjust strategy |
| GV.SC | Supply Chain Risk Management | Vendor security program |

### IDENTIFY (ID)
Understand organizational context to manage cybersecurity risk.

| Category | Key Activities |
|----------|---------------|
| ID.AM | Asset Management: hardware, software, data inventory |
| ID.RA | Risk Assessment: threat identification, risk analysis |
| ID.IM | Improvement: lessons learned, continuous improvement |

### PROTECT (PR)
Implement safeguards to manage cybersecurity risk.

| Category | Key Activities |
|----------|---------------|
| PR.AA | Identity Management, Authentication, Access Control |
| PR.AT | Awareness and Training |
| PR.DS | Data Security: encryption, DLP, integrity |
| PR.PS | Platform Security: configuration, vulnerability management |
| PR.IR | Technology Infrastructure Resilience |

### DETECT (DE)
Find and analyze cybersecurity events and anomalies.

| Category | Key Activities |
|----------|---------------|
| DE.CM | Continuous Monitoring: network, endpoint, cloud |
| DE.AE | Adverse Event Analysis: correlation, triage |

### RESPOND (RS)
Take action regarding detected cybersecurity incidents.

| Category | Key Activities |
|----------|---------------|
| RS.MA | Incident Management: response procedures, triage |
| RS.AN | Incident Analysis: forensics, root cause |
| RS.CO | Incident Response Reporting and Communication |
| RS.MI | Incident Mitigation: containment, eradication |

### RECOVER (RC)
Restore assets and operations affected by cybersecurity incidents.

| Category | Key Activities |
|----------|---------------|
| RC.RP | Incident Recovery Plan Execution |
| RC.CO | Recovery Communication |

## Implementation Guidance for Security Teams

### Using CSF 2.0 Profiles
1. **Current Profile**: Document current state of cybersecurity practices against CSF categories
2. **Target Profile**: Define desired state based on risk assessment and business objectives
3. **Gap Analysis**: Compare current and target profiles to identify priorities
4. **Action Plan**: Create remediation roadmap based on gap analysis
5. **Continuous Assessment**: Regularly reassess and update profiles

### CSF Tiers (Maturity Assessment)

| Tier | Name | Characteristics |
|------|------|----------------|
| Tier 1 | Partial | Ad hoc, reactive, limited risk awareness |
| Tier 2 | Risk Informed | Risk-aware practices exist but may not be org-wide |
| Tier 3 | Repeatable | Formal policies, consistent implementation, regular review |
| Tier 4 | Adaptive | Risk-informed, continuously improving, lessons learned integrated |

### Mapping to Other Frameworks
CSF 2.0 provides informative references to:
- NIST SP 800-53 (security controls)
- ISO 27001/27002 (information security management)
- CIS Controls v8
- COBIT
- Industry-specific frameworks (HIPAA, PCI DSS)

## Organizational Impact

### For CISOs and Security Leadership
- CSF 2.0's GOVERN function provides a framework for communicating security as a business risk management function
- Enables structured board reporting and strategy alignment
- Provides common language between security and business leadership
- Facilitates benchmarking against industry peers

### For Security Operations
- Updated detection and response categories provide clearer operational guidance
- Improved alignment with modern SOC operational models
- Supply chain categories drive vendor monitoring requirements

### For Compliance Teams
- Unified framework for cross-mapping multiple regulatory requirements
- Profiles enable compliance gap analysis documentation
- Tiers provide maturity assessment language for auditors

## Cross-References

- `frameworks/nist-csf.md` — Detailed NIST CSF implementation in squad
- `frameworks/nist-800-53-controls.md` — Control mapping
- `tasks/governance/compliance-gap-analysis.md` — CSF-based gap analysis
- `tasks/governance/risk-assessment-execution.md` — Risk assessment aligned to CSF
- `workflows/third-party-risk-assessment.md` — GV.SC implementation
- `workflows/security-metrics-reporting.md` — CSF-aligned metrics
