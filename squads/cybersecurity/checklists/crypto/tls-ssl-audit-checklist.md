# TLS/SSL Audit Checklist

## Purpose / When to Use

Execute this checklist when auditing TLS/SSL configurations on web servers, APIs, mail servers, VPN gateways, or any service using TLS for transport encryption. Misconfigured TLS is one of the most common findings in security assessments and a frequent vector for data interception. This checklist covers both server-side and client-side TLS security.

## Prerequisites

- [ ] Inventory of all TLS-enabled endpoints (domains, IPs, ports)
- [ ] Access to server configurations or ability to perform external scanning
- [ ] TLS scanning tools ready: `testssl.sh`, `sslyze`, `nmap --script ssl-*`, `openssl s_client`
- [ ] Certificate management records available (CA, expiration dates, key types)
- [ ] Organizational TLS policy document (if exists) for compliance comparison

---

## Phase 1 -- Protocol Version Assessment

- [ ] Scan all endpoints for supported protocol versions:
  ```bash
  testssl.sh --protocols https://target.example.com
  # Or with sslyze
  sslyze --regular target.example.com
  ```
- [ ] Verify protocol compliance:
  - **Required**: TLS 1.2 and/or TLS 1.3
  - **Prohibited**: SSL 2.0, SSL 3.0 (POODLE), TLS 1.0 (PCI DSS prohibited since 2018), TLS 1.1 (deprecated RFC 8996)
- [ ] If TLS 1.3 is supported: verify it is preferred over TLS 1.2 in server order
- [ ] If TLS 1.2 is still required for compatibility: document the business justification and timeline for deprecation
- [ ] Check for protocol downgrade attack resilience (TLS_FALLBACK_SCSV support)
  ```bash
  openssl s_client -connect target.example.com:443 -fallback_scsv -tls1_1
  ```
- [ ] Verify no cleartext fallback exists (port 80 redirects to 443, no mixed content)

## Phase 2 -- Cipher Suite Review

- [ ] Enumerate supported cipher suites:
  ```bash
  testssl.sh --cipher-per-proto https://target.example.com
  nmap --script ssl-enum-ciphers -p 443 target.example.com
  ```
- [ ] For TLS 1.3: only these cipher suites should be present:
  - TLS_AES_256_GCM_SHA384
  - TLS_AES_128_GCM_SHA256
  - TLS_CHACHA20_POLY1305_SHA256
- [ ] For TLS 1.2: verify cipher suites meet requirements:
  - **Required**: ECDHE or DHE key exchange (forward secrecy)
  - **Required**: AES-GCM or ChaCha20-Poly1305 (AEAD)
  - **Prohibited**: RC4, DES, 3DES, NULL ciphers, EXPORT ciphers
  - **Prohibited**: RSA key exchange (no forward secrecy)
  - **Prohibited**: CBC mode ciphers (BEAST, Lucky13 -- accept only if required for compatibility)
  - **Prohibited**: Anonymous key exchange (aNULL, ADH)
- [ ] Verify server cipher order preference is enforced (server chooses, not client)
- [ ] If DHE is used: DH parameters must be >= 2048 bits (check for Logjam vulnerability)
- [ ] If ECDHE is used: curve must be P-256, P-384, or X25519

## Phase 3 -- Certificate Validation

- [ ] Verify certificate chain completeness:
  ```bash
  openssl s_client -connect target.example.com:443 -showcerts </dev/null 2>/dev/null | openssl x509 -text -noout
  ```
- [ ] Certificate properties:
  - [ ] Subject/SAN matches the domain being accessed
  - [ ] Certificate is not expired (check `notAfter`)
  - [ ] Certificate is not yet valid in the future (check `notBefore`)
  - [ ] Key algorithm and size meet minimums: RSA >= 2048 (3072+ preferred), ECDSA P-256+
  - [ ] Signature algorithm uses SHA-256 or stronger (not SHA-1 or MD5)
  - [ ] Certificate is issued by a trusted CA (not self-signed in production)
- [ ] Certificate chain:
  - [ ] Intermediate certificates are served by the server (not relying on AIA fetching)
  - [ ] Chain terminates at a trusted root CA
  - [ ] No unnecessary certificates in the chain
- [ ] Check for certificate revocation:
  ```bash
  # OCSP check
  openssl s_client -connect target.example.com:443 -status </dev/null 2>/dev/null | grep -A 5 "OCSP Response"
  # CRL check
  openssl x509 -in cert.pem -text -noout | grep -A 2 "CRL Distribution"
  ```
- [ ] Verify OCSP stapling is enabled (reduces latency and privacy concerns)
- [ ] Wildcard certificates: verify scope is appropriate (no overly broad wildcards)
- [ ] Multi-domain (SAN) certificates: verify all listed domains are still active and owned

## Phase 4 -- Certificate Transparency

