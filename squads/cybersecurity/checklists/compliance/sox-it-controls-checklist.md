# SOX IT General Controls Checklist

## Purpose / When to Use

Execute this checklist when assessing, implementing, or auditing IT General Controls (ITGCs) for Sarbanes-Oxley (SOX) Section 404 compliance. ITGCs provide the foundation ensuring that application controls over financial reporting operate effectively. Weak ITGCs can result in material weakness findings, restatements, and auditor qualifications. This checklist covers the five ITGC domains: access management, change management, IT operations, program development, and segregation of duties.

## Prerequisites

- [ ] SOX scoping completed: financially significant applications and supporting IT infrastructure identified
- [ ] Control framework selected (COSO 2013 + COBIT mapping is standard for SOX IT)
- [ ] External auditor's ITGC testing expectations documented
- [ ] Prior year audit findings and remediation status available
- [ ] Control owners identified for each ITGC domain
- [ ] Risk and Control Matrix (RACM) drafted or available from prior year

---

## Phase 1 -- Access Management Controls

### Logical Access to Applications
- [ ] User access provisioning follows formal approval workflow:
  - [ ] Access requests documented with business justification
  - [ ] Approval by data owner or manager (not self-approved)
  - [ ] Approval evidence retained (email, ticketing system, workflow tool)
- [ ] Access is granted based on role and least privilege principle
- [ ] User access reviews performed periodically:
  - [ ] Quarterly for privileged/admin accounts
  - [ ] Semi-annually for standard user accounts
  - [ ] Review evidence: reviewer name, date, action taken (confirm/revoke)
  - [ ] Revocations completed within defined SLA (5 business days)
- [ ] Terminated user access revoked timely:
  - [ ] Integration with HR termination process
  - [ ] Access disabled within 1 business day of termination
  - [ ] Verification that access is disabled across all in-scope systems
  ```
  Control test: Sample terminated employees, verify access disabled on termination date
  Evidence: HR termination notice timestamp vs. account disable timestamp
  ```
- [ ] Transfer access reviews: users changing roles have prior access reviewed and adjusted

### Privileged Access
- [ ] Privileged accounts (admin, DBA, root) are restricted and individually assigned
- [ ] Privileged access requires separate approval from standard access
- [ ] Privileged account usage is logged and monitored
- [ ] Service accounts are inventoried, password-managed, and reviewed periodically
- [ ] Emergency/break-glass access: procedures exist, usage is logged and reviewed after each use
- [ ] Default vendor accounts are disabled or passwords changed from defaults

### Authentication Controls
- [ ] Password policy enforced on all in-scope systems:
  - Minimum length: 8+ characters (12+ recommended)
  - Complexity requirements enabled
  - Expiration: 90 days maximum
  - History: prevent reuse of last 12 passwords
  - Lockout: after 5 failed attempts
- [ ] Multi-factor authentication for remote access and privileged accounts
- [ ] Shared account usage prohibited or compensating controls documented

## Phase 2 -- Change Management Controls

### Change Request and Approval
- [ ] All changes to in-scope systems follow formal change management process:
  - [ ] Change request submitted with description, justification, risk assessment
  - [ ] Change categorized (standard, normal, emergency)
  - [ ] Change approved by appropriate authority before implementation:
    - Application changes: business owner + IT management
    - Infrastructure changes: IT management + CAB (Change Advisory Board)
  - [ ] Approval evidence retained in change management system
- [ ] Emergency changes follow expedited process with retroactive approval within defined period
- [ ] Change documentation includes rollback plan

### Development and Testing
- [ ] Changes are developed and tested in non-production environments
- [ ] Test evidence documented: test cases, expected results, actual results, tester sign-off
- [ ] User Acceptance Testing (UAT) completed and approved by business owner for significant changes
- [ ] No direct development or code changes in production environment:
  ```
  Control: Developers do not have write access to production
  Evidence: Access listings showing developer accounts lack production modify privileges
  ```

### Migration to Production
- [ ] Separation of duties: developer who wrote code is not the person who migrates to production
- [ ] Production migration performed by authorized personnel only (operations team or automated pipeline)
- [ ] Post-implementation validation performed to confirm change is functioning as intended
- [ ] Configuration changes tracked with before/after documentation

### Version Control and Audit Trail
- [ ] Source code maintained in version control system (Git or equivalent)
- [ ] All changes traceable from request to approval to implementation to testing
- [ ] Change log maintained and available for audit (ticket system with status history)

## Phase 3 -- IT Operations Controls

### Job Scheduling and Batch Processing
- [ ] Automated batch jobs (financial calculations, data transfers, reports) are scheduled and monitored:
  - [ ] Job schedules documented and maintained
  - [ ] Job failures generate alerts and are investigated promptly
  - [ ] Failed job remediation is documented
  - [ ] Successful completion verified before downstream processes execute
- [ ] Manual interventions in batch processing are logged and authorized

