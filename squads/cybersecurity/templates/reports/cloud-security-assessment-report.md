# Cloud Security Posture Assessment Report Template

## Purpose

Template for documenting cloud security posture assessments. Covers IAM, network, data, compute, logging, and compliance across AWS, Azure, and GCP environments with prioritized remediation guidance.

---

## [TEMPLATE BEGINS]

# Cloud Security Posture Assessment Report

**Client**: [Organization Name]
**Assessment ID**: [CSA-YYYY-NNN]
**Cloud Provider(s)**: [AWS / Azure / GCP / Multi-cloud]
**Assessment Date**: [Start] to [End]
**Assessor**: [Name / Team]

---

## 1. Executive Summary

[2-3 paragraphs summarizing cloud security posture, critical findings, and top recommendations for executive audience.]

**Overall Posture Rating**: [Critical / High / Medium / Low] Risk
**Accounts/Subscriptions Assessed**: [N]
**Total Findings**: [N] (Critical: [N], High: [N], Medium: [N], Low: [N])

---

## 2. Scope

### 2.1 Environments Assessed

| Account/Subscription | Provider | Environment | Services In Scope |
|---------------------|----------|-------------|-------------------|
| [Account ID/Name] | [AWS/Azure/GCP] | [Prod/Staging/Dev] | [EC2, S3, RDS, etc.] |

### 2.2 Assessment Framework

- CIS Benchmark for [Provider] v[X.X]
- NIST CSF alignment
- [Additional: SOC 2, PCI-DSS, HIPAA as applicable]

---

## 3. Findings Summary

### 3.1 Finding Distribution

| Category | Critical | High | Medium | Low | Info |
|----------|----------|------|--------|-----|------|
| Identity & Access | [N] | [N] | [N] | [N] | [N] |
| Network Security | [N] | [N] | [N] | [N] | [N] |
| Data Protection | [N] | [N] | [N] | [N] | [N] |
| Compute Security | [N] | [N] | [N] | [N] | [N] |
| Logging & Monitoring | [N] | [N] | [N] | [N] | [N] |
| Compliance | [N] | [N] | [N] | [N] | [N] |

### 3.2 Top 10 Critical Findings

| # | Finding | Category | Affected Resources | Remediation Priority |
|---|---------|----------|--------------------|---------------------|
| 1 | [Finding title] | [Category] | [N resources] | Immediate |
| 2 | [Finding] | [Category] | [N] | [Priority] |

---

## 4. Identity & Access Management

### 4.1 IAM Findings

| # | Finding | Severity | Resources | CIS Ref |
|---|---------|----------|-----------|---------|
| [N] | [Root account without MFA] | Critical | [Account] | [1.5] |
| [N] | [Overprivileged IAM policies] | High | [N policies] | [1.16] |
| [N] | [Unused credentials >90 days] | Medium | [N users] | [1.12] |

### 4.2 IAM Recommendations

- [ ] Enable MFA on all accounts, hardware MFA on root/admin
- [ ] Implement least privilege: remove unused permissions
- [ ] Disable/remove unused credentials
- [ ] Implement Just-In-Time access for privileged operations
- [ ] Enforce service control policies (SCPs) at organization level

---

## 5. Network Security

### 5.1 Network Findings

| # | Finding | Severity | Resources |
|---|---------|----------|-----------|
| [N] | [Security group allowing 0.0.0.0/0 on management ports] | Critical | [N SGs] |
| [N] | [No VPC flow logging enabled] | High | [N VPCs] |
| [N] | [Public subnets with direct internet routing] | Medium | [N subnets] |

### 5.2 Network Recommendations

- [ ] Remove 0.0.0.0/0 ingress rules on ports 22, 3389, 3306, etc.
- [ ] Enable VPC flow logs on all VPCs
- [ ] Implement network segmentation between environments
- [ ] Deploy WAF on internet-facing applications
- [ ] Enable DNS logging

---

## 6. Data Protection

### 6.1 Data Findings

| # | Finding | Severity | Resources |
|---|---------|----------|-----------|
| [N] | [S3 buckets with public access] | Critical | [N buckets] |
| [N] | [Unencrypted database instances] | High | [N instances] |
| [N] | [No data classification or DLP] | Medium | [Organization-wide] |

### 6.2 Data Recommendations

- [ ] Block public access on all storage (S3 Block Public Access, etc.)
- [ ] Enable encryption at rest on all data stores (KMS managed keys)
- [ ] Enable encryption in transit (TLS 1.2+)
- [ ] Implement data classification and labeling
- [ ] Deploy DLP monitoring on egress points

---

## 7. Compute Security

### 7.1 Compute Findings

| # | Finding | Severity | Resources |
|---|---------|----------|-----------|
| [N] | [Instances with IMDSv1 enabled] | High | [N instances] |
| [N] | [Containers running as root] | High | [N containers] |
| [N] | [Unpatched instances (>30 days)] | High | [N instances] |

---

## 8. Logging & Monitoring

### 8.1 Logging Findings

| # | Finding | Severity | Resources |
|---|---------|----------|-----------|
| [N] | [CloudTrail/Activity Log not enabled in all regions] | Critical | [N regions] |
| [N] | [No centralized log aggregation] | High | [Organization] |
| [N] | [No alerting on critical security events] | High | [Organization] |

---

## 9. Compliance Mapping

| Control | CIS Benchmark | Status | Finding Ref |
|---------|--------------|--------|-------------|
| [Control description] | [CIS reference] | [Pass/Fail] | [Finding #] |

---

## 10. Remediation Roadmap

### Immediate (0-7 days)

| # | Action | Finding Ref | Owner | Effort |
|---|--------|------------|-------|--------|
| 1 | [Enable MFA on root] | [F-001] | [Team] | [Low] |

### Short-Term (7-30 days)

| # | Action | Finding Ref | Owner | Effort |
|---|--------|------------|-------|--------|
| 1 | [Restrict security groups] | [F-005] | [Team] | [Medium] |

### Medium-Term (30-90 days)

| # | Action | Finding Ref | Owner | Effort |
|---|--------|------------|-------|--------|
| 1 | [Implement CSPM tooling] | [F-012] | [Team] | [High] |

---

## Appendices

### A. Tools and Methodology
### B. Full Finding Details
### C. Evidence Screenshots
### D. CIS Benchmark Compliance Matrix

## [TEMPLATE ENDS]

---

## Cross-References

- See `templates/briefs/cloud-assessment-brief.md` for assessment scoping
- See `frameworks/cloudsec-layer.md` for cloud security methodology
- See `checklists/cloud-security-assessment-quality.md` for quality gates
- See `reference/industries/saas-cloud-security.md` for cloud security context
- See `reference/tools/terraform-security-reference.md` for IaC remediation
