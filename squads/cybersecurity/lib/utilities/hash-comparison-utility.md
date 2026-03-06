# Hash Identification and Comparison Utility

## Purpose

Reference for identifying hash algorithms, comparing hashes for integrity verification, understanding known-hash databases, and recognizing collision risks for forensic analysis, password auditing, and file integrity monitoring.

## Hash Algorithm Identification

### By Length

| Length (chars) | Possible Algorithm | Hex Example |
|---------------|-------------------|-------------|
| 32 | MD5 | `d41d8cd98f00b204e9800998ecf8427e` |
| 40 | SHA-1 | `da39a3ee5e6b4b0d3255bfef95601890afd80709` |
| 56 | SHA-224 | `d14a028c2a3a2bc9476102bb288234c4...` |
| 64 | SHA-256 | `e3b0c44298fc1c149afbf4c8996fb924...` |
| 96 | SHA-384 | `38b060a751ac96384cd9327eb1b1e36a...` |
| 128 | SHA-512 | `cf83e1357eefb8bdf1542850d66d8007...` |
| 32 | NTLM | `31d6cfe0d16ae931b73c59d7e0c089c0` |
| 13 | DES crypt | `aafDCYqf0.M3o` |
| 34 | bcrypt | `$2b$12$WApznUPhDubN0oeveSXHru...` |
| Variable | Argon2 | `$argon2id$v=19$m=65536,t=3,p=4$...` |

### By Prefix

| Prefix | Algorithm |
|--------|-----------|
| `$1$` | MD5 crypt (Linux) |
| `$2a$`, `$2b$`, `$2y$` | bcrypt |
| `$5$` | SHA-256 crypt |
| `$6$` | SHA-512 crypt |
| `$argon2i$`, `$argon2id$` | Argon2 |
| `$pbkdf2-sha256$` | PBKDF2 |
| `$scrypt$` | scrypt |
| `{SSHA}` | Salted SHA-1 (LDAP) |
| `{SHA}` | SHA-1 (LDAP, unsalted) |

### Hash Identification Tools

```bash
# hashid
hashid 'd41d8cd98f00b204e9800998ecf8427e'
# Output: [+] MD5, [+] MD4, [+] NTLM, ...

# haiti
haiti 'd41d8cd98f00b204e9800998ecf8427e'
# Output: MD5 [HC: 0] [JtR: raw-md5]

# hashcat mode reference
hashcat --example-hashes | grep -A2 "MODE"

# john format reference
john --list=formats
```

## Common Hash Modes (Hashcat)

| Mode | Algorithm | Example Use |
|------|-----------|-------------|
| 0 | MD5 | Legacy application hashes |
| 100 | SHA-1 | Legacy applications |
| 1400 | SHA-256 | Modern applications (unsalted) |
| 1000 | NTLM | Windows password hashes |
| 3200 | bcrypt | Modern web applications |
| 5600 | NetNTLMv2 | Captured network authentication |
| 13100 | Kerberos TGS-REP (RC4) | Kerberoasting |
| 18200 | Kerberos AS-REP | AS-REP roasting |
| 22000 | WPA-PBKDF2 | WiFi password auditing |
| 1800 | SHA-512 crypt | Linux /etc/shadow |

## File Integrity Verification

### Generate Hashes

```bash
# Single file
md5sum file.bin
sha256sum file.bin
sha1sum file.bin

# Directory recursive
find /path -type f -exec sha256sum {} \; > baseline_hashes.txt

# Verify against baseline
sha256sum -c baseline_hashes.txt
```

### Forensic Hash Verification

```bash
# Create forensic image hash
dc3dd if=/dev/sda of=evidence.dd hash=sha256 log=hash.log

# Verify evidence integrity
sha256sum evidence.dd
# Compare with hash.log

# Multiple algorithms for added assurance
sha256sum evidence.dd && md5sum evidence.dd
```

## Known-Hash Databases

### Online Lookup Services

| Service | Description | Privacy Note |
|---------|-------------|-------------|
| VirusTotal | File hash reputation (malware analysis) | Uploads may be shared |
| NIST NSRL | National Software Reference Library (known good) | Government reference |
| Have I Been Pwned (API) | Breached password hashes (k-anonymity API) | Safe: sends only prefix |
| CrackStation | Precomputed hash lookup | Do not submit production hashes |

### Have I Been Pwned Password Check (Safe Pattern)

```python
import hashlib
import requests

def check_password_pwned(password):
    sha1 = hashlib.sha1(password.encode()).hexdigest().upper()
    prefix, suffix = sha1[:5], sha1[5:]
    response = requests.get(f'https://api.pwnedpasswords.com/range/{prefix}')
    for line in response.text.splitlines():
        hash_suffix, count = line.split(':')
        if hash_suffix == suffix:
            return int(count)  # Number of times seen in breaches
    return 0  # Not found in breaches
```

## Collision Awareness

### Algorithm Security Status

| Algorithm | Collision Resistance | Preimage Resistance | Recommendation |
|-----------|---------------------|--------------------|-|
| MD5 | BROKEN (2004) | Weakened | Do NOT use for security |
| SHA-1 | BROKEN (2017) | Weakened | Deprecate, migrate to SHA-256+ |
| SHA-256 | Secure | Secure | Recommended for general use |
| SHA-384 | Secure | Secure | Recommended for high security |
| SHA-512 | Secure | Secure | Recommended for high security |
| SHA-3 (Keccak) | Secure | Secure | Alternative to SHA-2 family |
| BLAKE2 | Secure | Secure | Fast, modern alternative |
| BLAKE3 | Secure | Secure | Fastest modern hash |

### Practical Collision Impact

| Scenario | Risk from MD5/SHA-1 Collision |
|----------|------------------------------|
| File integrity | Attacker can create different file with same hash |
| Code signing | Attacker can create malicious binary matching signed hash |
| Certificate forgery | CA using MD5 enables forged certificates (demonstrated 2008) |
| Digital forensics | Evidence integrity questionable if only MD5 |
| Password storage | Collision irrelevant (preimage resistance matters for passwords) |

## Quick Reference Commands

```bash
# Compare two files by hash
diff <(sha256sum file1.bin) <(sha256sum file2.bin)

# Hash a string (note: echo adds newline; use -n or printf)
echo -n "password" | sha256sum
printf "password" | sha256sum

# HMAC generation
echo -n "message" | openssl dgst -sha256 -hmac "secret_key"

# Base64 encoded hash
echo -n "data" | sha256sum | awk '{print $1}' | xxd -r -p | base64
```

## Cross-References

- See `lib/utilities/encoding-decoding-utility.md` for encoding/decoding operations
- See `lib/patterns/authentication-patterns.md` for password hashing in applications
- See `data/registries/file-signatures-registry.md` for file type identification
- See `frameworks/credential-attack-methodology.md` for hash cracking methodology
- See `reference/tools/ghidra-reference.md` for binary hash verification
