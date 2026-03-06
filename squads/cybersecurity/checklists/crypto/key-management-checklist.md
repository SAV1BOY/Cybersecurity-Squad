# Key Management Lifecycle Checklist

## Purpose / When to Use

Execute this checklist when establishing, auditing, or improving cryptographic key management practices. Key management is where cryptography meets operations -- the strongest algorithm provides zero security if keys are poorly generated, improperly stored, never rotated, or impossible to revoke. This checklist covers the complete key lifecycle from generation through destruction.

## Prerequisites

- [ ] Cryptographic inventory completed: all systems, algorithms, and key types cataloged
- [ ] Data classification scheme in place (determines key protection requirements)
- [ ] Regulatory requirements identified (PCI DSS, HIPAA, FIPS 140-2/3, eIDAS)
- [ ] Budget and infrastructure assessed for HSM or cloud KMS adoption
- [ ] Key management policy document drafted or available for review

---

## Phase 1 -- Key Generation

- [ ] Keys are generated using cryptographically secure random number generators (CSPRNG):
  - `/dev/urandom` (Linux), `BCryptGenRandom` (Windows), hardware RNG (HSM)
  - Never: `Math.random()`, `random.random()`, predictable seeds, system time
- [ ] Key generation occurs in a secure environment:
  - HSM (FIPS 140-2 Level 3+) for high-value keys (CA roots, master keys, signing keys)
  - Cloud KMS (AWS KMS, Azure Key Vault, GCP Cloud KMS) for application keys
  - Secure workstation for lower-sensitivity keys
- [ ] Key length meets or exceeds requirements:
  | Algorithm | Minimum | Recommended | Equivalent Security |
  |-----------|---------|-------------|-------------------|
  | AES | 128-bit | 256-bit | 128/256-bit |
  | RSA | 2048-bit | 3072-bit | 112/128-bit |
  | ECDSA | P-256 | P-384 | 128/192-bit |
  | Ed25519 | 256-bit | 256-bit | 128-bit |
- [ ] Key generation ceremony documented for high-value keys:
  - Witnesses present, roles defined
  - Split knowledge / dual control enforced
  - Ceremony script followed step-by-step
  - Artifacts (key shares, recovery materials) distributed to custodians
- [ ] Generated keys are immediately protected (never written to disk in plaintext)
- [ ] Key metadata recorded: algorithm, length, purpose, owner, generation date, expiration date

## Phase 2 -- Key Storage

- [ ] Keys at rest are encrypted (key-wrapping or envelope encryption):
  ```
  Data Encryption Key (DEK) encrypts data
  Key Encryption Key (KEK) encrypts DEK
  Master Key (in HSM) encrypts KEK
  ```
- [ ] Storage location meets security requirements:
  - **HSM**: root CA keys, master keys, signing keys, payment keys
  - **Cloud KMS**: application encryption keys, TLS private keys
  - **Secrets manager** (Vault, AWS Secrets Manager): API keys, database credentials
  - **Never**: source code, configuration files, environment variables (for long-term keys), shared drives
- [ ] Access to key material is restricted by role:
  - Developers: can use keys via API, cannot extract key material
  - Operations: can manage key lifecycle, cannot use keys for encryption
  - Security: can audit key usage, can authorize key operations
- [ ] Key access is logged and auditable (who accessed which key, when, for what operation)
- [ ] Backup of encrypted key material exists in geographically separate location
- [ ] Key storage systems are included in vulnerability management and patching programs
- [ ] File permissions on any key files are restrictive:
  ```bash
  chmod 600 /etc/ssl/private/server.key
  chown root:root /etc/ssl/private/server.key
  ```

## Phase 3 -- Key Rotation