### Backup and Recovery
- [ ] Backup procedures defined for all in-scope systems:
  - [ ] Backup frequency appropriate to data criticality (daily for financial data)
  - [ ] Backup completeness verified (monitoring for backup job success/failure)
  - [ ] Backup media stored in secure, environmentally controlled location
  - [ ] Offsite backup copies maintained for disaster recovery
- [ ] Restoration testing performed periodically:
  - [ ] At least annually for each in-scope system
  - [ ] Test results documented with restoration time and data integrity verification
- [ ] Retention periods comply with regulatory requirements (7+ years for SOX)

### Incident and Problem Management
- [ ] IT incident management process includes:
  - [ ] Incident logging and categorization
  - [ ] Impact assessment (especially for financial system incidents)
  - [ ] Escalation procedures for incidents affecting financial reporting
  - [ ] Root cause analysis for significant incidents
  - [ ] Incident closure with resolution documentation
- [ ] Incidents affecting data integrity are reported to finance/accounting team

### System Monitoring
- [ ] System availability monitored for in-scope applications
- [ ] Performance thresholds defined and alerting configured
- [ ] Security monitoring (SIEM) covers in-scope infrastructure
- [ ] Capacity planning performed to prevent resource exhaustion

## Phase 4 -- Program Development Controls

### System Development Lifecycle (SDLC)
- [ ] SDLC methodology documented and followed for new system implementations:
  - Requirements gathering with business stakeholder input
  - Design review including security requirements
  - Development with coding standards
  - Testing (unit, integration, system, UAT)
  - Deployment with change management integration
  - Post-implementation review
- [ ] Security requirements included in system design (data protection, access controls, audit logging)
- [ ] Data migration procedures for new systems include validation of migrated data accuracy

### Vendor/Package Software
- [ ] Vendor software changes (patches, upgrades) follow change management process
- [ ] Vendor software configuration changes are documented and approved
- [ ] Customizations to vendor software are tracked and tested during upgrades

### Data Conversion
- [ ] Data conversion during system changes includes:
  - [ ] Conversion plan with validation steps
  - [ ] Before and after reconciliation of converted data
  - [ ] Sign-off by data owner on conversion accuracy
  - [ ] Rollback plan if conversion produces errors

## Phase 5 -- Segregation of Duties

- [ ] Incompatible duties identified and separated:
  | Function A | Function B | Conflict |
  |-----------|-----------|---------|
  | Initiate transaction | Approve transaction | Self-approval |
  | Develop code | Migrate to production | Uncontrolled changes |
  | Administer users | Access financial data | Self-provisioning |
  | Process payments | Reconcile bank | Concealed fraud |
  | Create vendors | Approve invoices | Fictitious vendors |
- [ ] SoD conflicts identified through access analysis:
  ```
  For each user: map assigned roles -> map roles to functions -> identify conflicts
  Tool: GRC platform (SAP GRC, SailPoint, Saviynt) or manual matrix
  ```
- [ ] Identified SoD conflicts resolved through:
  - Access modification (preferred): remove conflicting access
  - Compensating controls (if access cannot be separated):
    - Management review of transactions
    - Detailed audit logging with periodic review
    - Dual approval requirements
- [ ] SoD reviews performed at least annually
- [ ] Compensating controls documented and tested for operating effectiveness

## Phase 6 -- Testing and Evidence

- [ ] For each control, define:
  - Control objective (what risk does it mitigate?)
  - Control activity (what is performed?)
  - Control frequency (daily, weekly, monthly, quarterly, annually, per-occurrence)
  - Control owner (who is responsible?)
  - Evidence of performance (what demonstrates the control operated?)
- [ ] Testing approach per control type:
  - **Per-occurrence controls**: sample from population (sample size per AICPA guidance)
  - **Periodic controls**: test each occurrence (e.g., quarterly access reviews = test all 4)
  - **Automated controls**: test once + validate IT-dependent controls (change management, access)
- [ ] Evidence types to collect:
  - Screenshots with timestamps
  - System-generated reports (not manually created)
  - Approval emails or workflow records
  - Meeting minutes and sign-off sheets
  - Configuration exports
- [ ] Deficiency classification:
  - **Control deficiency**: control exists but did not operate effectively in isolated instances
  - **Significant deficiency**: deficiency is important enough to merit attention by those responsible for oversight
  - **Material weakness**: reasonable possibility that a material misstatement will not be prevented or detected
- [ ] Remediation plans documented for all deficiencies with target dates and responsible owners
- [ ] Remediation validated through re-testing before year-end

---

## Cross-References

- Access management: `checklists/cloud/cloud-iam-least-privilege.md`
- Change management: `checklists/appsec/appsec-ci-cd-security.md`
- Logging and monitoring: `checklists/blue-team/blueteam-logging-coverage.md`
- Hardening baselines: `checklists/santos/santos-hardening-baselines.md`
- ISO 27001 alignment: `checklists/compliance/iso27001-audit-checklist.md`
- COSO 2013 Framework: https://www.coso.org/
- PCAOB AS 2201: Audit of Internal Control Over Financial Reporting
