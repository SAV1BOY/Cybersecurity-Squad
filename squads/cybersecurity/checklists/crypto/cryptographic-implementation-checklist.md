# Cryptographic Implementation Checklist

## Purpose / When to Use

Execute this checklist when implementing, reviewing, or auditing cryptographic operations in any application or system. Cryptography fails silently -- a system can appear to work perfectly while providing zero actual security. This checklist catches the implementation errors that turn strong algorithms into false confidence.

## Prerequisites

- [ ] Threat model completed identifying what data needs protection and against which adversaries
- [ ] Regulatory requirements identified (FIPS 140-2/3, PCI DSS, HIPAA, GDPR encryption mandates)
- [ ] Development team has access to approved cryptographic libraries (no hand-rolled crypto)
- [ ] Code review process includes cryptographic review gate
- [ ] Key management infrastructure available or planned (`key-management-checklist.md`)

---

## Phase 1 -- Algorithm Selection

- [ ] Symmetric encryption uses approved algorithms only:
  - **Approved**: AES-256 (preferred), AES-128 (acceptable), ChaCha20-Poly1305
  - **Prohibited**: DES, 3DES (deprecated 2023), RC4, Blowfish, IDEA
- [ ] Asymmetric encryption uses approved algorithms and key sizes:
  - **Approved**: RSA >= 2048-bit (3072+ preferred), ECDSA/ECDH with P-256 or P-384, Ed25519/X25519
  - **Prohibited**: RSA < 2048-bit, DSA, ElGamal with small parameters
- [ ] Hashing uses approved functions:
  - **Approved**: SHA-256, SHA-384, SHA-512, SHA-3, BLAKE2
  - **Prohibited**: MD5, SHA-1 (except HMAC-SHA1 in legacy compatibility)
- [ ] Password hashing uses dedicated functions:
  - **Approved**: Argon2id (preferred), bcrypt (cost >= 12), scrypt
  - **Prohibited**: PBKDF2-SHA1 with low iterations, plain SHA/MD5, unsalted hashing
- [ ] Message authentication uses HMAC or AEAD:
  - **Approved**: HMAC-SHA256, AES-GCM (integrated), ChaCha20-Poly1305 (integrated)
  - **Prohibited**: CBC-MAC (unless part of CCM), custom MAC constructions
- [ ] Document algorithm choices with justification and expected deprecation timeline

## Phase 2 -- Mode of Operation

- [ ] Block cipher mode selection:
  - **Preferred**: GCM (provides confidentiality + integrity), CCM, SIV
  - **Acceptable**: CBC with separate HMAC (Encrypt-then-MAC order)
  - **Prohibited**: ECB (never), CBC without MAC, CTR without MAC, OFB, CFB
- [ ] If using GCM:
  - [ ] Nonce is exactly 96 bits (12 bytes) for optimal performance
  - [ ] Nonce is never reused with the same key (nonce reuse = catastrophic key recovery)
  - [ ] Authentication tag length is at least 128 bits
  - [ ] Plaintext limit per key-nonce pair is respected (2^39 - 256 bits max)
- [ ] If using CBC:
  - [ ] IV is randomly generated for each encryption operation
  - [ ] MAC is applied AFTER encryption (Encrypt-then-MAC)
  - [ ] Padding oracle vulnerabilities are mitigated (constant-time padding validation)
- [ ] Streaming data uses appropriate stream cipher or CTR mode with proper nonce handling
- [ ] Verify no mode downgrade is possible (attacker cannot force ECB or other weak mode)

## Phase 3 -- IV / Nonce Handling

- [ ] IVs and nonces are generated using cryptographically secure random number generator
  ```python
  # Python: correct
  import os; nonce = os.urandom(12)
  # Python: WRONG
  import random; nonce = random.randbytes(12)  # Not cryptographic
  ```
- [ ] IV/nonce uniqueness is guaranteed per key:
  - Random generation with sufficient length (>= 96 bits gives negligible collision probability for < 2^32 messages)
  - Counter-based nonce with persistent state (if random is not suitable)
  - SIV mode for nonce-misuse resistance in high-risk scenarios
- [ ] IV/nonce is transmitted with ciphertext (typically prepended) -- it is not secret
- [ ] No IV/nonce is derived from predictable values (timestamps, counters without CSPRNG, sequential IDs)
- [ ] For database field encryption: verify nonce is unique per row update, not per row creation
- [ ] Document nonce generation strategy and collision probability analysis

