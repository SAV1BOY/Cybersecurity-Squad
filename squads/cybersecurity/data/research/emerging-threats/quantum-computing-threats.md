# Post-Quantum Cryptography Threats

## Purpose

Research reference on quantum computing threats to current cryptographic systems. Covers the harvest-now-decrypt-later threat, NIST post-quantum cryptography standards, migration planning, and timeline assessment for organizational quantum readiness.

## Quantum Threat to Cryptography

### Algorithms at Risk

| Algorithm | Type | Quantum Attack | Impact |
|-----------|------|---------------|--------|
| RSA (all key sizes) | Asymmetric | Shor's algorithm | Completely broken |
| ECC (ECDSA, ECDH) | Asymmetric | Shor's algorithm | Completely broken |
| Diffie-Hellman | Key exchange | Shor's algorithm | Completely broken |
| DSA | Digital signature | Shor's algorithm | Completely broken |
| AES-128 | Symmetric | Grover's algorithm | Weakened to 64-bit (upgrade to AES-256) |
| AES-256 | Symmetric | Grover's algorithm | Reduced to 128-bit (still secure) |
| SHA-256 | Hash | Grover's algorithm | Reduced to 128-bit (still secure) |
| SHA-3 | Hash | Grover's algorithm | Reduced but still secure |

### Impact Summary

- **Asymmetric cryptography**: Fundamentally broken by quantum computers
- **Symmetric cryptography**: Weakened but survivable by doubling key sizes
- **Hash functions**: Weakened but survivable with longer outputs

## Harvest Now, Decrypt Later (HNDL)

### Threat Model

```
Today (pre-quantum):
  Adversary intercepts and stores encrypted communications
  Data remains confidential (classical computers cannot break encryption)

Future (post-quantum):
  Adversary uses quantum computer to break stored encryption
  All historically captured data becomes readable

Risk window = Data sensitivity lifetime - Time until quantum computers
```

### Data at Risk Assessment

| Data Type | Sensitivity Lifetime | HNDL Risk Level |
|-----------|---------------------|-----------------|
| Military/intelligence secrets | 25-75 years | CRITICAL |
| Trade secrets | 5-20 years | HIGH |
| Personal health records | Patient's lifetime | HIGH |
| Financial records | 7-10 years | MEDIUM |
| Authentication credentials | Until rotated | LOW (if rotated regularly) |
| Public website content | None | NONE |

### Who is Harvesting Now?

Nation-state adversaries with the resources and patience to:
1. Tap undersea cables and internet exchange points
2. Compromise VPN concentrators for bulk traffic capture
3. Store petabytes of encrypted traffic for future decryption
4. Target diplomatic, military, and industrial communications

## NIST Post-Quantum Cryptography Standards

### FIPS 203: ML-KEM (Module-Lattice-Based Key Encapsulation)

| Parameter Set | Security Level | Public Key Size | Ciphertext Size |
|--------------|---------------|----------------|-----------------|
| ML-KEM-512 | NIST Level 1 (AES-128 equivalent) | 800 bytes | 768 bytes |
| ML-KEM-768 | NIST Level 3 (AES-192 equivalent) | 1,184 bytes | 1,088 bytes |
| ML-KEM-1024 | NIST Level 5 (AES-256 equivalent) | 1,568 bytes | 1,568 bytes |

Use case: TLS key exchange, VPN, encrypted messaging

### FIPS 204: ML-DSA (Module-Lattice-Based Digital Signature)

| Parameter Set | Security Level | Public Key Size | Signature Size |
|--------------|---------------|----------------|---------------|
| ML-DSA-44 | Level 2 | 1,312 bytes | 2,420 bytes |
| ML-DSA-65 | Level 3 | 1,952 bytes | 3,309 bytes |
| ML-DSA-87 | Level 5 | 2,592 bytes | 4,627 bytes |

Use case: Code signing, document signing, certificate signatures

### FIPS 205: SLH-DSA (Stateless Hash-Based Digital Signature)

- Based on hash functions (conservative, well-understood security)
- Larger signatures than ML-DSA but simpler security assumptions
- Use case: Root CA certificates, firmware signing, high-assurance applications

### Size Comparison with Classical Algorithms

| Algorithm | Public Key | Signature/Ciphertext |
|-----------|-----------|---------------------|
| RSA-2048 | 256 bytes | 256 bytes |
| ECDSA P-256 | 64 bytes | 64 bytes |
| ML-KEM-768 | 1,184 bytes | 1,088 bytes |
| ML-DSA-65 | 1,952 bytes | 3,309 bytes |

**Impact**: Larger keys and signatures affect bandwidth, storage, and handshake performance. TLS handshakes will be larger; certificate chains will be bigger.

## Migration Planning

### Crypto Agility Assessment

```
1. Inventory Phase
   - Identify all cryptographic usage (libraries, protocols, certificates)
   - Map data flows that rely on asymmetric crypto
   - Identify hardcoded algorithms vs. configurable
   - Assess vendor PQC roadmaps

2. Risk Assessment Phase
   - Classify data by sensitivity lifetime
   - Identify HNDL-vulnerable communications
   - Prioritize: long-sensitivity data on public networks = highest risk

3. Preparation Phase
   - Implement crypto-agility (ability to swap algorithms)
   - Begin hybrid mode testing (classical + PQC)
   - Update procurement requirements to include PQC readiness
   - Train development and operations teams

4. Migration Phase
   - Deploy hybrid mode (e.g., X25519 + ML-KEM-768 for TLS)
   - Migrate highest-risk systems first
   - Update certificates with PQC algorithms
   - Verify interoperability with partners

5. Completion Phase
   - Phase out classical-only asymmetric crypto
   - Continuous monitoring for PQC implementation vulnerabilities
   - Maintain crypto agility for future algorithm changes
```

### Hybrid Approach

During transition, use both classical and post-quantum algorithms simultaneously:

```
TLS 1.3 with hybrid key exchange:
  Classical: X25519 (ECDH)
  Post-quantum: ML-KEM-768
  Combined: Both must be broken to compromise the session
```

### Timeline Estimates

| Milestone | Estimated Timeline |
|-----------|-------------------|
| NIST standards finalized | 2024 (complete) |
| Library support mainstream | 2025-2026 |
| Browser/OS support | 2025-2027 |
| Enterprise migration begins | 2026-2028 |
| Cryptographically relevant quantum computer | 2030-2040 (uncertain) |
| Classical crypto fully deprecated | 2035+ |

## Organizational Actions (Start Now)

1. **Inventory cryptographic assets**: Know what algorithms you use and where
2. **Assess data sensitivity lifetimes**: Identify HNDL-vulnerable data
3. **Require crypto agility**: All new systems must support algorithm swapping
4. **Monitor vendor roadmaps**: Ensure suppliers plan for PQC migration
5. **Test PQC in labs**: Begin testing performance and compatibility
6. **Update procurement language**: Require PQC readiness in RFPs

## Cross-References

- See `data/research/emerging-threats/supply-chain-evolution.md` for cryptographic supply chain risk
- See `lib/patterns/authentication-patterns.md` for authentication algorithm selection
- See `lib/patterns/secrets-management-patterns.md` for key management evolution
- See `reference/industries/government-security.md` for government PQC mandates
- See `reference/industries/financial-services-security.md` for financial sector cryptographic requirements
