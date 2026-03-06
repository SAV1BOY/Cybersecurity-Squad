# MFA Implementation Checklist

## Purpose

Comprehensive checklist for MFA deployment covering method selection, enrollment procedures, recovery mechanisms, and phishing-resistant options. Ensures MFA is effectively deployed without creating operational gaps.

## MFA Method Assessment

### Method Comparison

| Method | Phishing Resistant | Convenience | Security Level | Recommended |
|--------|-------------------|-------------|---------------|-------------|
| FIDO2/WebAuthn (hardware key) | Yes | Medium | Highest | Primary for high-risk |
| FIDO2/WebAuthn (platform) | Yes | High | High | Primary for all users |
| TOTP (authenticator app) | No | Medium | Medium | Acceptable fallback |
| Push notification (with number matching) | Partial | High | Medium-High | Acceptable with controls |
| Push notification (simple approve) | No | High | Low | Not recommended |
| SMS OTP | No | High | Low | Not recommended |
| Voice call | No | Medium | Low | Not recommended |
| Email OTP | No | Medium | Low | Not recommended |
| Smart card/PIV | Yes | Low | High | Government/regulated |

### Method Selection Decisions

- [ ] Primary MFA method selected for general population
- [ ] Primary MFA method selected for privileged users
- [ ] Phishing-resistant MFA mandated for admin accounts
- [ ] Fallback method defined (if primary unavailable)
- [ ] SMS/voice deprecated or restricted to low-risk only
- [ ] Push notification configured with number matching (if used)
- [ ] Method selection documented with risk acceptance for non-ideal methods

## Pre-Deployment Planning

### Infrastructure Readiness

- [ ] Identity provider supports selected MFA methods
- [ ] FIDO2 server capability confirmed (if using WebAuthn)
- [ ] Authenticator app distribution plan defined
- [ ] Hardware security key procurement completed (if applicable)
- [ ] Network connectivity verified for MFA verification endpoints
- [ ] Conditional access policies drafted
- [ ] Integration testing completed for all protected applications
- [ ] Helpdesk prepared for enrollment support volume
- [ ] Self-service enrollment portal configured

### Scope and Phasing

| Phase | Scope | Timeline | Success Criteria |
|-------|-------|----------|-----------------|
| 1 | IT and security staff | Week 1-2 | 100% enrolled, issues identified |
| 2 | Executives and privileged users | Week 3-4 | 100% enrolled, phishing-resistant |
| 3 | General employees (pilot group) | Week 5-8 | 90% enrolled, support volume manageable |
| 4 | All remaining employees | Week 9-12 | 95% enrolled |
| 5 | Contractors and external users | Week 13-16 | 90% enrolled |
| 6 | Enforcement (block non-MFA) | Week 17+ | 100% enforced |

## Enrollment

### Enrollment Process

- [ ] Self-service enrollment portal deployed and tested
- [ ] Step-by-step enrollment guides created (per method, per platform)
- [ ] Video tutorials available
- [ ] In-person enrollment support available for first 2 weeks
- [ ] Enrollment deadline communicated (minimum 30 days notice)
- [ ] Reminder communications scheduled (weekly until deadline)
- [ ] Enrollment progress dashboard available to management
- [ ] Escalation process for non-enrolled users defined

### Enrollment Security

- [ ] Initial MFA enrollment requires identity verification (in-person or video call for high-risk)
- [ ] Enrollment from trusted network/device preferred
- [ ] Enrollment notification sent to user's secondary contact
- [ ] Admin enrollment override requires manager approval
- [ ] Bulk enrollment prevention (rate limiting)
- [ ] Enrollment of new MFA device alerts user via email/SMS
- [ ] Grace period for enrollment defined (with justification)
- [ ] Users required to register minimum 2 MFA methods

### FIDO2 Key Enrollment

- [ ] Hardware keys distributed securely (in-person or verified shipping)
- [ ] Key attestation verified (ensure genuine keys, not emulated)
- [ ] PIN/biometric configured on key during enrollment
- [ ] Backup key enrollment required (second key)
- [ ] Key registration associated with correct user identity
- [ ] Lost key reporting process established
- [ ] Key inventory maintained (assigned, spare, decommissioned)

## Recovery Mechanisms

### Account Recovery When MFA Unavailable

