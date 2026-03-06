# Attack Technique Taxonomy

## Purpose

Comprehensive attack technique classification from initial access through impact, mapped to MITRE ATT&CK with practical examples, detection approaches, and defensive controls for each category.

## Taxonomy Structure

### Tactic 1: Reconnaissance (TA0043)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Active Scanning | T1595 | Port scans, vulnerability scans | Nmap SYN scan of external perimeter | IDS alerts, firewall logs (high connection rate) |
| Search Open Websites | T1593 | GitHub, Pastebin, social media OSINT | Searching GitHub for leaked API keys | External monitoring, secret scanning |
| Gather Victim Identity | T1589 | Employee names, email formats, roles | LinkedIn scraping for org chart | Social media monitoring |
| Gather Victim Org Info | T1591 | Technology stack, relationships | Job postings revealing tech stack | Monitor job listing exposure |
| Search Victim-Owned Sites | T1594 | Website metadata, directory listings | Robots.txt, sitemap analysis | Web server hardening |

### Tactic 2: Initial Access (TA0001)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Phishing | T1566 | Spear-phishing with attachments or links | Macro-enabled document via email | Email gateway, sandbox detonation |
| Exploit Public Application | T1190 | Exploiting web apps, VPNs, RDP | Log4Shell against internet-facing app | WAF, vulnerability scanning, IDS |
| Valid Accounts | T1078 | Credential stuffing, purchased credentials | Reuse of leaked passwords from breaches | Impossible travel, password monitoring |
| Supply Chain Compromise | T1195 | Trojanized software update | SolarWinds-style backdoored update | SCA, integrity verification |
| Drive-by Compromise | T1189 | Watering hole with exploit kit | Compromised industry website serving exploit | Web proxy, browser isolation |
| Trusted Relationship | T1199 | Leverage vendor/partner access | MSP access to deploy malware | Vendor access monitoring |
| External Remote Services | T1133 | VPN, Citrix, RDP from internet | Brute force VPN with leaked credentials | MFA, auth anomaly detection |

### Tactic 3: Execution (TA0002)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Command/Script Interpreter | T1059 | PowerShell, cmd, bash, Python | `powershell -enc [base64]` | Script block logging, process monitoring |
| User Execution | T1204 | User opens malicious file/link | Double-clicking macro-enabled .docm | Endpoint protection, user training |
| Scheduled Task/Job | T1053 | Task scheduler, cron, at | `schtasks /create /sc onlogon /tr malware.exe` | EventID 4698/106, process monitoring |
| WMI | T1047 | Windows Management Instrumentation | `wmic /node:target process call create` | WMI event logging, process monitoring |
| Native API | T1106 | Direct Windows API calls | CreateRemoteThread for injection | API monitoring, EDR |
| System Services | T1569 | Service execution (sc.exe, PsExec) | PsExec deploying payload as service | EventID 7045, service monitoring |

### Tactic 4: Persistence (TA0003)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Registry Run Keys | T1547.001 | Auto-start via registry | Adding malware to HKCU\...\Run | Registry monitoring, Sysmon |
| Scheduled Task | T1053.005 | Persist via scheduled task | Task runs payload on boot/logon | Task scheduler monitoring |
| Account Creation | T1136 | Create new privileged account | `net user backdoor P@ssw0rd /add /domain` | EventID 4720, AD monitoring |
| Web Shell | T1505.003 | Web shell on server | PHP/ASP shell in web root | File integrity, YARA scanning |
| BITS Jobs | T1197 | Background transfer service | BITSAdmin persistent download | BITS job monitoring |
| Boot/Logon Init Scripts | T1037 | Logon scripts, boot scripts | GPO logon script modification | GPO monitoring, script review |
| Server Software Component | T1505 | IIS module, Exchange transport | Malicious Exchange transport agent | Application monitoring |
| Implant Container Image | T1525 | Backdoored container | Modified base image in registry | Image scanning, signing |

### Tactic 5: Privilege Escalation (TA0004)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Exploitation for Priv Esc | T1068 | Exploit kernel or service vulnerability | PrintNightmare (CVE-2021-34527) | Patch management, EDR |
| Access Token Manipulation | T1134 | Token impersonation/theft | Juicy Potato, PrintSpoofer | Token usage monitoring, EDR |
| Valid Accounts: Domain | T1078.002 | Use stolen domain admin creds | Pass-the-hash with domain admin NTLM | Admin logon monitoring, UEBA |
| Group Policy Modification | T1484.001 | Modify GPO for privilege | Add user to admins via GPO | GPO change monitoring |
| Domain Policy Modification | T1484 | Modify domain trust or policy | Add SID to SIDHistory | AD replication monitoring |

### Tactic 6: Defense Evasion (TA0005)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Indicator Removal | T1070 | Clear logs, timestomp | `wevtutil cl Security` | EventID 1102, remote logging |
| Masquerading | T1036 | Rename binary to look legitimate | svchost.exe in wrong directory | Path validation, process anomaly |
| Obfuscated Files | T1027 | Encoding, encryption, packing | Base64 PowerShell, UPX packed binary | Entropy analysis, deobfuscation |
| Process Injection | T1055 | Inject code into legitimate process | DLL injection into explorer.exe | Sysmon EventID 8/10, EDR |
| Rootkit | T1014 | Kernel-level hiding | UEFI rootkit | Secure Boot, integrity monitoring |
| Disable Security Tools | T1562 | Kill AV, tamper with EDR | Stopping Windows Defender service | Tamper protection, service monitoring |
| Signed Binary Proxy | T1218 | Use trusted binaries (LOLBins) | Regsvr32 loading remote scriptlet | LOLBin execution monitoring |

