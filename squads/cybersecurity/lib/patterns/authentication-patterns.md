# Secure Authentication Patterns

## Purpose

Reference patterns for implementing secure authentication. Covers password hashing algorithms, multi-factor authentication, session management, token handling, and phishing-resistant authentication for application developers and security architects.

## Password Hashing

### Algorithm Selection

| Algorithm | Recommendation | Parameters |
|-----------|---------------|------------|
| Argon2id | Preferred (winner of PHC) | Memory: 64MB, Iterations: 3, Parallelism: 4 |
| bcrypt | Acceptable | Cost factor: 12+ (adjusts every 2 years) |
| scrypt | Acceptable | N=2^17, r=8, p=1 |
| PBKDF2-HMAC-SHA256 | Legacy acceptable | Iterations: 600,000+ (OWASP 2023) |
| MD5, SHA-1, SHA-256 (unsalted) | NEVER | Not a password hash |

### Implementation Pattern

```python
# Argon2id (Python example)
from argon2 import PasswordHasher
ph = PasswordHasher(
    time_cost=3,        # iterations
    memory_cost=65536,  # 64 MB
    parallelism=4,
    hash_len=32,
    salt_len=16
)
hash = ph.hash(password)
# Verify
try:
    ph.verify(hash, password)
    if ph.check_needs_rehash(hash):
        new_hash = ph.hash(password)  # Upgrade hash parameters
except VerifyMismatchError:
    # Invalid password
```

### Password Policy (NIST 800-63B Aligned)

| Rule | Requirement |
|------|-------------|
| Minimum length | 8 characters (15+ for privileged accounts) |
| Maximum length | At least 64 characters |
| Composition rules | DO NOT require special characters or complexity |
| Breached password check | Check against known compromised password databases |
| Rotation | DO NOT force periodic rotation unless compromise suspected |
| Storage | Hashed with memory-hard algorithm |

## Multi-Factor Authentication (MFA)

### Factor Types

| Factor | Type | Strength |
|--------|------|----------|
| Password | Something you know | Weak (phishable, replayable) |
| SMS OTP | Something you have | Weak (SIM swap, SS7 interception) |
| TOTP (Authenticator app) | Something you have | Medium (phishable, but better than SMS) |
| Push notification | Something you have | Medium (MFA fatigue attacks possible) |
| FIDO2/WebAuthn (hardware key) | Something you have | Strong (phishing-resistant) |
| Passkeys | Something you have + biometric | Strong (phishing-resistant) |
| Biometric | Something you are | Medium (supplement, not sole factor) |

### Phishing-Resistant MFA

```
Phishing-Resistant means:
1. Cryptographic binding to the origin (FIDO2 checks the domain)
2. No shared secret that could be intercepted in transit
3. Resistant to real-time phishing proxies (adversary-in-the-middle)

FIDO2/WebAuthn flow:
1. User initiates login at https://example.com
2. Server sends challenge with its origin (example.com)
3. Authenticator verifies the origin matches registered domain
4. Authenticator signs challenge with private key
5. Server verifies signature with stored public key

Phishing site at evil.com cannot obtain a valid signature for example.com
```

### MFA Bypass Threats and Mitigations

| Attack | Mitigation |
|--------|-----------|
| MFA fatigue (push spam) | Number matching, rate limiting, user alerting |
| SIM swap | FIDO2 instead of SMS; carrier PIN protection |
| Adversary-in-the-middle | FIDO2/WebAuthn (origin-bound) |
| Session hijacking post-MFA | Token binding, continuous authentication |
| Social engineering helpdesk | Identity verification procedures for MFA reset |

## Session Management

### Secure Session Configuration

| Parameter | Recommendation |
|-----------|---------------|
| Session ID length | Minimum 128 bits of entropy |
| Session ID generation | CSPRNG (cryptographically secure random) |
| Cookie attributes | `Secure; HttpOnly; SameSite=Lax` (or Strict) |
| Session timeout (idle) | 15-30 minutes for sensitive apps |
| Session timeout (absolute) | 8-24 hours maximum |
| Session regeneration | On privilege change (login, role change) |
| Concurrent sessions | Limit per user, alert on anomaly |

### Session Lifecycle

```
1. Pre-Authentication
   - Generate session ID on first request
   - Do NOT store sensitive data before auth

2. Authentication
   - Validate credentials
   - REGENERATE session ID (prevent session fixation)
   - Bind session to user context
   - Set secure cookie attributes

3. Active Session
   - Validate session on every request
   - Check session freshness for sensitive operations
   - Step-up authentication for high-risk actions

4. Termination
   - Invalidate session server-side on logout
   - Clear session cookie
   - Invalidate on password change (all other sessions)
   - Invalidate on detected compromise
```

## Token Handling (JWT)

### JWT Security Rules

| Rule | Implementation |
|------|---------------|
| Algorithm | Use RS256 or ES256; NEVER allow "none" or HS256 with public key confusion |
| Validation | Always validate signature, expiration, issuer, audience |
| Storage | HttpOnly cookies preferred; if localStorage, protect against XSS |
| Expiration | Short-lived access tokens (5-15 min); longer refresh tokens |
| Refresh token | Server-side storage, rotation on use, family detection |
| Revocation | Token blacklist or short expiry + refresh rotation |
| Claims | Minimum necessary; no sensitive data in payload |

### JWT Validation Checklist

```
1. Verify signature using the expected algorithm
2. Reject tokens with "alg":"none"
3. Verify "exp" claim is in the future
4. Verify "nbf" claim is in the past (if present)
5. Verify "iss" matches expected issuer
6. Verify "aud" matches your application
7. Verify "sub" matches the expected user context
8. Check token against revocation list (if applicable)
```

## Account Security Features

| Feature | Implementation |
|---------|---------------|
| Account lockout | Temporary lockout after 5-10 failed attempts; exponential backoff |
| Rate limiting | Per-IP and per-account; graduated response |
| Credential stuffing protection | CAPTCHA after N failures, device fingerprinting |
| Account recovery | Out-of-band verification; avoid security questions |
| Login notification | Alert on new device/location/IP |
| Active session management | Show active sessions; allow remote termination |

## Cross-References

- See `lib/patterns/authorization-patterns.md` for post-authentication access control
- See `lib/patterns/secrets-management-patterns.md` for credential storage infrastructure
- See `reference/industries/government-security.md` for phishing-resistant MFA mandates
- See `frameworks/identity-layer.md` for identity security methodology
- See `data/registries/http-status-codes-security.md` for auth response handling
