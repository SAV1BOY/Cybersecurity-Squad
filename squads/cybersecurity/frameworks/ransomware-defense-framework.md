# Ransomware Defense Framework

## Purpose

Comprehensive ransomware defense covering prevention, detection, response, and recovery. Addresses the full ransomware kill chain from initial access through impact, with specific controls at each stage.

## Ransomware Kill Chain

```
Phishing/Exploit -> Initial Access -> Persistence -> Privilege Escalation
    -> Lateral Movement -> Discovery -> Collection -> Exfiltration
    -> Inhibit Recovery (backup deletion) -> Encryption/Impact -> Ransom Demand
```

## Prevention Controls

### Initial Access Prevention

| Attack Vector | Control | Implementation |
|--------------|---------|---------------|
| Phishing email | Email security gateway | Advanced threat protection, sandboxing, URL rewriting |
| Malicious attachment | Attachment filtering | Block macro-enabled docs, executable extensions |
| Exploit of public service | Patch management | Critical patches within 24-72 hours, WAF |
| RDP exposure | Network segmentation | No RDP to internet, VPN + MFA required |
| Stolen credentials | Credential protection | MFA everywhere, password monitoring, credential stuffing detection |
| Drive-by download | Web proxy/filtering | Category-based blocking, SSL inspection, browser isolation |
| Supply chain | Vendor risk management | Software allowlisting, code signing verification |

### Execution Prevention

| Control | Implementation | Bypass Resistance |
|---------|---------------|-------------------|
| Application allowlisting | AppLocker/WDAC policies | High (if properly configured) |
| Script execution control | PowerShell Constrained Language Mode | Medium |
| Macro blocking | Office macro block by default (Group Policy) | High |
| AMSI integration | Enable AMSI for scripting engines | Medium |
| User Account Control | Enforce UAC, no auto-elevate | Medium |
| Code signing enforcement | Only signed executables | High |

### Lateral Movement Prevention

| Control | Implementation |
|---------|---------------|
| Network segmentation | Micro-segmentation, VLAN isolation |
| SMB hardening | Disable SMBv1, restrict SMB access to file servers only |
| LAPS/credential tiering | Unique local admin passwords, tiered admin accounts |
| Just-in-time admin | Time-bounded privilege elevation |
| RDP restriction | RDP only from jump hosts, NLA required |
| WMI/WinRM restriction | Limit remote management to admin workstations |
| Service account hardening | No interactive login, credential rotation |

### Backup Protection (Immutable Backups)

| Requirement | Implementation |
|-------------|---------------|
| Immutability | WORM storage, immutable snapshots, object lock |
| Air-gap | Offline backups, tape, disconnected storage |
| Separate credentials | Backup admin accounts isolated from domain |
| Multi-location | Geographically distributed copies (3-2-1 rule) |
| Encryption | Backup encryption with offline key storage |
| Regular testing | Monthly restore tests, annual full DR exercise |
| Retention | Minimum 90-day retention for ransomware recovery |
| Monitoring | Alert on backup job failures, retention changes, deletion attempts |

**3-2-1-1-0 Backup Rule:**
- **3** copies of data
- **2** different storage media types
- **1** offsite copy
- **1** immutable or air-gapped copy
- **0** errors after recovery verification

## Detection Controls

### Canary Files and Tokens

| Canary Type | Placement | Detection Method |
|------------|-----------|-----------------|
| Honeypot files | Network shares, user desktops, server directories | File access monitoring (SACL audit) |
| Canary tokens | Documents with embedded beacons | HTTP callback on open/access |
| Decoy credentials | LSASS memory, credential stores | Authentication attempt monitoring |
| Honeyshares | Network shares with enticing names | Any access triggers alert |
| Canary DNS | Embedded DNS lookups in decoy files | DNS query monitoring |

### Behavioral Detection

| Behavior | Detection Rule | MITRE Technique |
|----------|---------------|----------------|
| Mass file rename | >100 file renames in 60 seconds per process | T1486 (Data Encrypted) |
| File extension change | Known ransomware extensions (.encrypted, .locked, etc.) | T1486 |
| Volume shadow deletion | vssadmin.exe, wmic shadowcopy | T1490 (Inhibit Recovery) |
| Backup catalog deletion | wbadmin delete, bcdedit /set | T1490 |
| Disable security tools | Service stop for AV/EDR, tamper with config | T1562 (Impair Defenses) |
| Encryption indicators | High entropy file writes, crypto API calls | T1486 |
| Lateral tool transfer | PsExec, WMI remote execution | T1570 |
| Data staging | Large data collection to staging directory | T1074 |

