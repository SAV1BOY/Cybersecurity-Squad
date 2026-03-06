# ISO 27001 Certification Audit Checklist

## Purpose / When to Use

Execute this checklist when preparing for ISO/IEC 27001:2022 certification, conducting internal audits, or assessing the maturity of an Information Security Management System (ISMS). This covers the mandatory ISMS clauses (4-10) and the Annex A control assessment. Use for Stage 1 (documentation review), Stage 2 (implementation audit), and surveillance audits.

## Prerequisites

- [ ] ISO/IEC 27001:2022 standard text available (clauses 4-10 + Annex A)
- [ ] ISO/IEC 27002:2022 available for control implementation guidance
- [ ] Top management commitment secured (resource allocation, policy endorsement)
- [ ] ISMS project team established with defined roles
- [ ] Gap assessment completed against current security posture
- [ ] Certification body selected (if pursuing external certification)

---

## Phase 1 -- ISMS Scope Definition (Clause 4)

- [ ] Context of the organization documented (Clause 4.1):
  - Internal issues: organizational structure, culture, capabilities, strategy
  - External issues: regulatory, legal, contractual, competitive, technological
- [ ] Interested parties identified with their requirements (Clause 4.2):
  | Interested Party | Security Requirements |
  |-----------------|----------------------|
  | Customers | Data protection, service availability, incident notification |
  | Regulators | Compliance with laws (GDPR, HIPAA, etc.) |
  | Shareholders | Risk management, business continuity |
  | Employees | Privacy, acceptable use, training |
  | Suppliers | Secure data exchange, access controls |
- [ ] ISMS scope defined and documented (Clause 4.3):
  - Organizational units included
  - Locations (physical and virtual/cloud)
  - Information assets and processes
  - Boundaries and interfaces with out-of-scope areas
  - Justification for any exclusions
- [ ] ISMS processes and interactions established (Clause 4.4)

## Phase 2 -- Leadership and Planning (Clauses 5-6)

### Leadership (Clause 5)
- [ ] Top management demonstrates leadership by:
  - [ ] Establishing information security policy aligned with strategic direction
  - [ ] Ensuring ISMS integration into business processes
  - [ ] Providing necessary resources (people, budget, tools)
  - [ ] Communicating the importance of information security
  - [ ] Ensuring the ISMS achieves intended outcomes
- [ ] Information security policy (Clause 5.2):
  - [ ] Appropriate to the purpose of the organization
  - [ ] Includes commitment to satisfy requirements and continual improvement
  - [ ] Available as documented information
  - [ ] Communicated within the organization
  - [ ] Available to interested parties as appropriate
- [ ] Roles, responsibilities, and authorities assigned (Clause 5.3):
  - [ ] ISMS ownership at senior management level
  - [ ] Information Security Manager/Officer designated
  - [ ] Risk owners identified for each risk area
  - [ ] Internal audit function independent from ISMS operations

### Planning (Clause 6)
- [ ] Risk assessment process defined (Clause 6.1.2):
  - [ ] Risk assessment methodology documented:
    - Risk identification approach (asset-based, scenario-based, or threat-based)
    - Risk analysis method (qualitative, quantitative, or semi-quantitative)
    - Risk evaluation criteria and risk acceptance thresholds
  - [ ] Risk assessment performed:
    - [ ] Information assets identified and valued
    - [ ] Threats and vulnerabilities identified for each asset
    - [ ] Likelihood and impact assessed
    - [ ] Risk levels calculated and compared against acceptance criteria
  - [ ] Risk assessment results documented and approved by risk owners
- [ ] Risk treatment plan developed (Clause 6.1.3):
  - [ ] Treatment option selected for each risk: mitigate, accept, transfer, avoid
  - [ ] Controls selected from Annex A (or other sources) with justification
  - [ ] Statement of Applicability (SoA) produced:
    - All 93 Annex A controls listed (ISO 27001:2022)
    - Each control marked as applicable or not applicable with justification
    - Implementation status documented
  - [ ] Residual risk assessed and formally accepted by risk owners
