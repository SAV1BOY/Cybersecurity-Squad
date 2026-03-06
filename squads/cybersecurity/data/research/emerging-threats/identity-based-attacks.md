# Identity-Based Attack Evolution

## Purpose

Research reference on the evolution of identity-focused attacks. Covers token theft, session hijacking, OAuth abuse, SSO exploitation, and defensive strategies for protecting identity infrastructure as the new perimeter.

## The Identity Perimeter

### Why Identity is the Primary Target

```
Traditional perimeter: Firewall protects internal network
  -> VPN/remote work eliminated this boundary

Zero trust perimeter: Identity verification on every request
  -> Identity becomes the new firewall
  -> Compromising identity = bypassing all controls
  -> Identity attacks are now the most impactful attack vector
```

### Attack Surface Map

| Component | Attack Vectors | Impact |
|-----------|---------------|--------|
| Passwords | Phishing, credential stuffing, brute force | Account takeover |
| MFA | Fatigue, SIM swap, AitM proxy | MFA bypass |
| SSO tokens | Token theft, session hijacking | Access to all SSO-connected apps |
| OAuth tokens | Token interception, consent phishing | API access, data exfiltration |
| Service accounts | Overprivileged, never rotated | Persistent access |
| API keys | Leaked in code, logs, config | Unauthorized API access |
| Certificates | Stolen, expired, misconfigured | Impersonation |
| Federated identity | Trust abuse, SAML manipulation | Cross-organization compromise |

## Token Theft Techniques

### Primary Access Token (Session Cookie/JWT)

| Technique | Description | Mitigation |
|-----------|-------------|-----------|
| AitM phishing proxy | Real-time relay steals session token post-MFA | FIDO2/WebAuthn (origin-bound) |
| Browser credential theft | Infostealer malware extracts browser cookies | EDR, browser isolation |
| Pass-the-Cookie | Stolen cookie replayed from attacker's browser | Token binding, device attestation |
| Token from memory dump | Extract tokens from process memory | Memory protection, short token TTL |
| XSS token exfiltration | JavaScript steals tokens from browser | HttpOnly cookies, CSP |

### Adversary-in-the-Middle (AitM) Phishing

```
Attack flow:
1. Attacker creates phishing page proxying real login (Evilginx, Modlishka)
2. User visits phishing page, enters credentials
3. Proxy forwards to real IdP, captures MFA challenge
4. User completes MFA on phishing page
5. Proxy captures session token from IdP response
6. Attacker uses stolen session token (MFA already completed)

This defeats:
  - SMS OTP
  - TOTP (authenticator apps)
  - Push notifications

This does NOT defeat:
  - FIDO2/WebAuthn (cryptographically bound to origin)
  - Passkeys (same origin binding)
  - Certificate-based authentication
```

## Session Hijacking Evolution

### Post-Authentication Session Attacks

| Attack | Vector | Detection |
|--------|--------|-----------|
| Cookie replay | Stolen cookies used from different device/IP | Device fingerprint change, IP anomaly |
| Session fixation | Attacker sets session ID before authentication | Session regeneration on login |
| Token exchange abuse | Refresh token stolen for new access tokens | Refresh token rotation, family detection |
| Browser profile export | Full browser profile stolen by malware | Behavioral analytics on session usage |
| Memory scraping | Tokens extracted from application memory | Process protection, short-lived tokens |

### Continuous Access Evaluation

```
Traditional: Authenticate once -> session valid until expiry
Modern (CAE): Continuous validation of session context

Evaluate on every request (or frequent intervals):
  - Source IP: Has it changed significantly?
  - Device: Is the device still compliant?
  - User risk: Has risk score changed?
  - Resource sensitivity: Does this access require re-evaluation?
  - Time: Has the session been idle too long?

Microsoft CAE implementation:
  - Critical event evaluation (password change, user disable)
  - Claims challenge (re-evaluate on policy change)
  - Token lifetime enforcement (1-hour max without CAE)
```

## OAuth and OIDC Abuse

### OAuth Attack Patterns

| Attack | Description | Mitigation |
|--------|-------------|-----------|
| Consent phishing | Attacker creates malicious OAuth app, requests broad permissions | Consent review, app governance |
| Redirect URI manipulation | Intercept authorization code via open redirect | Exact redirect URI matching |
| Authorization code interception | Steal code from URL parameters | PKCE enforcement |
| Scope escalation | Request more permissions than needed | Minimal scope enforcement |
| Client credential theft | Stolen client_secret used for API access | Short-lived credentials, certificate auth |
| Token exchange abuse | Abuse on-behalf-of flow for privilege escalation | Strict audience validation |
| Device code phishing | Trick user into authorizing attacker's device code | User education, conditional access |

### OAuth Security Best Practices

```
1. Enforce PKCE on ALL OAuth flows (not just public clients)
2. Use exact redirect URI matching (no wildcards)
3. Short-lived authorization codes (< 60 seconds)
4. Rotate refresh tokens on every use
5. Implement refresh token family detection (revoke entire family on reuse)
6. Restrict token scope to minimum necessary
7. Validate audience (aud) claim in all token validations
8. Monitor OAuth consent grants for anomalies
9. Periodically review granted permissions across all apps
```

## SSO Exploitation

### SAML Attacks

| Attack | Description |
|--------|-------------|
| Golden SAML | Forge SAML assertions using stolen signing certificate |
| SAML injection | Manipulate assertion attributes (e.g., change role) |
| XML Signature Wrapping | Move signature to cover different assertion |
| Replay attack | Reuse valid SAML assertion |
| IdP impersonation | Compromise IdP to issue arbitrary assertions |

### SSO-Specific Risks

```
Single point of compromise:
  SSO compromise = Access to ALL connected applications

Risk amplification:
  1. Compromise IdP (Okta, Azure AD, Ping)
  2. Mint tokens for any connected application
  3. Access all SaaS apps, internal tools, cloud consoles
  4. Pivot across the entire organization

Defensive priority:
  - IdP is the MOST critical infrastructure to protect
  - MFA on IdP must be phishing-resistant (FIDO2)
  - IdP admin access requires strongest controls
  - Monitor IdP logs for anomalous authentication patterns
```

## Service Account and Non-Human Identity Attacks

### Non-Human Identity Risk

| Risk | Prevalence | Impact |
|------|-----------|--------|
| Overprivileged service accounts | Very common | Broad access if compromised |
| Never-rotated API keys | Very common | Persistent access |
| Shared service accounts | Common | No accountability |
| Orphaned accounts (employees left) | Common | Unmonitored persistent access |
| Embedded credentials in code | Common | Source code exposure = compromise |
| Machine-to-machine tokens without expiry | Common | Permanent access if stolen |

### Non-Human Identity Security Program

1. Inventory all non-human identities (service accounts, API keys, certificates)
2. Assign ownership to each identity
3. Apply least privilege (scope to specific resources and actions)
4. Implement expiration and rotation for all credentials
5. Monitor usage patterns and alert on anomalies
6. Automate lifecycle management (provisioning, rotation, deprovisioning)
7. Regular attestation reviews (quarterly minimum)

## Cross-References

- See `lib/patterns/authentication-patterns.md` for phishing-resistant authentication
- See `lib/patterns/authorization-patterns.md` for access control post-authentication
- See `frameworks/identity-layer.md` for identity security methodology
- See `frameworks/credential-attack-methodology.md` for credential attack techniques
- See `data/research/emerging-threats/ai-powered-attacks.md` for AI-enhanced identity attacks
