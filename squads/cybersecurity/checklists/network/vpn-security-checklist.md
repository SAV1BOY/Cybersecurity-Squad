# VPN Security Checklist

## Purpose

Checklist for VPN security covering configuration review, authentication hardening, split tunneling assessment, logging requirements, and certificate management.

## VPN Configuration Review

### Protocol and Encryption

- [ ] VPN protocol is current (IKEv2, WireGuard, or OpenVPN preferred)
- [ ] IKEv1 disabled or migrated to IKEv2
- [ ] PPTP and L2TP without IPSec eliminated
- [ ] SSL/TLS VPN uses TLS 1.2+ only
- [ ] Weak cipher suites disabled (DES, 3DES, RC4, MD5)
- [ ] Strong encryption configured (AES-256-GCM or ChaCha20-Poly1305)
- [ ] Perfect Forward Secrecy (PFS) enabled (DH Group 14+ or ECDH)
- [ ] IKE lifetime: Phase 1 = 8 hours maximum, Phase 2 = 1 hour maximum
- [ ] Dead Peer Detection (DPD) enabled
- [ ] Anti-replay protection enabled
- [ ] Compression disabled (VORACLE/CRIME attack prevention)

### Recommended Cipher Configuration

| Component | Minimum | Recommended | Verified |
|-----------|---------|-------------|----------|
| IKE encryption | AES-256 | AES-256-GCM | [ ] |
| IKE integrity | SHA-256 | SHA-384/SHA-512 | [ ] |
| IKE DH group | Group 14 (2048-bit) | Group 19/20 (ECDH) | [ ] |
| ESP encryption | AES-256 | AES-256-GCM | [ ] |
| ESP integrity | SHA-256 | SHA-384 (or GCM) | [ ] |
| ESP DH group (PFS) | Group 14 | Group 19/20 | [ ] |

## Authentication

### VPN Authentication Configuration

- [ ] Multi-factor authentication required for all VPN users
- [ ] Certificate-based authentication preferred (certificate + MFA)
- [ ] Pre-shared key authentication eliminated (or per-user PSK minimum)
- [ ] RADIUS/LDAP integration for centralized authentication
- [ ] Account lockout configured for VPN authentication failures
- [ ] Authentication timeout configured (prevent stale sessions)
- [ ] Machine certificate validation enabled (managed devices only, if applicable)
- [ ] Authentication logs include source IP, username, result, and timestamp

### User Authorization

- [ ] VPN access requires explicit group membership (not all employees by default)
- [ ] VPN access grants are reviewed quarterly
- [ ] Terminated employee VPN access revoked within 1 hour
- [ ] Contractor VPN access is time-bounded with expiration
- [ ] VPN user-to-group mapping documented
- [ ] Least-privilege network access per VPN group (not full network)

### Certificate Management

- [ ] VPN server certificate issued by trusted CA (internal PKI preferred)
- [ ] VPN server certificate not expired
- [ ] VPN server certificate uses strong key (RSA 2048+ or ECDSA P-256+)
- [ ] VPN server certificate includes correct hostname/IP in SAN
- [ ] Client certificate validation enabled (if using cert-based auth)
- [ ] Certificate revocation checking enabled (OCSP or CRL)
- [ ] Certificate renewal automated before expiration
- [ ] Certificate private key protected (HSM for server, TPM for client)
- [ ] Self-signed certificates eliminated
- [ ] Certificate transparency monitoring for VPN domains

## Split Tunneling

### Split Tunneling Assessment

| Mode | Description | Risk | Use Case |
|------|-------------|------|----------|
| Full tunnel | All traffic through VPN | Low | Highest security, complete visibility |
| Split tunnel (include) | Only corporate traffic through VPN | Medium | Better performance, partial visibility |
| Split tunnel (exclude) | Most traffic through VPN, exceptions defined | Low-Medium | Performance + visibility balance |
| No VPN (ZTNA) | Per-application access | Lowest (if well-implemented) | Modern zero trust architecture |

### If Using Full Tunnel

- [ ] All traffic routes through corporate network
- [ ] Internet traffic exits through corporate proxy/firewall
- [ ] DNS queries use corporate DNS servers
- [ ] No local network access exceptions (or explicitly documented)
- [ ] Split DNS configured for internal domain resolution
- [ ] Performance impact assessed and acceptable

### If Using Split Tunnel