- [ ] Information security objectives established (Clause 6.2):
  - [ ] Consistent with information security policy
  - [ ] Measurable (where practicable)
  - [ ] Monitored and communicated
  - [ ] Action plans to achieve objectives (what, resources, responsible, timeline, evaluation)

## Phase 3 -- Support (Clause 7)

- [ ] Resources allocated (Clause 7.1):
  - Budget for security tools, training, and third-party services
  - Personnel with appropriate skills assigned
  - Infrastructure for ISMS operation
- [ ] Competence ensured (Clause 7.2):
  - [ ] Competence requirements defined for ISMS roles
  - [ ] Training needs identified and training provided
  - [ ] Training effectiveness evaluated
  - [ ] Competence records retained (certifications, training completions)
- [ ] Awareness program in place (Clause 7.3):
  - [ ] All employees aware of information security policy
  - [ ] Employees understand their contribution to ISMS effectiveness
  - [ ] Consequences of non-conformity communicated
- [ ] Communication plan defined (Clause 7.4):
  - What to communicate (security policies, incidents, risks)
  - When to communicate (onboarding, changes, incidents)
  - With whom to communicate (all staff, management, external parties)
  - How to communicate (intranet, email, training sessions, reports)
- [ ] Documented information controlled (Clause 7.5):
  - [ ] Document management system in place (creation, review, approval, distribution)
  - [ ] Version control and change tracking active
  - [ ] Retention and disposal procedures defined
  - [ ] Access to documentation appropriately controlled

## Phase 4 -- Operation (Clause 8)

- [ ] Operational planning and control implemented (Clause 8.1):
  - [ ] Processes needed to meet ISMS requirements are planned and controlled
  - [ ] Outsourced processes are identified and controlled
  - [ ] Changes are managed (planned, reviewed, assessed for impact)
- [ ] Risk assessment executed at planned intervals and when significant changes occur (Clause 8.2)
- [ ] Risk treatment plan implemented (Clause 8.3):
  - [ ] Selected controls from SoA are implemented
  - [ ] Control implementation evidence documented
  - [ ] Residual risk documented and accepted

## Phase 5 -- Statement of Applicability and Control Implementation

### Annex A Controls (ISO 27001:2022 -- 93 controls in 4 themes)

#### Organizational Controls (A.5)
- [ ] A.5.1 Policies for information security: comprehensive policy set approved and communicated
- [ ] A.5.2 Information security roles and responsibilities: documented and assigned
- [ ] A.5.3 Segregation of duties: conflicting duties separated
- [ ] A.5.7 Threat intelligence: threat information collected and analyzed
- [ ] A.5.8 Information security in project management: security integrated into projects
- [ ] A.5.23 Information security for use of cloud services: cloud security assessed
- [ ] A.5.24 Information security incident management planning: IR plan documented and tested
- [ ] A.5.30 ICT readiness for business continuity: IT DR plan tested

#### People Controls (A.6)
- [ ] A.6.1 Screening: background checks proportionate to role
- [ ] A.6.2 Terms and conditions of employment: security responsibilities in contracts
- [ ] A.6.3 Information security awareness, education, and training: program implemented
- [ ] A.6.5 Responsibilities after termination: post-employment obligations defined

#### Physical Controls (A.7)
- [ ] A.7.1 Physical security perimeters: secured boundaries for sensitive areas
- [ ] A.7.4 Physical security monitoring: surveillance and detection systems
- [ ] A.7.10 Storage media: lifecycle management including secure disposal

