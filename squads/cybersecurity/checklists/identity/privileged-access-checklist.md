# Privileged Access Management Checklist

## Purpose

Comprehensive checklist for PAM implementation covering vault configuration, session recording, just-in-time access, emergency break-glass procedures, and privileged access monitoring.

## Privileged Account Inventory

- [ ] All privileged accounts identified and cataloged
- [ ] Account ownership assigned for every privileged account
- [ ] Privileged account types classified (domain admin, local admin, cloud admin, DBA, app admin)
- [ ] Service accounts inventoried with purpose and dependencies documented
- [ ] Shared accounts identified with migration plan to individual accounts
- [ ] Default vendor accounts identified and secured (changed/disabled)
- [ ] Emergency/break-glass accounts documented and secured
- [ ] Privileged account count baseline established with reduction targets

## Vault Configuration

### Credential Vault Security

- [ ] Vault solution deployed in high-availability configuration
- [ ] Vault infrastructure hardened per vendor security guide
- [ ] Vault access restricted to PAM administrators only
- [ ] Vault data encrypted at rest (AES-256 minimum)
- [ ] Vault communication encrypted in transit (TLS 1.2+)
- [ ] Vault master key stored in HSM or secure key ceremony performed
- [ ] Vault backup encrypted and stored separately from vault infrastructure
- [ ] Vault disaster recovery procedure documented and tested
- [ ] Vault audit logs forwarded to SIEM (not modifiable by vault admins)
- [ ] Vault separated from general IT infrastructure (dedicated network segment)

### Credential Management

| Credential Type | Rotation Frequency | Rotation Method | Verified |
|----------------|-------------------|----------------|----------|
| Domain admin password | After each use | Automatic (vault) | [ ] |
| Local admin password | Daily or after use | Automatic (LAPS or vault) | [ ] |
| Service account password | 90 days maximum | Automatic with dependency check | [ ] |
| Database admin password | After each use | Automatic (vault) | [ ] |
| Cloud root/admin | After each use | Automatic (vault) | [ ] |
| Network device credentials | 90 days | Automatic (vault) | [ ] |
| Application admin | After each use | Automatic (vault) | [ ] |
| SSH keys | 90 days | Automatic rotation | [ ] |
| API keys | 90 days | Automatic rotation | [ ] |

### Credential Checkout Workflow

- [ ] Checkout requires MFA authentication
- [ ] Checkout requires business justification
- [ ] High-risk checkouts require dual approval
- [ ] Checkout duration is time-bounded (default: 4 hours maximum)
- [ ] Credential is automatically changed after check-in
- [ ] Concurrent checkout prevented (exclusive use)
- [ ] Checkout notification sent to account owner
- [ ] Failed checkout attempts logged and alerted

## Session Recording

### Session Management

- [ ] All interactive privileged sessions recorded (video + keystroke)
- [ ] Session recordings stored in tamper-proof storage
- [ ] Session recordings encrypted at rest
- [ ] Retention period defined (minimum 1 year for compliance)
- [ ] Session recordings searchable by command/keyword
- [ ] Session metadata indexed (user, target, time, duration)
- [ ] Real-time session monitoring capability enabled
- [ ] Suspicious command alerting configured
- [ ] Session termination capability available for active sessions
- [ ] Session recordings accessible for incident investigation

### Session Recording Rules

| Session Type | Recording Required | Live Monitoring | Alert on Commands |
|-------------|-------------------|----------------|-------------------|
| Domain admin | Mandatory | Recommended | Yes (risky commands) |
| Cloud admin console | Mandatory | Optional | Yes (IAM changes) |
| Database admin | Mandatory | Optional | Yes (DDL, bulk operations) |
| Network device | Mandatory | Optional | Yes (config changes) |
| Production server (SSH/RDP) | Mandatory | Optional | Yes (suspicious patterns) |
| Break-glass sessions | Mandatory | Mandatory | Yes (all commands) |

### Suspicious Command Alerts

