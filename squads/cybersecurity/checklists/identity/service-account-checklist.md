# Service Account Security Checklist

## Purpose

Checklist for securing service accounts across on-premises and cloud environments. Covers inventory, least privilege enforcement, credential rotation, monitoring, and lifecycle management.

## Service Account Inventory

- [ ] Complete inventory of all service accounts maintained
- [ ] Each service account has a documented owner (individual, not team)
- [ ] Each service account has a documented purpose/business justification
- [ ] Service account dependencies documented (what breaks if disabled)
- [ ] Service accounts classified by risk level (critical, high, medium, low)
- [ ] Inventory reconciled quarterly against active directory and cloud IAM
- [ ] Orphan accounts (no owner, no documented purpose) identified and remediated

### Inventory Template

| Account Name | Type | Owner | Purpose | Systems | Risk Level | Last Review |
|-------------|------|-------|---------|---------|------------|-------------|
| svc-backup | AD service acct | J. Smith | Backup agent | Backup servers | High | 2026-02-01 |
| app-api-prod | Cloud IAM role | K. Chen | API service | Production ECS | Critical | 2026-01-15 |

## Least Privilege

### Permission Assessment

- [ ] Each service account reviewed for minimum required permissions
- [ ] No service account has domain admin or equivalent privileges
- [ ] Service accounts restricted to specific systems/resources they need
- [ ] Write access only where writes are required
- [ ] Network access restricted to required destinations only
- [ ] Cloud service accounts use narrowest IAM policy possible
- [ ] Unused permissions identified and removed (IAM Access Analyzer or equivalent)
- [ ] Permission creep detected and remediated during quarterly reviews

### AD Service Account Hardening

- [ ] Group Managed Service Accounts (gMSA) used where possible
- [ ] Interactive logon denied (`Deny log on locally` GPO)
- [ ] RDP logon denied (`Deny log on through Remote Desktop Services` GPO)
- [ ] Account restricted to specific computers (`Log on to` setting)
- [ ] Service account cannot change its own password (managed by system/vault)
- [ ] Account is member of minimal groups (removed from Domain Users if possible)
- [ ] Delegation restricted (not trusted for delegation unless explicitly required)
- [ ] If delegation required, constrained delegation configured (not unconstrained)
- [ ] Kerberos AES encryption enforced (disable RC4 to prevent Kerberoasting)
- [ ] Account has strong password (30+ characters, random)

### Cloud Service Account Hardening

- [ ] Workload identity/instance profiles used instead of long-lived keys where possible
- [ ] No access keys for cloud service accounts (use IAM roles/managed identity)
- [ ] If keys required, keys stored in secrets manager (not in code/config)
- [ ] Cross-account access uses role assumption with external ID
- [ ] Service account has inline policy (not attached to broad managed policies)
- [ ] Condition keys used to restrict by source IP, VPC, or time
- [ ] No `*:*` or wildcard resource permissions
- [ ] Cloud audit logging covers service account API calls

## Credential Management

### Credential Rotation

| Credential Type | Rotation Frequency | Method | Verified |
|----------------|-------------------|--------|----------|
| AD service account password | 90 days (or use gMSA) | PAM vault or gMSA auto-rotation | [ ] |
| Cloud access keys | 90 days maximum | Automated rotation via secrets manager | [ ] |
| API keys | 90 days | Automated rotation with zero-downtime swap | [ ] |
| Database credentials | 90 days | Secrets manager with connection pool refresh | [ ] |
| SSH keys | 90 days | Certificate-based auth preferred | [ ] |
| Application secrets | 90 days | Secrets manager, deployment pipeline injection | [ ] |
| OAuth client secrets | 180 days | Manual rotation with testing | [ ] |

### Credential Storage

- [ ] No credentials in source code (git history scanned and cleaned)
- [ ] No credentials in environment variables on shared systems
- [ ] No credentials in configuration files (use secrets manager references)
- [ ] No credentials in CI/CD pipeline definitions (use pipeline secrets)
- [ ] No credentials in container images (use runtime injection)
- [ ] No credentials in documentation or wikis
- [ ] Secret scanning enabled in code repositories
- [ ] Credential exposure alerts forwarded to security team

## Monitoring

### Service Account Monitoring Rules

| Rule | Severity | Detection Logic |
|------|----------|----------------|
| Interactive login by service account | Critical | Logon type 2 (interactive) or 10 (RDP) by service account |
| Service account authentication from new source | High | Source IP/host not in baseline |
| Service account used outside normal hours | Medium | Authentication outside expected time window |
| Service account privilege escalation | Critical | Adding self to privileged groups |
| Service account password changed manually | High | Not by rotation system |
| New service account created | Medium | Any new account matching naming convention |
| Service account accessing unusual resources | High | File shares, databases outside normal pattern |
| Service account authentication failure spike | Medium | >3 failures in 5 minutes |
| Service account key created (cloud) | High | New long-lived credential created |

### Baseline Documentation

- [ ] Normal authentication patterns documented per service account
- [ ] Expected source systems documented
- [ ] Expected time windows documented
- [ ] Expected destination resources documented
- [ ] Baseline reviewed and updated when service changes occur

## Lifecycle Management

### Service Account Creation

- [ ] Request requires manager and security approval
- [ ] Business justification documented
- [ ] Owner assigned (individual who is accountable)
- [ ] Expiration date set (default: 1 year, renewable with re-approval)
- [ ] Permissions defined using least privilege principle
- [ ] Naming convention followed (e.g., `svc-<app>-<function>`)
- [ ] Password generated by vault/PAM (30+ characters)
- [ ] Account added to monitoring baseline
- [ ] Account registered in service account inventory

### Service Account Review (Quarterly)

- [ ] Owner confirms account is still needed
- [ ] Permissions reviewed and trimmed
- [ ] Last usage verified (disable if unused for 90 days)
- [ ] Dependencies revalidated
- [ ] Credential rotation verified
- [ ] Monitoring rules confirmed active
- [ ] Risk classification revalidated

### Service Account Decommission

- [ ] Dependent services identified and migrated
- [ ] Account disabled (not deleted immediately)
- [ ] 30-day observation period for dependencies
- [ ] Account deleted after observation period
- [ ] Inventory updated
- [ ] Associated secrets/keys deleted from vault
- [ ] Monitoring rules removed
- [ ] Owner notified of decommission

## Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| Service accounts with documented owner | 100% | Monthly |
| Service accounts with gMSA (AD) | >80% | Monthly |
| Service accounts with no access keys (cloud) | >90% | Monthly |
| Credential rotation compliance | 100% | Monthly |
| Service accounts with interactive login denied | 100% (AD) | Monthly |
| Orphan service accounts | 0 | Monthly |
| Average permissions per service account | Decreasing | Quarterly |

## Cross-References

- [Privileged Access Checklist](privileged-access-checklist.md) -- PAM for service accounts
- [Directory Services Checklist](directory-services-checklist.md) -- AD service account specifics
- [Identity Governance Framework](../../frameworks/identity-governance-framework.md) -- lifecycle governance
- [Credential Attack Methodology](../../frameworks/credential-attack-methodology.md) -- attack vectors
