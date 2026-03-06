# DNS Security Checklist

## Purpose

Comprehensive DNS security checklist covering DNSSEC, DNS-over-HTTPS controls, DNS sinkholing, query monitoring, and cache poisoning prevention.

## DNS Infrastructure Security

### DNS Server Hardening

- [ ] DNS servers run current, patched software
- [ ] DNS servers are dedicated (not shared with other services)
- [ ] DNS servers run with least-privilege service accounts
- [ ] Zone transfer restricted to authorized secondary servers only (AXFR/IXFR)
- [ ] Recursion disabled on authoritative DNS servers
- [ ] DNS server management interface on dedicated management network
- [ ] DNS server access restricted via firewall rules
- [ ] DNS server logs forwarded to SIEM
- [ ] DNS server OS hardened (unnecessary services disabled)
- [ ] DNS version information hidden (version.bind disabled)
- [ ] Dynamic DNS updates restricted (secure dynamic updates only)
- [ ] Response Rate Limiting (RRL) enabled to prevent amplification attacks

### Resolver Configuration

- [ ] Internal resolvers configured for internal zones
- [ ] Forwarders configured to trusted upstream resolvers only
- [ ] Resolver cache poisoning protections enabled (source port randomization, TXID randomization)
- [ ] Resolver query logging enabled
- [ ] Resolver access restricted to internal networks only
- [ ] Open resolver check performed (no external recursion)
- [ ] EDNS0 supported and configured
- [ ] DNS over TCP supported (for large responses)

## DNSSEC

### DNSSEC Deployment

- [ ] DNSSEC enabled on authoritative zones (external domains)
- [ ] Zone Signing Key (ZSK) algorithm: ECDSAP256SHA256 or RSA-SHA256 (2048+)
- [ ] Key Signing Key (KSK) algorithm: ECDSAP256SHA256 or RSA-SHA256 (2048+)
- [ ] ZSK rotation automated (monthly recommended)
- [ ] KSK rotation planned (annual, with DS record coordination)
- [ ] DS records published in parent zone
- [ ] NSEC3 used (not NSEC, to prevent zone walking)
- [ ] DNSSEC validation enabled on resolvers
- [ ] DNSSEC monitoring configured (alert on validation failures)
- [ ] Key rollover procedures documented and tested

### DNSSEC Validation

- [ ] Internal resolvers validate DNSSEC signatures
- [ ] DNSSEC validation failures logged and alerted
- [ ] Trust anchors configured and maintained
- [ ] Regular validation testing performed (known-good and known-bad domains)
- [ ] Negative trust anchors documented for legitimate validation failures

## DNS-over-HTTPS (DoH) and DNS-over-TLS (DoT) Controls

### Organizational Policy

| Policy Decision | Options | Selected |
|----------------|---------|----------|
| Allow DoH/DoT | Permit for privacy | [ ] |
| Block DoH/DoT | Maintain DNS visibility | [ ] |
| Redirect DoH/DoT | Force through corporate resolver | [ ] |

### If Blocking DoH/DoT

- [ ] Known DoH resolver IPs blocked at firewall
- [ ] Known DoH domains blocked at DNS level
- [ ] TLS inspection identifies and blocks DoH on port 443 (if capable)
- [ ] DoT (port 853) blocked at firewall
- [ ] Browser DoH settings controlled via GPO/MDM
- [ ] Application-level DoH disabled (Firefox: network.trr.mode = 5)
- [ ] Detection rules deployed for DoH/DoT bypass attempts

### If Allowing DoH/DoT

- [ ] Organization operates its own DoH/DoT resolver
- [ ] All DoH/DoT traffic directed to organizational resolver
- [ ] External DoH/DoT resolvers blocked
- [ ] DoH/DoT query logging maintained

## DNS Sinkholing

### Sinkhole Configuration