- [ ] Rotation schedule defined per key type:
  | Key Type | Rotation Frequency | Trigger |
  |----------|-------------------|---------|
  | TLS certificates | 90 days (Let's Encrypt) to 1 year | Automated |
  | Application encryption keys | 1 year | Automated |
  | Database encryption keys | 1 year | Scheduled |
  | Signing keys | 2 years | Scheduled |
  | Master/root keys | 3-5 years | Ceremony |
  | SSH keys | 1 year | Scheduled |
  | API keys | 90 days | Automated |
- [ ] Rotation process is automated where possible:
  ```bash
  # Example: automated certificate rotation with certbot
  certbot renew --deploy-hook "systemctl reload nginx"
  ```
- [ ] Rotation maintains backward compatibility:
  - New key encrypts new data
  - Old key remains available for decrypting historical data (grace period)
  - Re-encryption of historical data scheduled if required
- [ ] Rotation does not cause service disruption (blue-green key deployment)
- [ ] Post-rotation validation confirms new key is operational
- [ ] Old key version is retained for the defined grace period, then scheduled for destruction

## Phase 4 -- Key Distribution

- [ ] Keys are distributed through secure channels only:
  - HSM-to-HSM: secure key transport protocol (PKCS#11, key wrapping)
  - Cloud: KMS API with IAM authentication and TLS
  - Manual: split knowledge with separate channels per share
  - Never: email, chat, shared drives, unencrypted FTP
- [ ] Key distribution uses envelope encryption (key wrapped by transport key)
- [ ] Recipients are authenticated before key delivery
- [ ] Key distribution is logged with sender, recipient, key identifier, and timestamp
- [ ] For TLS certificates: private key is generated on the target system (CSR model) rather than generated centrally and transported
- [ ] Temporary keys used for distribution are destroyed after successful delivery

## Phase 5 -- Key Revocation

- [ ] Revocation procedures are documented and tested for each key type:
  - TLS certificates: CRL publication and OCSP responder update
  - Code signing: certificate revocation and re-signing with new key
  - Encryption keys: transition to new key, re-encrypt data
  - Authentication keys: remove from authorized_keys, revoke tokens
- [ ] Revocation triggers are defined:
  - Known or suspected key compromise
  - Personnel change (key custodian leaves organization)
  - Algorithm or key length deprecation
  - End of key validity period
  - System decommissioning
- [ ] Revocation can be executed within defined SLA:
  - Critical compromise: within 1 hour
  - Suspected compromise: within 24 hours
  - Planned revocation: within 1 week
- [ ] Revocation status is propagated to all relying parties:
  - CRL distribution points are accessible and updated
  - OCSP responders reflect current revocation status
  - Key blacklists are distributed to all consuming systems
- [ ] Revoked keys cannot be reactivated without explicit authorization

## Phase 6 -- HSM Usage

- [ ] HSM is used for highest-value key operations:
  - Certificate Authority signing
  - Master key storage
  - Payment transaction processing (PCI HSM requirements)
  - Code signing
  - DNSSEC key management
- [ ] HSM is FIPS 140-2 Level 3 certified (minimum) or Level 4 for highest security
- [ ] HSM firmware is current and vendor-supported
- [ ] HSM access requires multi-factor authentication
- [ ] HSM admin roles implement separation of duties:
  - Security Officer: initialize HSM, manage policies
  - Operator: perform key operations within policy
  - Auditor: review logs, cannot perform operations
- [ ] HSM audit logs are forwarded to SIEM and reviewed regularly
- [ ] HSM high-availability and disaster recovery tested (clustered HSMs, key backup)
- [ ] HSM network isolation enforced (dedicated management VLAN)

## Phase 7 -- Key Escrow and Disaster Recovery

- [ ] Key escrow policy defined: which keys are escrowed, where, and under what conditions
- [ ] Escrow storage is physically and logically separate from primary key storage
- [ ] Escrow access requires multi-party authorization (M-of-N threshold)
- [ ] Escrow recovery procedure is documented and tested annually:
  - [ ] Contact information for key custodians is current
  - [ ] Recovery hardware/software is available and functional
  - [ ] Recovery time objective (RTO) is defined and achievable
- [ ] Disaster recovery scenarios addressed:
  - HSM failure: backup HSM or cloud failover
  - Data center loss: geographically replicated key material
  - Key custodian unavailability: sufficient M-of-N threshold with alternates
  - Total key loss: documented impact and recovery procedure
- [ ] Crypto-shredding capability: ability to destroy all copies of a key to render data irrecoverable (data deletion compliance)
- [ ] Annual DR test includes cryptographic key recovery exercise

## Phase 8 -- Audit and Compliance

- [ ] Complete cryptographic inventory maintained:
  - Key identifier, algorithm, length, purpose, owner
  - Generation date, expiration date, last rotation date
  - Storage location, access controls, backup status
- [ ] Key usage logs reviewed monthly for anomalies:
  - Unusual access patterns or times
  - Failed access attempts
  - Key operations by unauthorized roles
- [ ] Compliance validation:
  - PCI DSS: Requirement 3.5-3.7 (key management)
  - FIPS 140-2/3: validated modules for federal systems
  - HIPAA: encryption of PHI at rest and in transit
  - GDPR: encryption as technical safeguard, crypto-shredding for right to erasure
- [ ] Key management procedures are reviewed and updated annually
- [ ] Penetration testing includes attempts to extract key material

---

## Cross-References

- Cryptographic implementation: `checklists/crypto/cryptographic-implementation-checklist.md`
- TLS/SSL audit: `checklists/crypto/tls-ssl-audit-checklist.md`
- Crypto vulnerability assessment: `checklists/crypto/crypto-vulnerability-assessment-checklist.md`
- Secrets management: `checklists/appsec/appsec-secrets-management.md`
- NIST SP 800-57: Recommendation for Key Management
- NIST SP 800-130: Framework for Designing Key Management Systems
