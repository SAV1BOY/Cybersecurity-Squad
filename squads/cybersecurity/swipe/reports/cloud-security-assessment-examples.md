# Cloud Security Posture Assessment Report Examples

## Purpose

Templates for cloud security posture assessment reports covering misconfiguration findings, IAM review, compliance mapping, and cloud-specific risk presentation. Applicable to AWS, Azure, and GCP environments.

## Report Structure

### 1. Executive Summary

```markdown
# Cloud Security Posture Assessment Report

**Organization:** [Name]
**Cloud Providers:** AWS (primary), Azure (secondary)
**Assessment Period:** [Date range]
**Assessor:** [Name/Team]

## Executive Summary

Assessment of [Organization]'s cloud infrastructure across [N] AWS accounts
and [N] Azure subscriptions identified [total] security findings including
[critical] critical misconfigurations requiring immediate remediation.

### Posture Overview

| Severity | AWS | Azure | Total |
|----------|-----|-------|-------|
| Critical | 5 | 2 | 7 |
| High | 18 | 8 | 26 |
| Medium | 42 | 15 | 57 |
| Low | 31 | 12 | 43 |
| **Total** | **96** | **37** | **133** |

### Cloud Security Score

| Domain | Score | Rating |
|--------|-------|--------|
| Identity & Access | 45/100 | Poor |
| Network Security | 72/100 | Good |
| Data Protection | 58/100 | Fair |
| Logging & Monitoring | 65/100 | Fair |
| Compute Security | 70/100 | Good |
| **Overall** | **62/100** | **Fair** |

### Top 3 Risks
1. **15 IAM roles with AdministratorAccess** -- violates least privilege,
   any compromised role grants full account control
2. **S3 buckets with public read access** -- 3 buckets containing internal
   data accessible from the internet
3. **CloudTrail logging gaps** -- 2 accounts missing CloudTrail, no
   management event visibility
```

### 2. IAM Review

```markdown
## Identity and Access Management Review

### IAM Statistics

| Metric | AWS | Azure | Risk Level |
|--------|-----|-------|-----------|
| Total IAM users | 142 | 85 | -- |
| Users without MFA | 23 (16%) | 12 (14%) | High |
| Admin-level users | 15 | 8 | Critical |
| Inactive users (90+ days) | 18 | 7 | High |
| Access keys > 90 days old | 34 | N/A | High |
| Service accounts | 67 | 42 | -- |
| Cross-account roles | 28 | N/A | Medium |
| Root account usage (last 90 days) | 3 events | N/A | Critical |

### IAM Finding: Overly Permissive Roles

**Finding ID:** CLOUD-IAM-001
**Severity:** Critical
**Provider:** AWS
**Service:** IAM

**Condition:**
15 IAM roles have `AdministratorAccess` or equivalent (`*:*`) policies attached.
Only 3 of these roles require broad access (break-glass accounts).

| Role Name | Last Used | Attached Policies | Actual Services Used |
|-----------|-----------|-------------------|---------------------|
| DevOps-Role | 2 hours ago | AdministratorAccess | EC2, S3, Lambda, CloudFormation |
| Data-Pipeline | 1 day ago | AdministratorAccess | S3, Glue, Athena |
| App-Deploy | 3 hours ago | AdministratorAccess | ECS, ECR, CloudWatch |
| [12 more] | ... | ... | ... |

**Risk:** Compromise of any of these roles grants full account control.
Blast radius is the entire AWS account.

**Recommendation:**
1. Analyze IAM Access Analyzer findings for each role
2. Generate least-privilege policies based on actual usage (Access Analyzer policy generation)
3. Implement permission boundaries for all non-break-glass roles
4. Reduce to 3 admin roles (break-glass only)
5. Timeline: 30 days for critical roles, 60 days for all

### IAM Finding: Service Account Key Management

**Finding ID:** CLOUD-IAM-003
**Severity:** High
**Provider:** AWS

**Condition:**
34 IAM access key pairs are older than 90 days. 8 keys have not been used
in over 180 days.

| Access Key Age | Count | Risk |
|---------------|-------|------|
| 90-180 days | 26 | High |
| 180-365 days | 6 | Critical |
| > 365 days | 2 | Critical |

**Recommendation:**
1. Disable unused keys immediately (8 keys)
2. Rotate all keys > 90 days within 2 weeks
3. Implement key rotation automation (AWS Secrets Manager)
4. Migrate to IAM roles/IRSA where possible (eliminate keys)
```

### 3. Misconfiguration Findings

