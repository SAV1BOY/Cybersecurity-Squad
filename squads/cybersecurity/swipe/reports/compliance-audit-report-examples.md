# Compliance Audit Report Examples

## Purpose

Model compliance audit reports demonstrating proper scope definition, methodology documentation, evidence-based findings, and actionable recommendations. Applicable to SOC 2, ISO 27001, PCI DSS, HIPAA, and general regulatory audits.

## Report Structure

### 1. Cover Page and Document Control

```markdown
# [Framework] Compliance Audit Report

**Organization:** [Client Name]
**Report Date:** [Date]
**Audit Period:** [Start Date] to [End Date]
**Report Classification:** Confidential
**Prepared By:** [Auditor Name], [Certification]
**Reviewed By:** [Senior Auditor Name]
**Report Version:** 1.0
**Distribution:** [Named recipients]

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 0.1 | [Date] | [Name] | Initial draft |
| 0.9 | [Date] | [Name] | Review incorporation |
| 1.0 | [Date] | [Name] | Final release |
```

### 2. Executive Summary

```markdown
## Executive Summary

### Audit Objective
Assess [Organization]'s compliance with [Framework/Standard] requirements
for the [system/environment/scope] environment covering the period
[start date] through [end date].

### Overall Assessment

| Rating | Definition |
|--------|-----------|
| **Satisfactory** | Controls operating effectively with minor observations |

### Summary of Results

| Category | Compliant | Partially Compliant | Non-Compliant | Not Applicable |
|----------|-----------|--------------------:|---------------|----------------|
| Access Control | 12 | 2 | 1 | 0 |
| Change Management | 8 | 1 | 0 | 1 |
| Incident Response | 6 | 2 | 0 | 0 |
| Data Protection | 10 | 0 | 1 | 2 |
| Physical Security | 5 | 0 | 0 | 3 |
| **Total** | **41** | **5** | **2** | **6** |

### Key Findings
1. **Non-Compliant:** Privileged access reviews not performed quarterly as required (AC-7)
2. **Non-Compliant:** Encryption at rest not implemented for all PII data stores (DP-3)
3. **Partially Compliant:** Incident response plan not tested within last 12 months (IR-4)

### Positive Observations
- Strong MFA implementation across all remote access
- Comprehensive logging and monitoring program
- Well-documented change management procedures
```

### 3. Scope and Methodology

```markdown
## Scope

### Audit Scope
**Framework:** [ISO 27001:2022 / SOC 2 Type II / PCI DSS v4.0 / HIPAA]
**Scope Boundaries:**
- Systems: [List of in-scope systems]
- Locations: [Physical locations assessed]
- Processes: [Business processes covered]
- Third parties: [Relevant service providers]

### Exclusions
| Excluded Item | Reason | Risk Acceptance |
|--------------|--------|----------------|
| [System X] | Decommissioned prior to audit period | N/A |
| [Location Y] | Not processing in-scope data | Documented |

## Methodology

### Audit Approach
1. **Documentation review** -- Policy, procedure, and standard review
2. **Interview** -- Key personnel interviews (see Appendix A)
3. **Observation** -- Direct observation of control operation
4. **Testing** -- Sample-based testing of control effectiveness
5. **Technical validation** -- Configuration review, vulnerability assessment

### Sampling Methodology
| Population Size | Sample Size | Method |
|----------------|-------------|--------|
| 1-10 | All | Census |
| 11-50 | 10 | Random |
| 51-200 | 25 | Stratified random |
| 201-500 | 30 | Stratified random |
| 500+ | 40 | Stratified random |

### Evidence Types Accepted
| Evidence Type | Examples | Weight |
|--------------|---------|--------|
| System-generated | Logs, reports, screenshots | High |
| Documentation | Policies, procedures, diagrams | Medium |
| Interview | Verbal confirmation from personnel | Low (requires corroboration) |
| Observation | Direct auditor observation | High |
```

### 4. Detailed Findings