- [ ] Split tunnel policy explicitly defines corporate routes
- [ ] DNS for corporate domains routes through VPN
- [ ] DNS for internet domains uses corporate DNS (DNS leak prevention)
- [ ] Local network access restricted where possible
- [ ] Client firewall active on non-VPN interface
- [ ] Endpoint security controls enforced regardless of VPN status
- [ ] Internet traffic monitored via endpoint agent (not relying on network)
- [ ] Risk acceptance documented by security leadership

## VPN Client Security

### Client Configuration

- [ ] VPN client is enterprise-managed (deployed via MDM/SCCM)
- [ ] VPN client auto-update enabled
- [ ] VPN client version is current and supported
- [ ] Always-on VPN configured (auto-connect when off corporate network)
- [ ] VPN client prevents disconnect by user (if always-on required)
- [ ] VPN reconnect on network change (WiFi to cellular, etc.)
- [ ] Client-side firewall rules active during VPN session
- [ ] Kill switch enabled (block internet if VPN drops, if full tunnel)
- [ ] VPN profile locked (users cannot modify settings)

### Endpoint Posture Assessment

- [ ] Endpoint health check before VPN access (NAC/posture assessment)
- [ ] Minimum OS version enforced
- [ ] Antivirus/EDR running and current
- [ ] OS patches current (within acceptable window)
- [ ] Disk encryption enabled
- [ ] No jailbreak/root detection bypass
- [ ] Compliance check results logged
- [ ] Non-compliant devices given limited access or blocked

## Logging and Monitoring

### VPN Logging Requirements

| Log Type | Data Captured | Retention | Verified |
|----------|-------------|-----------|----------|
| Authentication | Username, source IP, result, timestamp, MFA method | 1 year | [ ] |
| Session | Connect/disconnect time, duration, bytes transferred | 90 days | [ ] |
| Authorization | Group membership, ACL applied, resources accessed | 90 days | [ ] |
| Errors | Connection failures, certificate errors | 90 days | [ ] |
| Admin | Configuration changes, user management | 1 year | [ ] |

### VPN Monitoring Alerts

| Alert | Severity | Condition |
|-------|----------|-----------|
| VPN login from unusual country | High | GeoIP outside normal locations |
| Multiple VPN sessions same user | Medium | Concurrent sessions (if not expected) |
| VPN authentication failure brute force | High | >5 failures in 5 minutes from same IP |
| VPN login outside business hours | Low-Medium | Configurable time window |
| VPN connection from known-bad IP | Critical | Threat intelligence match |
| VPN tunnel established from Tor exit node | High | Tor exit node IP list match |
| Large data transfer over VPN | Medium | >threshold per session |
| VPN gateway approaching capacity | Medium | >80% concurrent sessions |
| VPN service certificate expiring | High | <30 days to expiry |

## VPN Infrastructure Security

### VPN Gateway Hardening

- [ ] VPN gateway OS/firmware patched and current
- [ ] VPN gateway management interface on dedicated management network
- [ ] VPN gateway management access requires MFA
- [ ] VPN gateway admin accounts are individual (no shared admin)
- [ ] VPN gateway hardened (unnecessary services disabled)
- [ ] VPN gateway HA configured and tested
- [ ] VPN gateway capacity planned for peak usage
- [ ] VPN gateway in DMZ or dedicated network segment
- [ ] Inbound firewall rules restrict VPN protocols only (UDP 500, 4500; or TCP 443)
- [ ] VPN concentrator does not host other services

### Operational Security

- [ ] VPN configuration backup automated and encrypted
- [ ] VPN disaster recovery procedure documented and tested
- [ ] VPN capacity monitoring and alerting configured
- [ ] VPN software vulnerability monitoring (subscribe to vendor advisories)
- [ ] Emergency VPN shutdown procedure documented
- [ ] VPN access can be remotely revoked per user or globally
- [ ] Regular VPN penetration testing included in assessment scope

## Cross-References

- [Network Segmentation Framework](../../frameworks/network-segmentation-framework.md) -- VPN and segmentation
- [MFA Implementation Checklist](../identity/mfa-implementation-checklist.md) -- VPN MFA
- [Firewall Audit Checklist](firewall-audit-checklist.md) -- VPN firewall rules
- [Network Monitoring Checklist](network-monitoring-checklist.md) -- VPN traffic monitoring