```markdown
## Infrastructure Misconfiguration Findings

### Finding: Public S3 Buckets

**Finding ID:** CLOUD-S3-001
**Severity:** Critical
**Provider:** AWS
**Service:** S3

**Condition:**
3 S3 buckets have public read access enabled via bucket policy or ACL.

| Bucket | Access Type | Data Classification | Account |
|--------|-----------|--------------------:|---------|
| company-reports-2025 | Public via bucket policy | Internal | Production |
| staging-assets | Public via ACL | Internal | Staging |
| data-exports | Public via bucket policy | Confidential | Analytics |

**Evidence:**
```
$ aws s3api get-bucket-policy-status --bucket data-exports
{
    "PolicyStatus": {
        "IsPublic": true
    }
}
```

**Impact:** Confidential data in `data-exports` bucket is accessible to
anyone on the internet without authentication.

**Remediation:**
1. Immediately remove public access from all 3 buckets
2. Enable S3 Block Public Access at the account level
3. Implement SCP to prevent future public bucket creation
4. Scan bucket contents for sensitive data exposure

### Finding: Unencrypted Storage

**Finding ID:** CLOUD-ENC-001
**Severity:** High
**Provider:** AWS, Azure

**Condition:**
| Resource Type | Unencrypted Count | Total | % Unencrypted |
|--------------|-------------------|-------|---------------|
| EBS Volumes | 45 | 312 | 14% |
| RDS Instances | 2 | 18 | 11% |
| S3 Buckets | 8 | 95 | 8% |
| Azure Managed Disks | 5 | 67 | 7% |

**Remediation:**
1. Enable default EBS encryption per region (account-level setting)
2. Encrypt unencrypted RDS instances (requires snapshot + restore)
3. Enable default S3 encryption (SSE-S3 minimum, SSE-KMS preferred)
4. Enable Azure disk encryption on all managed disks

### Finding: Security Groups with Unrestricted Access

**Finding ID:** CLOUD-NET-002
**Severity:** High
**Provider:** AWS

**Condition:**
12 security groups allow inbound access from 0.0.0.0/0 on sensitive ports.

| Port | Protocol | Security Groups | Attached Resources |
|------|----------|----------------|-------------------|
| 22 (SSH) | TCP | sg-abc123, sg-def456 | 8 EC2 instances |
| 3389 (RDP) | TCP | sg-ghi789 | 3 EC2 instances |
| 3306 (MySQL) | TCP | sg-jkl012 | 2 RDS instances |
| 5432 (Postgres) | TCP | sg-mno345 | 1 RDS instance |
| 0-65535 (All) | All | sg-pqr678 | 4 EC2 instances |

**Remediation:**
1. Restrict SSH/RDP to VPN CIDR or bastion security group only
2. Database ports must never be exposed to 0.0.0.0/0 -- restrict to application tier SGs
3. Remove "all traffic" rules and replace with specific port allowances
4. Implement AWS Config rule to detect and auto-remediate
```

### 4. Compliance Mapping

```markdown
## Compliance Mapping

### CIS Benchmark Compliance (AWS CIS v3.0)

| Section | Controls | Passed | Failed | Score |
|---------|----------|--------|--------|-------|
| 1 - IAM | 22 | 14 | 8 | 64% |
| 2 - Storage | 8 | 5 | 3 | 63% |
| 3 - Logging | 14 | 10 | 4 | 71% |
| 4 - Monitoring | 15 | 8 | 7 | 53% |
| 5 - Networking | 6 | 4 | 2 | 67% |
| **Total** | **65** | **41** | **24** | **63%** |

### Failed Controls Detail

| CIS Control | Description | Status | Finding ID |
|------------|-------------|--------|-----------|
| 1.4 | Root account should not have access keys | FAIL | CLOUD-IAM-005 |
| 1.5 | MFA enabled for root account | FAIL | CLOUD-IAM-006 |
| 1.10 | MFA enabled for all IAM users with console | FAIL | CLOUD-IAM-002 |
| 2.1.1 | S3 Block Public Access enabled | FAIL | CLOUD-S3-001 |
| 2.1.2 | S3 default encryption enabled | FAIL | CLOUD-ENC-001 |
| 3.1 | CloudTrail enabled in all regions | FAIL | CLOUD-LOG-001 |
| ... | ... | ... | ... |

### Regulatory Mapping

| Finding | PCI DSS 4.0 | SOC 2 | HIPAA | GDPR |
|---------|------------|-------|-------|------|
| CLOUD-IAM-001 (admin access) | 7.2.2 | CC6.1 | 164.312(a) | Art. 32 |
| CLOUD-S3-001 (public buckets) | 1.3.1 | CC6.6 | 164.312(e) | Art. 32 |
| CLOUD-ENC-001 (no encryption) | 3.5.1 | CC6.7 | 164.312(a)(2)(iv) | Art. 32 |
| CLOUD-LOG-001 (logging gaps) | 10.2 | CC7.2 | 164.312(b) | Art. 30 |
```

### 5. Remediation Roadmap

```markdown
## Remediation Roadmap

### Immediate (0-48 hours) -- 7 Critical Findings
| ID | Finding | Action | Owner |
|----|---------|--------|-------|
| CLOUD-S3-001 | Public S3 buckets | Remove public access, enable Block Public Access | Cloud Ops |
| CLOUD-IAM-005 | Root access keys | Delete root access keys | Cloud Ops |
| CLOUD-IAM-006 | Root MFA | Enable hardware MFA on root | Cloud Ops |
| CLOUD-LOG-001 | Missing CloudTrail | Enable org-level CloudTrail | Security |
| CLOUD-NET-003 | Database public access | Restrict security groups | Cloud Ops |

### Short-Term (1-2 weeks) -- 26 High Findings
[Prioritized list with owners]

### Medium-Term (30 days) -- 57 Medium Findings
[Grouped by remediation category]

### Automated Remediation Recommendations
| Finding Category | Auto-Remediation | Tool |
|-----------------|-----------------|------|
| Public S3 buckets | Auto-remove public access | AWS Config + Lambda |
| Unencrypted resources | Auto-enable encryption | AWS Config + SSM |
| Unused IAM keys | Auto-disable after 90 days | Lambda scheduled |
| Open security groups | Alert + auto-restrict | AWS Config + Lambda |
```

## Cross-References

- [Secure Cloud Architecture](../../frameworks/secure-cloud-architecture.md) -- architecture patterns
- [Cloud Shared Responsibility](../../frameworks/cloud-shared-responsibility.md) -- responsibility model
- [Cloud Compromise Runbook](../runbooks/cloud-compromise-runbook.md) -- incident response
- [Cloud Security Assessment Checklist](../../checklists/cloud-security-assessment-quality.md) -- quality gates