### Tactic 7: Credential Access (TA0006)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| OS Credential Dumping | T1003 | Dump LSASS, SAM, NTDS | Mimikatz sekurlsa::logonpasswords | LSASS access monitoring, Credential Guard |
| Brute Force | T1110 | Password spraying, stuffing | Spray single password across all accounts | Account lockout, auth anomaly |
| Kerberoasting | T1558.003 | Request service tickets, crack offline | Rubeus kerberoast | EventID 4769 with RC4 |
| Unsecured Credentials | T1552 | Credentials in files, registry, env vars | Passwords in Group Policy Preferences | Credential scanning, GPP audit |
| Steal Web Session Cookie | T1539 | Browser cookie theft | Evilginx2 phishing proxy | Phishing-resistant MFA |
| Adversary-in-the-Middle | T1557 | LLMNR/NBT-NS poisoning, ARP spoofing | Responder capturing NTLMv2 hashes | Network protocol monitoring |
| DCSync | T1003.006 | Replicate AD to extract hashes | Mimikatz lsadump::dcsync | EventID 4662 with replication GUIDs |

### Tactic 8: Discovery (TA0007)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Account Discovery | T1087 | Enumerate users and groups | `net user /domain`, `Get-ADUser` | AD query monitoring, LDAP logging |
| Network Service Discovery | T1046 | Internal port scanning | Nmap scan of internal subnets | IDS, network anomaly |
| Permission Groups Discovery | T1069 | Enumerate group memberships | BloodHound data collection | AD query monitoring |
| System Information Discovery | T1082 | OS version, patch level | `systeminfo`, `uname -a` | Process monitoring |
| Remote System Discovery | T1018 | Enumerate network hosts | `net view /domain`, ARP scanning | Network scanning detection |
| Domain Trust Discovery | T1482 | Map AD trust relationships | `nltest /domain_trusts` | AD query monitoring |

### Tactic 9: Lateral Movement (TA0008)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Remote Services: SMB | T1021.002 | PsExec, SMB file copy | PsExec deploying payload | EventID 7045, named pipe monitoring |
| Remote Services: RDP | T1021.001 | RDP to other systems | RDP with stolen credentials | EventID 4624 Type 10, UEBA |
| Remote Services: WinRM | T1021.006 | PowerShell Remoting | `Enter-PSSession -ComputerName target` | WinRM logging, EventID 4688 |
| Lateral Tool Transfer | T1570 | Copy tools between systems | Copy Mimikatz to target via SMB | File creation monitoring |
| Pass-the-Hash | T1550.002 | Use NTLM hash without cracking | Mimikatz sekurlsa::pth | EventID 4624 with NTLM, UEBA |
| Pass-the-Ticket | T1550.003 | Use stolen Kerberos ticket | Rubeus ptt | Anomalous ticket usage |
| Exploitation of Remote Services | T1210 | Exploit internal service | EternalBlue (MS17-010) internal | Patch management, IDS |

### Tactic 10: Collection (TA0009)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Data from Local System | T1005 | Collect files from compromised host | Copy sensitive documents | File access monitoring, DLP |
| Data from Network Shared Drive | T1039 | Access file shares | Bulk copy from finance share | Share access monitoring |
| Data Staged | T1074 | Stage data before exfil | Compress files to temp directory | Large file creation monitoring |
| Input Capture | T1056 | Keylogging | Keylogger capturing credentials | API monitoring, EDR |
| Email Collection | T1114 | Read/export email | Exchange mailbox export | Mailbox access auditing |
| Automated Collection | T1119 | Scripted data gathering | PowerShell script collecting files | Script execution monitoring |

### Tactic 11: Exfiltration (TA0010)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Exfil Over C2 Channel | T1041 | Send data through C2 | Upload via HTTPS beacon | DLP, traffic volume monitoring |
| Exfil Over Web Service | T1567 | Cloud storage, paste sites | Upload to Mega, Dropbox | CASB, proxy monitoring |
| Exfil Over Alternative Protocol | T1048 | DNS, ICMP tunneling | DNS TXT record exfiltration | DNS monitoring, NDR |
| Exfil to Cloud Storage | T1567.002 | AWS S3, Azure Blob | Upload to personal AWS account | Cloud DLP, CASB |
| Transfer Data to Cloud Account | T1537 | Use cloud account for staging | Create S3 bucket in attacker account | Cloud audit logs |

### Tactic 12: Impact (TA0040)

| Technique | ATT&CK ID | Description | Practical Example | Detection |
|-----------|-----------|-------------|-------------------|-----------|
| Data Encrypted for Impact | T1486 | Ransomware encryption | LockBit encrypting file servers | Canary files, EDR, backup monitoring |
| Data Destruction | T1485 | Wipe data/systems | Wiper malware (WhisperGate) | File integrity monitoring, backup alerts |
| Service Stop | T1489 | Stop critical services | Disable backup services before ransomware | Service monitoring |
| Inhibit System Recovery | T1490 | Delete backups, shadow copies | `vssadmin delete shadows /all` | EventID 7036, process monitoring |
| Defacement | T1491 | Modify website content | Deface company website | File integrity monitoring |
| Account Access Removal | T1531 | Lock out legitimate users | Mass password reset | Account change monitoring |

## Cross-References

- [Detection Coverage Matrix](../../frameworks/detection-coverage-matrix.md) -- coverage mapping
- [Adversary Simulation Framework](../../frameworks/adversary-simulation-framework.md) -- red team TTP usage
- [Sigma Rule Examples](../../swipe/detection/sigma-rule-examples.md) -- detection rules
- [Threat Actor Taxonomy](threat-actor-taxonomy.md) -- actor TTP profiles