#### Technological Controls (A.8)
- [ ] A.8.1 User endpoint devices: security policies and configurations
- [ ] A.8.2 Privileged access rights: restricted and monitored
- [ ] A.8.3 Information access restriction: need-to-know basis
- [ ] A.8.5 Secure authentication: MFA, password policies
- [ ] A.8.7 Protection against malware: anti-malware controls
- [ ] A.8.8 Management of technical vulnerabilities: vulnerability management program
- [ ] A.8.9 Configuration management: secure baselines, change control
- [ ] A.8.12 Data leakage prevention: DLP controls where appropriate
- [ ] A.8.15 Logging: centralized logging and monitoring
- [ ] A.8.16 Monitoring activities: security monitoring and alerting
- [ ] A.8.24 Use of cryptography: crypto policy and implementation
- [ ] A.8.25 Secure development lifecycle: SDLC with security activities
- [ ] A.8.28 Secure coding: coding standards and practices

*Note: Full SoA must address all 93 controls with applicability determination.*

## Phase 6 -- Performance Evaluation (Clause 9)

- [ ] Monitoring, measurement, analysis, and evaluation (Clause 9.1):
  - [ ] Security metrics defined and collected:
    - Incident count and severity trends
    - Vulnerability remediation times
    - Policy compliance rates
    - Training completion rates
    - Risk treatment plan progress
  - [ ] Metrics reviewed at defined intervals and reported to management
- [ ] Internal audit program (Clause 9.2):
  - [ ] Audit program planned covering all ISMS requirements over audit cycle
  - [ ] Audit criteria, scope, and methods defined for each audit
  - [ ] Auditor independence ensured (auditors do not audit their own work)
  - [ ] Audit findings documented with nonconformities classified (major/minor)
  - [ ] Corrective actions tracked to closure
  - [ ] Audit results reported to management
- [ ] Management review (Clause 9.3):
  - [ ] Conducted at planned intervals (at least annually)
  - [ ] Inputs include: audit results, interested party feedback, risk assessment status, incident trends, metrics, improvement opportunities, changes affecting ISMS
  - [ ] Outputs include: decisions on continual improvement, resource allocation, ISMS changes
  - [ ] Minutes documented and retained

## Phase 7 -- Improvement (Clause 10)

- [ ] Nonconformities addressed (Clause 10.1):
  - [ ] Nonconformities identified from audits, incidents, monitoring, or complaints
  - [ ] Corrective actions implemented:
    - Immediate correction to contain the nonconformity
    - Root cause analysis performed
    - Corrective action to prevent recurrence
    - Effectiveness of corrective action verified
  - [ ] Corrective action records retained
- [ ] Continual improvement (Clause 10.2):
  - [ ] Improvement opportunities identified and evaluated
  - [ ] ISMS suitability, adequacy, and effectiveness continuously improved
  - [ ] Improvements documented and communicated

## Phase 8 -- Certification Audit Preparation

- [ ] **Stage 1 preparation** (documentation review):
  - [ ] ISMS scope document
  - [ ] Information security policy
  - [ ] Risk assessment methodology and results
  - [ ] Risk treatment plan and Statement of Applicability
  - [ ] Internal audit reports
  - [ ] Management review minutes
  - [ ] Evidence of corrective actions
- [ ] **Stage 2 preparation** (implementation audit):
  - [ ] Control implementation evidence for all applicable Annex A controls
  - [ ] Staff available for auditor interviews
  - [ ] Technical evidence accessible (configurations, logs, scan results)
  - [ ] Process demonstrations planned (incident response, change management, access provisioning)
- [ ] Address all Stage 1 findings before Stage 2
- [ ] Schedule surveillance audits (annual) and recertification (every 3 years)

---

## Cross-References

- Risk assessment: `checklists/threat-model-quality.md`
- Incident response: `checklists/incident-response/initial-triage-checklist.md`
- Access controls: `checklists/cloud/cloud-iam-least-privilege.md`
- Cryptography: `checklists/crypto/cryptographic-implementation-checklist.md`
- Logging: `checklists/blue-team/blueteam-logging-coverage.md`
- Hardening: `checklists/santos/santos-hardening-baselines.md`
- PCI DSS mapping: `checklists/compliance/pci-dss-audit-checklist.md`
- ISO/IEC 27001:2022: https://www.iso.org/standard/27001
- ISO/IEC 27002:2022: https://www.iso.org/standard/75652.html