## Phase 4 -- Padding

- [ ] If using a mode that requires padding (CBC):
  - [ ] PKCS#7 padding is used (standard, well-supported)
  - [ ] Padding validation is constant-time to prevent padding oracle attacks
  - [ ] Padding errors are indistinguishable from MAC errors in error responses
- [ ] If using AEAD mode (GCM, CCM): no padding is needed -- confirm no superfluous padding is added
- [ ] For RSA encryption:
  - [ ] OAEP padding is used (PKCS#1 v2.x)
  - [ ] PKCS#1 v1.5 padding is NOT used (Bleichenbacher attack)
- [ ] For RSA signatures:
  - [ ] PSS padding is used (preferred)
  - [ ] PKCS#1 v1.5 signature padding is acceptable but PSS is recommended
- [ ] Verify no null/zero padding is used for any cryptographic operation

## Phase 5 -- Key Derivation

- [ ] Keys are never used directly from passwords -- always use a KDF:
  ```python
  # Correct: Argon2id for password-based key derivation
  from argon2 import PasswordHasher
  # For key derivation from high-entropy input
  from cryptography.hazmat.primitives.kdf.hkdf import HKDF
  ```
- [ ] Password-based KDF parameters meet minimums:
  - Argon2id: memory >= 64MB, iterations >= 3, parallelism >= 4
  - bcrypt: cost factor >= 12
  - scrypt: N >= 2^15, r >= 8, p >= 1
  - PBKDF2 (if mandated): iterations >= 600,000 for SHA-256
- [ ] Key derivation from shared secrets uses HKDF with proper info/context parameters
- [ ] Salt is unique per derivation (>= 128 bits, randomly generated)
- [ ] Derived keys are of appropriate length for the target algorithm (256 bits for AES-256)
- [ ] Key derivation is deterministic only when required (same input always produces same key)

## Phase 6 -- Library Selection and Usage

- [ ] Cryptographic library is well-maintained, widely reviewed, and actively supported:
  - **Recommended**: libsodium/NaCl, OpenSSL (>= 3.x), BoringSSL, Bouncy Castle, Go crypto/stdlib
  - **Acceptable**: Python cryptography (pyca), Web Crypto API (browser), .NET System.Security.Cryptography
  - **Prohibited**: Custom implementations, abandoned libraries, educational-only libraries
- [ ] Library version is current with no known CVEs
- [ ] Library is used through high-level APIs where available (not raw primitives)
  ```python
  # Preferred: high-level Fernet (authenticated encryption)
  from cryptography.fernet import Fernet
  # Acceptable: explicit AEAD construction
  from cryptography.hazmat.primitives.ciphers.aead import AESGCM
  # Risky: raw cipher primitives (requires expert knowledge)
  from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
  ```
- [ ] Error handling does not leak cryptographic state (no detailed error messages about padding, MAC, or decryption)
- [ ] Cryptographic operations use constant-time comparison for MAC/signature verification
  ```python
  import hmac
  hmac.compare_digest(expected_mac, computed_mac)  # Correct
  expected_mac == computed_mac  # WRONG: timing side-channel
  ```
- [ ] Memory containing keys is zeroized after use where language permits
- [ ] FIPS mode is enabled if regulatory requirement applies

## Phase 7 -- Implementation Verification

- [ ] Test vectors from NIST/RFC are used to validate implementation correctness
- [ ] Known-answer tests (KATs) are included in the test suite
- [ ] Negative tests verify that:
  - Tampered ciphertext fails authentication
  - Wrong key fails decryption
  - Invalid padding is rejected
  - Truncated data is handled safely
- [ ] Interoperability tested: encrypted by implementation A, decrypted by implementation B
- [ ] Performance tested under expected load (crypto operations can be CPU-bottleneck)
- [ ] Code review performed by someone with cryptographic expertise
- [ ] Static analysis scan for crypto misuse patterns (e.g., Semgrep crypto rules, CryptoGuard)

---

## Cross-References

- TLS/SSL audit: `checklists/crypto/tls-ssl-audit-checklist.md`
- Key management: `checklists/crypto/key-management-checklist.md`
- Crypto vulnerability assessment: `checklists/crypto/crypto-vulnerability-assessment-checklist.md`
- Secure coding review: `checklists/manico/manico-secure-coding-review.md`
- NIST SP 800-175B: Guideline for Using Cryptographic Standards
- NIST SP 800-131A: Transitioning the Use of Cryptographic Algorithms