```markdown
## Finding: AC-7 -- Privileged Access Review

**Control Requirement:** Privileged access shall be reviewed quarterly to
ensure appropriateness and least privilege compliance.

**Compliance Status:** Non-Compliant

**Risk Rating:** High

### Condition (What we found)
Privileged access reviews for domain administrator accounts were not performed
during Q2 and Q3 of the audit period. The last completed review was Q1
(March 2025). At the time of audit, 47 domain admin accounts were active,
including 8 accounts belonging to terminated employees.

### Criteria (What was expected)
Per [Organization] Access Control Policy (AC-POL-001 v3.2, Section 4.3):
"All privileged access shall be reviewed by the account owner's manager and
the Information Security team on a quarterly basis."

[Framework] Requirement [X.Y.Z] requires periodic review of privileged access
at intervals not exceeding 90 days.

### Cause (Why it happened)
- Access review process was manual and dependent on a single team member
  who was on extended leave
- No automated tooling for access review campaigns
- No escalation process for missed review deadlines

### Effect (Impact/Risk)
- 8 active domain admin accounts for terminated employees represent
  immediate unauthorized access risk
- Potential for privilege creep across remaining accounts
- Regulatory non-compliance with [Framework] requirement

### Evidence
| Evidence ID | Description | Date |
|-------------|-------------|------|
| E-AC-7-01 | Access review log showing last review March 2025 | 2025-10-15 |
| E-AC-7-02 | HR termination report showing 8 unrevoked accounts | 2025-10-15 |
| E-AC-7-03 | Interview with IAM team lead confirming gap | 2025-10-12 |

### Recommendation
1. **Immediate:** Disable 8 terminated employee admin accounts (24 hours)
2. **Short-term:** Complete overdue access review for all privileged accounts (2 weeks)
3. **Medium-term:** Implement automated access certification tool (90 days)
4. **Long-term:** Integrate HR termination workflow with automated deprovisioning (6 months)

### Management Response
[Space for management to document planned corrective action, responsible
party, and target completion date]

**Responsible Party:** [Name/Role]
**Target Date:** [Date]
**Corrective Action Plan:** [Description]
```

### 5. Framework-Specific Sections

#### SOC 2 Type II Example

```markdown
## Control Activity Testing -- SOC 2 Trust Services Criteria

### CC6.1 -- Logical Access Security

| Control | Description | Test Procedure | Result |
|---------|-------------|---------------|--------|
| CC6.1-01 | MFA required for remote access | Inspected VPN configuration, tested login | Effective |
| CC6.1-02 | Unique user IDs assigned | Reviewed user provisioning records (n=25) | Effective |
| CC6.1-03 | Access removed on termination | Compared HR terminations to access logs (n=15) | Exception (2 delays >24hr) |
| CC6.1-04 | Quarterly access reviews | Reviewed review documentation for 4 quarters | Exception (2 quarters missed) |

**Exception Detail for CC6.1-03:**
2 of 15 sampled terminations showed access removal delays of 3 and 5 business
days respectively. Root cause: manual process, no SLA enforcement.
```

#### PCI DSS v4.0 Example

```markdown
## PCI DSS v4.0 Assessment Findings

### Requirement 8: Identify Users and Authenticate Access

| Sub-Req | Description | Status | Evidence |
|---------|-------------|--------|----------|
| 8.2.1 | Unique IDs for all users | In Place | User account listing, provisioning records |
| 8.2.2 | Shared/group accounts managed | In Place | Shared account inventory with justification |
| 8.3.1 | MFA for admin access to CDE | In Place | MFA configuration, authentication logs |
| 8.3.2 | MFA for all remote access | In Place | VPN MFA configuration |
| 8.3.6 | Password complexity requirements | Not In Place | Policy requires 8 chars, 4.0 requires 12 |
| 8.6.1 | System/service account management | In Place | Service account inventory, rotation records |
```

### 6. Appendices

```markdown
## Appendix A: Personnel Interviewed

| Name | Title | Topics Discussed | Date |
|------|-------|-----------------|------|
| [Name] | CISO | Security program, governance | [Date] |
| [Name] | IT Director | Infrastructure, change management | [Date] |
| [Name] | DBA Lead | Database security, encryption | [Date] |

## Appendix B: Documents Reviewed

| Document | Version | Date | Relevance |
|----------|---------|------|-----------|
| Information Security Policy | 3.2 | 2025-01-15 | Overall governance |
| Access Control Procedure | 2.1 | 2024-09-01 | Access management |
| Incident Response Plan | 4.0 | 2025-03-01 | IR readiness |

## Appendix C: Systems Tested

| System | IP/Hostname | Function | Test Type |
|--------|-------------|----------|-----------|
| [System] | [IP] | [Function] | Config review |
```

## Cross-References

- [Security Program Maturity Examples](security-program-maturity-examples.md) -- maturity assessment
- [Governance Layer](../../frameworks/governance-layer.md) -- governance framework
- [NIST 800-53 Controls](../../frameworks/nist-800-53-controls.md) -- control mapping
- [CIS Controls v8](../../frameworks/cis-controls-v8.md) -- control baselines