### EDR Detection Rules

| Rule | Logic | Severity |
|------|-------|----------|
| Ransomware canary triggered | Canary file accessed by non-approved process | Critical |
| Shadow copy deletion | Process executes vssadmin delete shadows | Critical |
| Mass file modification | >50 files modified in <30 seconds by single process | Critical |
| Boot config modification | bcdedit.exe modifying recovery settings | High |
| Encryption API abuse | CryptEncrypt/CryptGenKey calls by unsigned process | High |
| Backup service disruption | Backup agent service stopped or disabled | High |
| Known ransomware IOC | Hash, mutex, or registry key match | Critical |

## Response Procedures

### Immediate Response (First 30 Minutes)

1. **Isolate** -- Network-isolate affected systems (EDR isolation or switch port disable)
2. **Preserve** -- Do NOT reboot or power off (preserve memory evidence)
3. **Scope** -- Determine extent of encryption and lateral movement
4. **Communicate** -- Activate incident response team, notify CISO
5. **Contain** -- Block C2 domains/IPs at firewall, disable compromised accounts
6. **Preserve backups** -- Verify backup integrity, disconnect backup systems if not already isolated

### Investigation (Hours 1-24)

| Task | Priority | Responsible |
|------|----------|-------------|
| Identify ransomware variant | Critical | Malware analyst |
| Determine initial access vector | Critical | IR team |
| Map lateral movement path | Critical | IR team |
| Assess data exfiltration | High | IR team + network forensics |
| Identify all affected systems | High | SOC + IR team |
| Check for decryption tools | High | IR team (check No More Ransom) |
| Preserve forensic evidence | High | Forensics team |
| Engage external IR firm (if needed) | High | CISO |
| Notify legal counsel | High | CISO |
| Notify cyber insurance carrier | High | Legal/finance |

### Decision Framework: To Pay or Not to Pay

| Factor | Pay Consideration | Do Not Pay Consideration |
|--------|-------------------|--------------------------|
| Backups available | -- | Backups intact and tested |
| Business impact | Revenue loss exceeds ransom | Limited impact, recovery feasible |
| Decryptor available | No free decryptor exists | Free decryptor available |
| Legal restrictions | Not sanctioned entity | OFAC-sanctioned group |
| Data exfiltration | Sensitive data at risk of leak | No exfiltration evidence |
| Threat actor reliability | Known to provide working decryptor | Known to re-extort or not decrypt |
| Insurance coverage | Coverage includes ransom | No coverage |

**Recommendation:** Exhaust all recovery options before considering payment. Engage law enforcement and legal counsel before any payment decision.

## Recovery

### Recovery Priority

| Priority | System Category | Target RTO |
|----------|----------------|-----------|
| 1 | Identity infrastructure (AD, DNS, DHCP) | 4-8 hours |
| 2 | Security infrastructure (SIEM, EDR, AV) | 8-12 hours |
| 3 | Communication systems (email, messaging) | 12-24 hours |
| 4 | Critical business applications | 24-48 hours |
| 5 | General business applications | 48-72 hours |
| 6 | End-user workstations | 72+ hours |

### Recovery Steps

1. Build clean recovery environment (isolated network segment)
2. Restore AD from known-good backup or rebuild
3. Reset ALL credentials (every account, every service)
4. Restore systems from verified clean backups
5. Scan restored systems before reconnecting to network
6. Implement additional monitoring before full reconnection
7. Gradually reconnect systems with enhanced logging
8. Monitor for re-infection indicators for 30+ days

## Cross-References

- [Incident Response Workflow](../workflows/incident-response-workflow.md) -- response procedures
- [Incident Severity Classification](incident-severity-classification.md) -- SEV-1 classification
- [Backup Security Checklist](../checklists/data-protection/backup-security-checklist.md) -- backup hardening
- [Network Segmentation Framework](network-segmentation-framework.md) -- lateral movement prevention
- [Sigma Rule Examples](../swipe/detection/sigma-rule-examples.md) -- detection rules