- [ ] DNS sinkhole deployed for malicious domain blocking
- [ ] Sinkhole response directs to controlled IP (for logging)
- [ ] Threat intelligence feed integrated (malware domains, C2, phishing)
- [ ] Feed update frequency: at least daily
- [ ] Sinkhole logging captures: querying IP, queried domain, timestamp
- [ ] Sinkhole alerts configured for known high-severity domains
- [ ] Sinkhole bypass detection (direct IP access to C2)
- [ ] Legitimate domains not inadvertently sinkholed (allowlist maintained)

### Sinkhole Feed Sources

| Feed Type | Source Examples | Update Frequency |
|-----------|---------------|-----------------|
| Malware C2 | Abuse.ch, AlienVault OTX | Hourly |
| Phishing domains | PhishTank, OpenPhish | Hourly |
| DGA domains | DGA detection algorithms | Real-time |
| Newly registered domains | WHOIS feeds | Daily |
| Threat intelligence platform | Internal TIP, ISAC feeds | As available |
| Category-based | Adult, gambling, etc. (policy-based) | Daily |

## DNS Query Monitoring

### Monitoring Requirements

- [ ] All DNS queries logged (source IP, query name, query type, response code)
- [ ] DNS logs forwarded to SIEM in real-time
- [ ] DNS query volume baseline established
- [ ] Anomaly detection configured for DNS

### Detection Rules

| Detection | Indicator | Severity |
|-----------|-----------|----------|
| DNS tunneling | High-entropy subdomains, excessive TXT queries | High |
| DGA detection | Algorithmically generated domain names | High |
| Newly registered domain queries | Domain age < 7 days | Medium |
| High-volume queries to single domain | >100 queries/min to one domain | Medium |
| Direct DNS to external resolvers | Bypass of internal DNS | High |
| DNS query for known malicious domain | IOC match | Critical |
| Unusual query types | AXFR, ANY, HINFO from clients | Medium |
| Excessive NXDOMAIN responses | >50 NXDOMAIN/min per client | Medium |
| Long subdomain labels | Subdomain > 30 characters | Medium |

### DNS Analytics

- [ ] Top queried domains dashboard (identify unusual entries)
- [ ] Top NXDOMAIN responses dashboard (DGA, misconfig, or recon)
- [ ] Query type distribution dashboard (unusual TXT/NULL/CNAME spikes)
- [ ] Query volume trend by client (identify compromised hosts)
- [ ] Geographic query distribution (queries to unexpected regions)
- [ ] New domain first-seen tracking

## Cache Poisoning Prevention

### Resolver Protections

- [ ] Source port randomization enabled (not predictable UDP ports)
- [ ] Transaction ID randomization enabled
- [ ] 0x20 encoding supported (case randomization in query names)
- [ ] Response validation checks enabled (bailiwick checking)
- [ ] DNS cookies (RFC 7873) supported and enabled
- [ ] Maximum cache TTL configured (prevent indefinite caching of poison)
- [ ] DNSSEC validation enabled (strongest defense against poisoning)
- [ ] DNS over TCP fallback enabled

### Network-Level Protections

- [ ] Ingress filtering prevents spoofed DNS responses from entering network
- [ ] Egress filtering prevents DNS queries with spoofed source addresses
- [ ] DNS traffic only allowed to/from authorized DNS servers
- [ ] Rate limiting on DNS responses from external sources

## Operational Security

- [ ] DNS change management process in place
- [ ] DNS zone file backups automated and tested
- [ ] DNS failover/redundancy tested quarterly
- [ ] DNS registrar accounts secured with MFA and access logging
- [ ] Domain lock (registrar lock) enabled for critical domains
- [ ] WHOIS privacy enabled where appropriate
- [ ] DNS monitoring for unauthorized zone changes
- [ ] Certificate Transparency monitoring for unauthorized cert issuance
- [ ] SPF, DKIM, and DMARC configured for email-sending domains

## Cross-References

- [Network Monitoring Checklist](network-monitoring-checklist.md) -- monitoring integration
- [Firewall Audit Checklist](firewall-audit-checklist.md) -- DNS-related firewall rules
- [Snort/Suricata Rules](../../swipe/detection/snort-suricata-rules.md) -- DNS detection rules
- [SPL Hunting Queries](../../swipe/detection/spl-hunting-queries.md) -- DNS anomaly queries