| Recovery Method | Security | Use Case | Verified |
|----------------|----------|----------|----------|
| Backup MFA method (second key, backup codes) | High | Lost primary device | [ ] |
| Identity verification by help desk | Medium | All methods unavailable | [ ] |
| Manager-approved temporary bypass | Medium | Emergency access | [ ] |
| TAP (Temporary Access Pass) | Medium | Device replacement | [ ] |
| In-person identity verification | High | Full credential reset | [ ] |

### Recovery Process Security

- [ ] Help desk identity verification procedure documented
- [ ] Verification requires multiple identity proof points (employee ID + manager confirmation)
- [ ] Social engineering resistant (no reset based on "urgency" alone)
- [ ] Recovery events logged and auditable
- [ ] Temporary bypass is time-limited (maximum 24 hours)
- [ ] User must re-enroll MFA after recovery
- [ ] Recovery events trigger notification to user and manager
- [ ] Backup codes generated at enrollment (stored securely by user)
- [ ] Backup codes are single-use and limited quantity (8-10)

### Help Desk Verification Protocol

```
Before resetting MFA, help desk must:
1. Verify caller identity via employee number AND date of birth
2. Confirm with caller's manager via separate communication channel
3. Issue Temporary Access Pass (not permanent MFA reset)
4. TAP expires in 1 hour maximum
5. User must re-enroll MFA within 24 hours
6. Log the event with ticket number and verification details
```

## Conditional Access Policies

### Policy Configuration

- [ ] MFA required for all cloud application access
- [ ] MFA required for all VPN/remote access
- [ ] MFA required for admin portal access (Azure AD, AWS, GCP)
- [ ] MFA required for email access from non-managed devices
- [ ] Step-up MFA for sensitive operations (password change, role elevation)
- [ ] MFA challenge frequency configured (avoid excessive prompts)
- [ ] Trusted location policy configured (office networks, but still enforce MFA)
- [ ] Device compliance integrated with MFA policy
- [ ] Legacy authentication blocked (does not support MFA)
- [ ] Named exclusions documented with risk acceptance

### Conditional Access Testing

- [ ] Each policy tested in report-only mode before enforcement
- [ ] Edge cases tested (new device, new location, new application)
- [ ] Break-glass account excluded from conditional access
- [ ] Policy interactions tested (no conflicting policies)
- [ ] Sign-in logs reviewed after enforcement (unexpected blocks)

## Phishing-Resistant MFA

### FIDO2/WebAuthn Requirements

- [ ] FIDO2 security keys certified (FIDO Alliance certification)
- [ ] Platform authenticators enabled (Windows Hello, Touch ID, Face ID)
- [ ] Relying party ID correctly configured (matches application domain)
- [ ] Attestation verified during registration (if required by policy)
- [ ] User verification required (PIN or biometric)
- [ ] Resident credentials configured where needed (passwordless)
- [ ] Cross-origin authentication properly restricted
- [ ] FIDO2 metadata service integrated for key validation

### Passwordless Configuration (If Applicable)

- [ ] Passwordless authentication flow tested end-to-end
- [ ] Password fallback disabled for passwordless users
- [ ] Passwordless works across all required applications
- [ ] Mobile device passwordless flow tested
- [ ] Passwordless enrollment process defined
- [ ] User communication explains passwordless benefits

## Monitoring and Metrics

### MFA Monitoring

| Monitor | Alert Condition | Action |
|---------|----------------|--------|
| MFA bypass attempts | Any authentication without MFA | Investigate |
| MFA fatigue (push bombing) | >5 push requests in 10 minutes | Alert + contact user |
| New MFA device registration | Any new device enrolled | Notify user |
| MFA failure rate spike | >2x baseline | Investigate (attack or outage) |
| Legacy auth attempts | Any non-MFA capable auth | Block + notify |
| Enrollment deadline approaching | Users not enrolled | Escalate to manager |

### Program Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| MFA enrollment rate | 100% | Weekly during rollout |
| Phishing-resistant MFA adoption | >90% (high-risk users) | Monthly |
| MFA-related help desk tickets | Decreasing trend | Monthly |
| Legacy authentication volume | 0 | Monthly |
| Successful MFA challenges | >99% (not failing) | Weekly |
| Recovery/bypass events | Decreasing trend | Monthly |

## Cross-References

- [SSO Security Checklist](sso-security-checklist.md) -- MFA in SSO context
- [Privileged Access Checklist](privileged-access-checklist.md) -- MFA for PAM
- [Identity Governance Framework](../../frameworks/identity-governance-framework.md) -- governance
- [BEC Runbook](../../swipe/runbooks/business-email-compromise-runbook.md) -- MFA bypass incidents
