# Windows Event IDs for Security Monitoring

## Purpose

Critical Windows Event ID reference for security monitoring, threat detection, and forensic investigation. Maps event IDs to MITRE ATT&CK techniques and provides detection guidance for SOC analysts and detection engineers.

## Authentication Events (Security Log)

### Logon Events

| Event ID | Description | Detection Use |
|----------|-------------|--------------|
| 4624 | Successful logon | Baseline legitimate access, detect anomalous logons |
| 4625 | Failed logon | Brute force detection, credential stuffing |
| 4634 | Logoff | Session duration analysis |
| 4647 | User-initiated logoff | Interactive session tracking |
| 4648 | Logon using explicit credentials (runas) | Lateral movement, credential use |
| 4672 | Special privileges assigned to logon | Admin logon tracking |
| 4768 | Kerberos TGT requested (AS-REQ) | Authentication tracking, AS-REP roasting |
| 4769 | Kerberos service ticket requested (TGS-REQ) | Kerberoasting detection |
| 4770 | Kerberos service ticket renewed | Persistent access tracking |
| 4771 | Kerberos pre-authentication failed | Password spraying detection |
| 4776 | NTLM authentication (success/failure) | Pass-the-hash, NTLM relay |

### Logon Type Reference

| Logon Type | Description | Security Context |
|-----------|-------------|-----------------|
| 2 | Interactive (console) | Physical or virtual console access |
| 3 | Network | SMB, mapped drives, lateral movement |
| 4 | Batch | Scheduled tasks |
| 5 | Service | Service account startup |
| 7 | Unlock | Workstation unlock |
| 8 | NetworkCleartext | IIS basic auth (cleartext password in transit) |
| 9 | NewCredentials | RunAs /netonly (credential use for network only) |
| 10 | RemoteInteractive | RDP |
| 11 | CachedInteractive | Cached domain credentials (offline logon) |

### Detection Rules

```
# Brute Force Detection
EventID=4625 | stats count by TargetUserName, IpAddress
| where count > 10 within 5 minutes

# Password Spraying (many users, few attempts each)
EventID=4625 | stats dc(TargetUserName) as unique_users count by IpAddress
| where unique_users > 10 AND count/unique_users < 3

# Kerberoasting
EventID=4769 TicketEncryptionType=0x17 (RC4)
| where ServiceName does not end with "$"

# Pass-the-Hash
EventID=4624 LogonType=3 AuthPackage=NTLM
| where LogonProcessName="NtLmSsp" AND not known_service_account
```

## Account Management Events

| Event ID | Description | Detection Use |
|----------|-------------|--------------|
| 4720 | User account created | Unauthorized account creation |
| 4722 | User account enabled | Dormant account activation |
| 4723 | Password change attempt | Credential manipulation |
| 4724 | Password reset attempt | Admin password reset abuse |
| 4725 | User account disabled | Account lifecycle tracking |
| 4726 | User account deleted | Evidence destruction |
| 4728 | Member added to security-enabled global group | Privilege escalation |
| 4732 | Member added to security-enabled local group | Local admin additions |
| 4735 | Security-enabled local group changed | Group policy manipulation |
| 4738 | User account changed | Account property modification |
| 4740 | User account locked out | Brute force indicator |
| 4756 | Member added to universal security group | Domain-wide privilege change |
| 4757 | Member removed from universal security group | Privilege change tracking |

### Critical Group Monitoring

```
Monitor additions to these groups (EventID 4728, 4732, 4756):
- Domain Admins
- Enterprise Admins
- Schema Admins
- Administrators (local)
- Backup Operators
- Account Operators
- DnsAdmins (can load arbitrary DLLs)
- Group Policy Creator Owners
```

## Process and Service Events

### Process Creation (Sysmon Event ID 1 / Security Event ID 4688)

| Event ID | Source | Description | Detection Use |
|----------|--------|-------------|--------------|
| 4688 | Security | Process creation | Command-line auditing (requires policy) |
| 4689 | Security | Process termination | Process lifecycle |
| 7045 | System | New service installed | Persistence, lateral movement |
| 7040 | System | Service start type changed | Persistence mechanism |

### Critical Process Monitoring

```
# Suspicious parent-child relationships
Alert when:
- winword.exe spawns cmd.exe/powershell.exe (macro execution)
- explorer.exe spawns csc.exe (dynamic compilation)
- services.exe spawns cmd.exe (service-based execution)
- svchost.exe spawns unusual child processes
- wmiprvse.exe spawns powershell.exe (WMI-based execution)

# LOLBin Execution
Monitor execution of:
- certutil.exe (download, encode/decode)
- mshta.exe (HTA execution)
- regsvr32.exe (COM scriptlet execution)
- rundll32.exe (DLL execution)
- bitsadmin.exe (download)
- wmic.exe (remote execution)
- msiexec.exe (MSI-based execution)
```

## PowerShell and Script Events

| Event ID | Log Source | Description |
|----------|-----------|-------------|
| 4103 | PowerShell Operational | Module logging |
| 4104 | PowerShell Operational | Script block logging (CRITICAL) |
| 4105 | PowerShell Operational | Script block start |
| 4106 | PowerShell Operational | Script block stop |

### PowerShell Detection

```
# Suspicious PowerShell patterns in Event ID 4104:
- "IEX" or "Invoke-Expression" (remote code execution)
- "DownloadString" or "DownloadFile" (payload download)
- "-enc" or "-EncodedCommand" (obfuscation)
- "FromBase64String" (deobfuscation)
- "Net.WebClient" (network download)
- "Reflection.Assembly" (in-memory loading)
- "AMSI" (AMSI bypass attempts)
```

## Sysmon Events (Supplement)

| Event ID | Description | Detection Use |
|----------|-------------|--------------|
| 1 | Process creation (with hash + parent) | Full process lineage |
| 3 | Network connection | Process-to-network mapping |
| 7 | Image loaded (DLL) | DLL sideloading detection |
| 8 | CreateRemoteThread | Process injection |
| 10 | ProcessAccess | Credential dumping (LSASS access) |
| 11 | FileCreate | File drop monitoring |
| 12-14 | Registry events | Persistence via registry |
| 17-18 | Pipe created/connected | Named pipe C2, lateral movement |
| 22 | DNSEvent | DNS query logging per process |
| 23 | FileDelete | Anti-forensics detection |
| 25 | ProcessTampering | Process hollowing/herpaderping |

## Audit Policy Requirements

```powershell
# Enable critical audit policies
auditpol /set /subcategory:"Logon" /success:enable /failure:enable
auditpol /set /subcategory:"Account Logon" /success:enable /failure:enable
auditpol /set /subcategory:"Account Management" /success:enable /failure:enable
auditpol /set /subcategory:"Process Creation" /success:enable
auditpol /set /subcategory:"Logoff" /success:enable

# Enable command-line in process creation events
# GPO: Computer Configuration > Administrative Templates > System > Audit Process Creation
# "Include command line in process creation events" = Enabled
```

## Cross-References

- See `reference/tools/splunk-reference.md` for SPL detection queries
- See `reference/tools/bloodhound-reference.md` for AD attack path analysis
- See `frameworks/detection-coverage-matrix.md` for MITRE ATT&CK mapping
- See `data/registries/linux-log-sources-registry.md` for Linux equivalent events
- See `workflows/detection-engineering-workflow.md` for rule development