- [ ] Alert on `net user /add` or equivalent user creation
- [ ] Alert on scheduled task creation on remote systems
- [ ] Alert on service installation on remote systems
- [ ] Alert on security event log clearing
- [ ] Alert on firewall rule modification
- [ ] Alert on registry Run key modification
- [ ] Alert on password dump tool execution patterns
- [ ] Alert on mass file operations (ransomware indicator)

## Just-in-Time (JIT) Access

### JIT Configuration

- [ ] Zero standing privilege established as target state
- [ ] JIT access request workflow defined and automated
- [ ] JIT access duration defaults are minimal (1-4 hours)
- [ ] JIT access automatically expires without renewal
- [ ] JIT access can be extended with re-approval
- [ ] JIT access scope limited to specific systems/tasks
- [ ] JIT access audit trail maintained (who, what, when, why, approved by)
- [ ] JIT access denied by default (explicit grant required)

### JIT Approval Matrix

| Access Level | Approval Required | Maximum Duration | Auto-Approve |
|-------------|------------------|-----------------|-------------|
| Standard admin | Manager | 8 hours | During business hours |
| Elevated admin | Manager + Security | 4 hours | Never |
| Domain admin | Dual approval (Manager + CISO) | 2 hours | Never |
| Cloud root/org admin | Dual approval + CISO | 1 hour | Never |
| Break-glass | Post-use review only | Until revoked | Emergency only |

## Emergency Break-Glass

### Break-Glass Account Setup

- [ ] Break-glass accounts created for critical systems (AD, cloud root, network)
- [ ] Break-glass credentials sealed in secure envelope or HSM
- [ ] Break-glass credentials known to minimum 2 people (dual custody)
- [ ] Break-glass accounts exempt from conditional access (but logged)
- [ ] Break-glass accounts have unique, strong passwords (30+ characters)
- [ ] Break-glass accounts have hardware MFA tokens (stored securely)
- [ ] Break-glass account usage triggers immediate critical alert
- [ ] Break-glass procedure documented and accessible during outages

### Break-Glass Procedure

```
1. Determine break-glass is necessary (PAM unavailable, critical outage)
2. Two authorized individuals retrieve sealed credentials
3. Log usage in out-of-band system (even paper log if needed)
4. Perform required actions with minimal scope
5. Immediately after use:
   - Change break-glass credentials
   - Reseal new credentials
   - Submit incident report
   - Review all actions taken
6. Post-use audit within 24 hours
```

### Break-Glass Testing

- [ ] Break-glass procedure tested quarterly
- [ ] Test includes credential retrieval, system access, and re-sealing
- [ ] Test results documented
- [ ] Identified issues remediated within 30 days

## Monitoring and Alerting

### PAM-Specific Alerts

| Alert | Severity | Response |
|-------|----------|----------|
| Break-glass account used | Critical | Immediate investigation |
| Vault admin login | High | Verify authorized |
| Failed vault authentication (3+) | High | Investigate, possible attack |
| Credential checkout outside business hours | Medium | Review next business day |
| Session recording failure | High | Investigate, may indicate tampering |
| Privilege escalation on managed host | High | Correlate with checkout |
| Vault configuration change | High | Verify change management ticket |
| New privileged account created outside PAM | Critical | Investigate, bring under management |

### Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| Privileged accounts in vault | >95% | Monthly |
| Standing privilege accounts | Decreasing trend | Monthly |
| JIT adoption rate | >80% | Monthly |
| Average session duration | Decreasing trend | Monthly |
| Credential rotation compliance | 100% | Monthly |
| Break-glass usage | 0 (unless emergency) | Monthly |
| Session recording coverage | 100% | Monthly |

## Cross-References

- [Identity Governance Framework](../../frameworks/identity-governance-framework.md) -- PAM governance
- [Service Account Checklist](service-account-checklist.md) -- service account management
- [Directory Services Checklist](directory-services-checklist.md) -- AD admin security
- [Active Directory Attack Defense](../../frameworks/active-directory-attack-defense.md) -- AD hardening
