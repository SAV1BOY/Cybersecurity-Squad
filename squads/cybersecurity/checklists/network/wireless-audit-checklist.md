# Wireless Security Audit Checklist

## Purpose

Checklist for wireless network security audits covering rogue AP detection, encryption review, segmentation validation, client isolation, and monitoring requirements.

## Wireless Infrastructure Review

### Access Point Configuration

- [ ] All access points inventoried (make, model, firmware, location)
- [ ] AP firmware current and patched
- [ ] Default credentials changed on all APs
- [ ] AP management interface restricted to wired management network
- [ ] AP management uses HTTPS/SSH only (HTTP/telnet disabled)
- [ ] AP physical security assessed (tamper-proof mounting, secure locations)
- [ ] Unused radio interfaces disabled
- [ ] AP transmit power configured appropriately (minimize coverage outside premises)
- [ ] Channel assignment reviewed (minimize interference)
- [ ] AP configuration backup automated

### SSID Configuration

| Check | Corporate SSID | Guest SSID | IoT SSID | Verified |
|-------|---------------|-----------|----------|----------|
| SSID broadcast appropriate | Hidden optional | Broadcast | Hidden preferred | [ ] |
| Encryption: WPA3 or WPA2-Enterprise | Required | WPA2 minimum | WPA2 minimum | [ ] |
| Authentication: 802.1X/EAP | Required | Captive portal | PSK or 802.1X | [ ] |
| VLAN assignment | Corporate VLAN | Isolated guest VLAN | Isolated IoT VLAN | [ ] |
| Client isolation | Disabled (trusted) | Enabled (required) | Enabled (required) | [ ] |
| Band steering | Enabled (prefer 5GHz) | Optional | As needed | [ ] |
| Maximum clients per AP | Configured | Configured (lower) | Configured | [ ] |

## Encryption Review

### Encryption Standards

- [ ] WPA3-Enterprise (SAE) deployed for corporate wireless (preferred)
- [ ] WPA2-Enterprise (AES-CCMP) minimum for corporate wireless
- [ ] WPA2 with TKIP disabled (AES/CCMP only)
- [ ] WEP completely eliminated from environment
- [ ] Open (unencrypted) networks eliminated or strictly controlled
- [ ] Pre-shared key (PSK) networks eliminated for corporate use
- [ ] PMF (Protected Management Frames) enabled (802.11w)
- [ ] OWE (Opportunistic Wireless Encryption) enabled for open networks

### 802.1X/EAP Configuration

- [ ] EAP-TLS used for certificate-based authentication (preferred)
- [ ] If EAP-PEAP/MSCHAPv2: server certificate validation enforced on clients
- [ ] If EAP-PEAP: outer identity does not reveal username
- [ ] RADIUS server uses signed certificate from trusted CA
- [ ] RADIUS server certificate validated by clients (pinned or CA-verified)
- [ ] RADIUS accounting enabled for audit trail
- [ ] RADIUS shared secret is strong (32+ characters)
- [ ] RADIUS traffic encrypted (RadSec/DTLS preferred)
- [ ] EAP timeout and retransmission values configured
- [ ] Failed authentication logged and alerted

### Certificate Management (EAP-TLS)

- [ ] Client certificates deployed via MDM or PKI auto-enrollment
- [ ] Certificate revocation checking enabled (OCSP or CRL)
- [ ] Certificate validity period appropriate (1-2 years for client certs)
- [ ] Private keys protected (TPM or secure enclave)
- [ ] Certificate enrollment restricted to managed devices only
- [ ] Certificate renewal automated before expiration

## Network Segmentation

### Wireless Network Isolation

- [ ] Corporate wireless on separate VLAN from guest and IoT
- [ ] Guest wireless isolated from all internal networks
- [ ] Guest wireless has internet access only (no internal routing)
- [ ] IoT wireless on dedicated VLAN with restricted access
- [ ] BYOD wireless separated from corporate managed devices
- [ ] Inter-VLAN routing controlled by firewall (not switch ACLs alone)
- [ ] Wireless management traffic on dedicated VLAN

