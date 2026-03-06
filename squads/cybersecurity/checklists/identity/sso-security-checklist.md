# SSO Security Checklist

## Purpose

Security checklist for Single Sign-On implementations covering SAML, OIDC, and OAuth 2.0 configuration hardening, token handling, session management, and federation trust validation.

## SAML Configuration

### Identity Provider (IdP) Hardening

- [ ] SAML assertions are signed (mandatory)
- [ ] SAML responses are signed (recommended in addition to assertions)
- [ ] SAML assertions are encrypted (for sensitive applications)
- [ ] Strong signing algorithm used (RSA-SHA256 minimum, not SHA1)
- [ ] IdP signing certificate is RSA 2048-bit minimum (4096 preferred)
- [ ] Certificate rotation plan documented and tested
- [ ] IdP metadata endpoint is HTTPS-only
- [ ] IdP discovery is restricted to authorized service providers

### Service Provider (SP) Configuration

- [ ] SP validates assertion signature before processing
- [ ] SP validates Issuer field matches expected IdP
- [ ] SP validates Audience/AudienceRestriction matches SP entity ID
- [ ] SP validates NotBefore and NotOnOrAfter conditions
- [ ] SP validates InResponseTo matches original AuthnRequest ID
- [ ] SP validates Destination matches SP ACS URL
- [ ] SP validates SubjectConfirmation recipient and timing
- [ ] SP rejects unsigned assertions
- [ ] SP rejects assertions with XML signature wrapping attacks
- [ ] ACS URL is HTTPS-only
- [ ] Only expected ACS URLs are registered at IdP

### SAML Attack Prevention

| Attack | Mitigation | Check |
|--------|-----------|-------|
| XML Signature Wrapping | Validate signature covers entire assertion | [ ] |
| Assertion replay | Enforce NotOnOrAfter, track used assertion IDs | [ ] |
| Certificate substitution | Pin IdP certificate or validate chain | [ ] |
| XXE injection | Disable external entity processing in XML parser | [ ] |
| SAML Response injection | Validate InResponseTo and Destination | [ ] |
| Recipient mismatch | Validate Recipient matches ACS URL | [ ] |

## OIDC/OAuth 2.0 Configuration

### Authorization Server

- [ ] Authorization code flow with PKCE used (not implicit flow)
- [ ] Implicit flow disabled for all clients
- [ ] Client credentials stored securely (not in client-side code)
- [ ] Redirect URIs are exact match (no wildcards)
- [ ] Redirect URIs use HTTPS only
- [ ] Token endpoint requires client authentication
- [ ] Refresh token rotation enabled (one-time use)
- [ ] Token introspection endpoint is authenticated
- [ ] Revocation endpoint available and functional
- [ ] JWKS endpoint is HTTPS with proper caching headers
- [ ] Key rotation is automated (at least quarterly)
- [ ] Consent screen accurately describes requested scopes
- [ ] Device authorization flow secured (if used)

### Token Security

| Token Type | Requirement | Verification |
|-----------|-------------|-------------|
| Access token | Short lifetime (15 min recommended, 60 min max) | [ ] Verified |
| Refresh token | Bound to client, rotated on use | [ ] Verified |
| ID token | Audience validated, signature verified | [ ] Verified |
| Authorization code | Single use, short lifetime (10 min) | [ ] Verified |
| PKCE code verifier | S256 method used (not plain) | [ ] Verified |

### Token Validation Checklist

- [ ] Validate JWT signature using JWKS endpoint
- [ ] Validate `iss` (issuer) matches expected authorization server
- [ ] Validate `aud` (audience) matches this application's client ID
- [ ] Validate `exp` (expiration) is in the future
- [ ] Validate `nbf` (not before) is in the past
- [ ] Validate `iat` (issued at) is reasonable
- [ ] Validate `nonce` matches if provided in authentication request
- [ ] Validate `azp` (authorized party) if present
- [ ] Validate scopes/claims match expected values
- [ ] Reject tokens with algorithm `none`
- [ ] Reject tokens with unexpected algorithms (algorithm confusion)

## Session Management

### Session Security

- [ ] Session tokens are cryptographically random (128+ bits entropy)
- [ ] Session cookies use `Secure` flag (HTTPS only)
- [ ] Session cookies use `HttpOnly` flag (no JavaScript access)
- [ ] Session cookies use `SameSite=Lax` or `Strict`
- [ ] Session timeout configured (idle: 15-30 min, absolute: 8-12 hours)
- [ ] Session invalidated on logout (server-side)
- [ ] Session invalidated on password change
- [ ] Concurrent session limit enforced (where appropriate)
- [ ] Session fixation prevented (new session ID on authentication)
- [ ] Back-channel logout (OIDC) or SLO (SAML) implemented
- [ ] Session state stored server-side (not in client cookie)

### SSO Session Lifecycle

| Event | Required Action | Verified |
|-------|----------------|----------|
| Login | New session created, old session invalidated | [ ] |
| IdP session expiry | SP sessions re-authenticate | [ ] |
| User logout | All SP sessions terminated (SLO) | [ ] |
| Password change | All sessions invalidated | [ ] |
| Account disable | All sessions immediately terminated | [ ] |
| MFA step-up | Session upgraded, not new session | [ ] |
| Role change | Session permissions refreshed | [ ] |

## Federation Trust

### Trust Configuration

- [ ] Federation trust limited to specific, known IdPs
- [ ] Wildcard or open federation disabled
- [ ] Each federation trust has a documented business justification
- [ ] Federation trust owner assigned and reviewed quarterly
- [ ] IdP metadata is fetched over HTTPS with certificate validation
- [ ] IdP metadata refresh is automated but validated
- [ ] Cross-tenant/cross-domain claims are explicitly mapped
- [ ] No implicit trust inheritance (each SP explicitly configured)

### Federation Monitoring

| Monitor | Alert Condition | Severity |
|---------|----------------|----------|
| New federation trust created | Any new trust | High |
| Federation trust modified | Configuration change | Medium |
| Authentication from unexpected IdP | IdP not in allowlist | Critical |
| Token from expired/revoked certificate | Certificate validation failure | Critical |
| Unusual volume from federated IdP | >2x baseline | Medium |
| Failed federation authentication spike | >10 failures in 5 min | High |

## Operational Security

- [ ] SSO infrastructure is highly available (redundant IdP)
- [ ] Break-glass accounts exist that bypass SSO (for SSO outage)
- [ ] Break-glass procedure tested quarterly
- [ ] SSO audit logs are forwarded to SIEM
- [ ] Login/logout events are logged with source IP, user agent
- [ ] Failed authentication events are alerted on
- [ ] SSO configuration changes require change management
- [ ] Disaster recovery plan includes SSO infrastructure
- [ ] Service provider integration requests follow approval workflow
- [ ] Decommissioned SP trusts are removed promptly

## Cross-References

- [Identity Governance Framework](../../frameworks/identity-governance-framework.md) -- governance
- [MFA Implementation Checklist](mfa-implementation-checklist.md) -- MFA deployment
- [API Security Architecture](../../frameworks/api-security-architecture.md) -- OAuth for APIs
- [Directory Services Checklist](directory-services-checklist.md) -- AD/LDAP as IdP backend