- [ ] Verify certificates are logged in Certificate Transparency (CT) logs
  ```bash
  # Check CT log presence
  curl -s "https://crt.sh/?q=%.example.com&output=json" | jq '.[0:5]'
  ```
- [ ] Monitor CT logs for unauthorized certificate issuance for your domains
- [ ] Verify SCT (Signed Certificate Timestamp) is delivered via:
  - TLS extension (preferred)
  - OCSP stapling
  - X.509 certificate extension
- [ ] Set up continuous CT monitoring with tools like CertStream, Facebook CT monitor, or crt.sh alerts
- [ ] Investigate any certificates in CT logs that were not issued by your organization

## Phase 5 -- HTTP Security Headers

- [ ] HSTS (HTTP Strict Transport Security) is enabled:
  ```
  Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
  ```
  - [ ] `max-age` is at least 1 year (31536000 seconds)
  - [ ] `includeSubDomains` is set if all subdomains use HTTPS
  - [ ] Consider HSTS preload list submission (https://hstspreload.org/)
- [ ] HTTP responses on port 80 return 301 redirect to HTTPS (not 302)
- [ ] No mixed content: all resources (scripts, stylesheets, images, iframes) loaded via HTTPS
- [ ] `Expect-CT` header set (deprecated but still provides monitoring value during transition)
- [ ] Cookies use `Secure` flag (never sent over HTTP)
- [ ] Content-Security-Policy `upgrade-insecure-requests` directive considered

## Phase 6 -- Certificate Pinning Assessment

- [ ] Evaluate whether certificate pinning is appropriate for the application:
  - Mobile apps: pinning recommended (pin to leaf or intermediate CA)
  - Web browsers: HPKP deprecated; use CAA DNS records instead
  - API-to-API: mutual TLS (mTLS) preferred over pinning
- [ ] If pinning is implemented:
  - [ ] Backup pins are configured (at least one backup key/CA)
  - [ ] Pin rotation procedure is documented and tested
  - [ ] Report-only mode used during rollout
  - [ ] Monitoring for pin validation failures is active
- [ ] CAA DNS records configured to restrict which CAs can issue certificates:
  ```bash
  dig CAA example.com
  # Expected: 0 issue "letsencrypt.org" (or your CA)
  ```

## Phase 7 -- Advanced TLS Testing

- [ ] Test for known vulnerabilities:
  ```bash
  testssl.sh --vulnerable https://target.example.com
  ```
  - [ ] BEAST (CVE-2011-3389): mitigated by TLS 1.1+ or RC4 avoidance
  - [ ] CRIME/BREACH: TLS compression disabled
  - [ ] Heartbleed (CVE-2014-0160): OpenSSL patched
  - [ ] POODLE (CVE-2014-3566): SSL 3.0 disabled
  - [ ] FREAK (CVE-2015-0204): no EXPORT ciphers
  - [ ] Logjam (CVE-2015-4000): DH >= 2048 bits
  - [ ] ROBOT (CVE-2017-13099): RSA key exchange disabled or patched
  - [ ] Ticketbleed: session ticket implementation patched
  - [ ] DROWN (CVE-2016-0800): no SSLv2 on any server sharing the same key
- [ ] Test TLS renegotiation:
  - [ ] Client-initiated renegotiation disabled or rate-limited
  - [ ] Secure renegotiation extension supported (RFC 5746)
- [ ] Test session resumption security (session tickets, session IDs)
- [ ] Verify 0-RTT (TLS 1.3 early data) is disabled or replay-protected for sensitive endpoints
- [ ] Test for timing side-channels in certificate validation and key exchange

## Phase 8 -- Remediation and Documentation

- [ ] Generate prioritized finding list:
  - **Critical**: protocol or cipher vulnerabilities enabling interception
  - **High**: missing HSTS, weak certificates, disabled forward secrecy
  - **Medium**: missing CT monitoring, suboptimal cipher order
  - **Low**: cosmetic issues, informational findings
- [ ] Provide specific remediation configurations:
  ```nginx
  # Nginx example
  ssl_protocols TLSv1.2 TLSv1.3;
  ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305;
  ssl_prefer_server_ciphers on;
  ssl_session_timeout 1d;
  ssl_session_cache shared:SSL:10m;
  ssl_stapling on;
  ssl_stapling_verify on;
  ```
- [ ] Schedule re-test after remediation to verify fixes
- [ ] Set up automated TLS monitoring for continuous compliance

---

## Cross-References

- Cryptographic implementation: `checklists/crypto/cryptographic-implementation-checklist.md`
- Key management: `checklists/crypto/key-management-checklist.md`
- Crypto vulnerability assessment: `checklists/crypto/crypto-vulnerability-assessment-checklist.md`
- Web application assessment: `checklists/web-app-assessment-quality.md`
- Mozilla SSL Configuration Generator: https://ssl-config.mozilla.org/
- NIST SP 800-52r2: Guidelines for TLS Implementations