### Segmentation Validation

| Test | Method | Verified |
|------|--------|----------|
| Guest cannot reach internal systems | Port scan from guest VLAN | [ ] |
| Guest can only reach internet | Traceroute and connectivity test | [ ] |
| IoT cannot reach corporate resources | Port scan from IoT VLAN | [ ] |
| Corporate wireless reaches authorized resources | Application connectivity test | [ ] |
| BYOD restricted to authorized services | Access test matrix | [ ] |
| Cross-VLAN traffic logged at firewall | Log review | [ ] |

## Rogue AP Detection

### Detection Methods

- [ ] Wireless intrusion detection system (WIDS) deployed
- [ ] Dedicated sensors or AP-based scanning configured
- [ ] Rogue AP detection scans run continuously (not just periodic)
- [ ] Wired-side rogue detection enabled (NAC, 802.1X on switch ports)
- [ ] Alert workflow defined for rogue AP detection
- [ ] Rogue AP response procedure documented

### Rogue AP Response

| Detection | Classification | Response |
|-----------|---------------|----------|
| Unknown SSID on premises | Potential rogue | Investigate, locate, disable |
| Corporate SSID from unauthorized AP | Evil twin / rogue | Immediate containment, locate |
| Ad-hoc network detected | Policy violation | Notify user, disable |
| Bluetooth AP / mobile hotspot | Policy violation | Notify user, enforce policy |
| Neighboring AP (expected) | Benign | Document and exclude from alerts |

### Periodic Wireless Surveys

- [ ] Physical wireless survey conducted annually
- [ ] Coverage maps updated after infrastructure changes
- [ ] Signal bleed outside premises assessed
- [ ] Dead zones identified and addressed
- [ ] Unauthorized APs identified during survey
- [ ] Channel utilization and interference documented

## Client Security

### Managed Device Configuration

- [ ] Auto-connect to corporate SSID only (not open networks)
- [ ] Certificate-based authentication configured (not username/password prompts)
- [ ] Server certificate validation enforced (prevent evil twin)
- [ ] Preferred network list controlled (remove unauthorized SSIDs)
- [ ] WiFi sense / auto-sharing disabled
- [ ] Direct WiFi / ad-hoc mode disabled
- [ ] VPN auto-connect configured for non-corporate networks
- [ ] Device firewall active on wireless interfaces

### BYOD/Unmanaged Devices

- [ ] BYOD wireless policy defined and communicated
- [ ] BYOD devices use separate SSID/VLAN from corporate managed
- [ ] BYOD access requires registration and acceptance of terms
- [ ] BYOD network access limited to specific services (email, SaaS)
- [ ] NAC/posture assessment for BYOD where possible
- [ ] BYOD devices cannot access file shares or internal applications directly

## Monitoring

### Wireless Monitoring Requirements

- [ ] Authentication success/failure events logged
- [ ] Association/disassociation events logged
- [ ] Rogue AP alerts monitored 24x7
- [ ] Deauthentication flood detection enabled
- [ ] Evil twin detection enabled
- [ ] Client probe request monitoring (optional, privacy considerations)
- [ ] Bandwidth anomaly detection per client
- [ ] New device type detection (unusual device fingerprints)

### Wireless Security Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| WPA3/WPA2-Enterprise coverage | 100% of corporate | Quarterly |
| Rogue APs detected | 0 unresolved | Monthly |
| PSK networks | 0 for corporate | Monthly |
| AP firmware currency | 100% current | Monthly |
| 802.1X authentication failure rate | <2% | Weekly |
| Guest network isolation verified | Pass | Quarterly |

## Cross-References

- [Network Segmentation Framework](../../frameworks/network-segmentation-framework.md) -- segmentation strategy
- [Network Monitoring Checklist](network-monitoring-checklist.md) -- monitoring integration
- [Wireless Security Methodology](../../frameworks/wireless-security-methodology.md) -- testing methodology
- [MFA Implementation Checklist](../identity/mfa-implementation-checklist.md) -- wireless + MFA
