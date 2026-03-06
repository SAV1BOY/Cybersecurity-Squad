# Identity Governance Framework

## Purpose

Comprehensive identity governance and administration (IGA) framework covering the full identity lifecycle. Ensures appropriate access through role management, access certification, segregation of duties enforcement, and privileged access management.

## Identity Lifecycle Management

### Lifecycle Phases

| Phase | Trigger | Actions | Owner |
|-------|---------|---------|-------|
| Joiner | New hire, contractor start | Provision base access per role, assign manager, enroll MFA, issue credentials | HR + IT |
| Mover | Transfer, promotion, role change | Adjust access to match new role, revoke previous role access, review privileges | Manager + IGA system |
| Leaver | Termination, contract end | Disable account (immediate), revoke all access, transfer data ownership, archive mailbox | HR + IT (automated) |
| Temporary | Project assignment, break-glass | Time-bounded access with automatic expiration, enhanced logging | Manager + Security |

### Provisioning Standards

**Joiner Process:**
1. HR creates identity record in HRIS (source of truth)
2. IGA system auto-provisions accounts based on role template
3. Base access granted: email, intranet, collaboration tools
4. Role-specific access per role catalog
5. Manager verifies access within 3 business days
6. User completes security awareness training before sensitive access
7. MFA enrollment required within 24 hours

**Leaver Process (Critical Path):**
1. HR triggers termination in HRIS
2. IGA disables all accounts within 1 hour (involuntary) or end of day (voluntary)
3. Active sessions terminated across all SSO-integrated applications
4. VPN and remote access revoked immediately
5. Service account ownership transferred
6. Shared credentials rotated if user had access
7. Email forwarding set (manager approval required)
8. Account deletion after 90-day retention period

## Access Certification

### Certification Campaigns

| Campaign Type | Scope | Frequency | Reviewer | SLA |
|--------------|-------|-----------|----------|-----|
| Manager certification | All direct report access | Quarterly | People manager | 14 days |
| Application owner | All users of application | Semi-annually | App owner | 21 days |
| Privileged access | Admin/elevated access | Monthly | Security team + manager | 7 days |
| Sensitive data | Access to restricted data | Quarterly | Data owner | 14 days |
| Orphan account | Accounts without owners | Monthly | Security team | 7 days |

### Certification Decisions

| Decision | Meaning | Action |
|----------|---------|--------|
| Approve | Access is appropriate | Access retained, timestamp recorded |
| Revoke | Access is no longer needed | Access removed within 24 hours |
| Modify | Access level needs adjustment | Route to access request workflow |
| Delegate | Reviewer cannot assess | Escalate to secondary reviewer |
| Flag | Suspicious or unusual access | Route to security for investigation |

### Non-Response Handling
- Reminder at 50% of SLA
- Escalation to reviewer's manager at 75% of SLA
- Auto-revoke at SLA expiry (configurable per risk level)
- Non-compliance reported to governance committee

## Role Mining and Management

### Role Engineering Process

1. **Data collection** -- Extract current access assignments across all systems
2. **Cluster analysis** -- Identify common access patterns using role mining algorithms
3. **Role definition** -- Create role templates with appropriate access bundles
4. **Validation** -- Business owners validate role definitions
5. **Assignment** -- Map users to roles, identify outliers
6. **Monitoring** -- Track role drift, unused permissions, and exceptions

### Role Catalog Structure

```
Role: [Business Role Name]
Department: [Department]
Job Family: [Job family/function]
Access Includes:
  - [Application 1]: [Permission level]
  - [Application 2]: [Permission level]
  - [Network share]: [Read/Write]
  - [Distribution group]: [Member]
Segregation of Duties Conflicts: [Conflicting roles]
Risk Level: [High/Medium/Low]
Certification Frequency: [Based on risk]
Owner: [Business owner]
```

## Segregation of Duties (SoD)

### SoD Conflict Matrix

| Function A | Function B | Risk | Control |
|-----------|-----------|------|---------|
| Purchase requisition | Purchase approval | Fraud | Preventive (block) |
| Payment creation | Payment approval | Fraud | Preventive (block) |
| User provisioning | Access certification | Conflict of interest | Detective (alert) |
| Code development | Production deployment | Integrity | Preventive (block) |
| Security rule creation | Security rule approval | Bypass | Preventive (block) |
| Account creation | Account privilege assignment | Elevation | Detective (alert) |
| Backup administration | Backup audit | Concealment | Detective (alert) |

### SoD Enforcement Levels

| Level | Mechanism | Response |
|-------|-----------|----------|
| Preventive | System blocks conflicting assignment | Access denied, exception request required |
| Detective | Alert on conflicting assignment | Review within 48 hours, compensating control required |
| Monitoring | Report on existing conflicts | Quarterly review, remediation plan required |

## Privileged Access Management (PAM)

### Privileged Account Types

| Type | Examples | Controls |
|------|----------|----------|
| Domain admin | AD Domain Admins, Enterprise Admins | Dedicated admin workstation, MFA, session recording |
| Local admin | Server local admin, root | Password vault, checkout with approval |
| Cloud admin | AWS root, Azure Global Admin, GCP org admin | Hardware MFA, break-glass only, conditional access |
| Database admin | DBA accounts, sa/root | Password vault, session recording, query logging |
| Application admin | Application super-admin accounts | MFA, access certification, audit logging |
| Service account | Automated process accounts | Managed service account, no interactive login, key rotation |
| Emergency access | Break-glass accounts | Sealed credentials, dual custody, full audit, time-bounded |

### PAM Architecture

```
User -> MFA Challenge -> PAM Gateway -> Credential Vault -> Target System
                                    |
                              Session Recording
                                    |
                              Audit / SIEM
```

### PAM Requirements

1. All privileged credentials stored in vault (zero standing privilege goal)
2. Just-in-time (JIT) access: check out credentials for defined time window
3. Approval workflow for high-risk access (dual approval)
4. Full session recording for interactive privileged sessions
5. Automatic credential rotation after each use (or on schedule)
6. Emergency break-glass procedure with post-use review
7. Integration with SIEM for anomaly detection on privileged activity

## Metrics and Reporting

| Metric | Target | Frequency |
|--------|--------|-----------|
| Certification completion rate | >95% within SLA | Per campaign |
| Orphan accounts | 0 | Monthly |
| SoD violations (unresolved) | 0 critical | Monthly |
| Privileged account count | Decreasing trend | Monthly |
| JIT adoption rate | >90% of privileged access | Monthly |
| Mean time to deprovision (leaver) | < 1 hour (involuntary) | Per event |
| Access request fulfillment time | < 4 hours (standard) | Monthly |

## Cross-References

- [SSO Security Checklist](../checklists/identity/sso-security-checklist.md) -- SSO configuration
- [Privileged Access Checklist](../checklists/identity/privileged-access-checklist.md) -- PAM implementation
- [MFA Implementation Checklist](../checklists/identity/mfa-implementation-checklist.md) -- MFA deployment
- [Service Account Checklist](../checklists/identity/service-account-checklist.md) -- service account governance
- [Directory Services Checklist](../checklists/identity/directory-services-checklist.md) -- AD/LDAP security
