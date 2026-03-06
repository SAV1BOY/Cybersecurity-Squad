# Sigma Detection Rule Examples

## Purpose

High-fidelity Sigma detection rules covering lateral movement, credential access, persistence, and defense evasion. Includes tuning notes, false positive guidance, and ATT&CK mapping for each rule.

## Rule Structure Reference

```yaml
title: Rule name (concise, descriptive)
id: UUID
status: experimental | test | stable
description: Detailed description of what this detects
references:
    - https://relevant-reference-url
author: Author name
date: YYYY/MM/DD
modified: YYYY/MM/DD
tags:
    - attack.tactic
    - attack.technique_id
logsource:
    category: process_creation | network_connection | file_event | ...
    product: windows | linux | ...
    service: sysmon | security | ...
detection:
    selection:
        field: value
    condition: selection
falsepositives:
    - Known legitimate use case
level: informational | low | medium | high | critical
```

## Lateral Movement Rules

### Rule 1: PsExec Service Installation

```yaml
title: PsExec Service Installation
id: c462f537-a1e3-4b6e-8bfb-2c7a5b3d9e1f
status: stable
description: |
    Detects PsExec service installation on target host, indicating lateral
    movement via PsExec or similar tools. Monitors for the PSEXESVC service
    creation event.
references:
    - https://attack.mitre.org/techniques/T1021/002/
    - https://jpcertcc.github.io/ToolAnalysisResultSheet/details/PsExec.htm
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.lateral_movement
    - attack.t1021.002
    - attack.execution
    - attack.t1569.002
logsource:
    product: windows
    service: system
detection:
    selection:
        EventID: 7045
        ServiceName|contains:
            - 'PSEXESVC'
            - 'csexec'
            - 'paexec'
    condition: selection
falsepositives:
    - Legitimate IT administration using PsExec (should be rare and documented)
    - Inventory or patch management tools using PsExec-like mechanisms
level: high
---
# Tuning Notes:
# - Add allowlisted admin workstations to filter section if legitimate use exists
# - Correlate with EventID 4624 Type 3 logon from same timeframe
# - Consider alerting on ANY 7045 (new service) from non-standard installers
# - Pair with Sysmon EventID 1 for process creation context
```

### Rule 2: WMI Remote Process Creation

```yaml
title: WMI Remote Process Creation via WMIC
id: 8a2b4c6d-e8f0-1234-5678-9abcdef01234
status: stable
description: |
    Detects use of wmic.exe to create processes on remote systems, a common
    lateral movement technique. Monitors for wmic process call create with
    /node parameter.
references:
    - https://attack.mitre.org/techniques/T1047/
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.lateral_movement
    - attack.execution
    - attack.t1047
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        Image|endswith: '\wmic.exe'
        CommandLine|contains|all:
            - '/node:'
            - 'process'
            - 'call'
            - 'create'
    condition: selection
falsepositives:
    - IT automation scripts using WMI for remote management
    - SCCM or similar management tools
level: high
---
# Tuning Notes:
# - Filter by source user: admin accounts performing WMI are less suspicious
# - Correlate with destination host WMI provider events (EventID 5857-5861)
# - High volume from single source = likely automation (investigate but may be legit)
# - Unusual parent processes (not cmd.exe/powershell.exe) increase confidence
```

## Credential Access Rules

### Rule 3: LSASS Memory Access

```yaml
title: Suspicious LSASS Memory Access
id: 3d4e5f6a-7b8c-9d0e-1f2a-3b4c5d6e7f8a
status: stable
description: |
    Detects processes accessing LSASS memory, which may indicate credential
    dumping via Mimikatz, comsvcs.dll, or custom tools. Uses Sysmon
    ProcessAccess events.
references:
    - https://attack.mitre.org/techniques/T1003/001/
    - https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.credential_access
    - attack.t1003.001
logsource:
    product: windows
    category: process_access
detection:
    selection:
        TargetImage|endswith: '\lsass.exe'
        GrantedAccess|contains:
            - '0x1010'  # PROCESS_QUERY_LIMITED_INFORMATION + PROCESS_VM_READ
            - '0x1410'
            - '0x1438'
            - '0x143a'
            - '0x1fffff'  # PROCESS_ALL_ACCESS
    filter_legitimate:
        SourceImage|endswith:
            - '\MsMpEng.exe'       # Windows Defender
            - '\csrss.exe'
            - '\lsass.exe'
            - '\wmiprvse.exe'
            - '\svchost.exe'
            - '\taskmgr.exe'
            - '\procexp64.exe'
    filter_specific:
        SourceImage|startswith:
            - 'C:\Program Files\CrowdStrike\'
            - 'C:\Program Files\SentinelOne\'
            - 'C:\Program Files (x86)\Symantec\'
    condition: selection and not (filter_legitimate or filter_specific)
falsepositives:
    - Antivirus/EDR scanning LSASS (add to filter_specific)
    - System administration tools that query process information
    - Performance monitoring tools
level: critical
---
# Tuning Notes:
# - This is a HIGH-VALUE rule -- tune carefully to minimize false positives
# - Add your EDR/AV paths to filter_specific
# - GrantedAccess 0x1fffff (PROCESS_ALL_ACCESS) is almost always malicious
# - Correlate with Sysmon EventID 10 for full process access context
# - Consider enabling Credential Guard to mitigate this attack entirely
```

### Rule 4: DCSync Attack Detection

```yaml
title: DCSync Attack - Directory Replication Request
id: 9e8d7c6b-5a4f-3e2d-1c0b-a9876543210f
status: stable
description: |
    Detects DCSync attacks by monitoring for directory replication service
    (DRS) requests from non-domain controller sources. Attackers with
    Replicating Directory Changes privileges can extract password hashes.
references:
    - https://attack.mitre.org/techniques/T1003/006/
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.credential_access
    - attack.t1003.006
logsource:
    product: windows
    service: security
detection:
    selection:
        EventID: 4662
        Properties|contains:
            - '1131f6aa-9c07-11d1-f79f-00c04fc2dcd2'  # DS-Replication-Get-Changes
            - '1131f6ad-9c07-11d1-f79f-00c04fc2dcd2'  # DS-Replication-Get-Changes-All
    filter_dc:
        SubjectUserName|endswith: '$'
        SubjectUserName|startswith:
            - 'DC01'  # Replace with your DC hostnames
            - 'DC02'
    condition: selection and not filter_dc
falsepositives:
    - Azure AD Connect service account (add to filter)
    - Legitimate replication monitoring tools
level: critical
---
# Tuning Notes:
# - CRITICAL: Update filter_dc with ALL domain controller computer accounts
# - Azure AD Connect uses replication -- add its service account to filter
# - Any hit from a non-DC should be treated as critical and investigated immediately
# - Correlate with 4624 logon events for the source account
```

## Persistence Rules

### Rule 5: Scheduled Task Creation via Command Line

```yaml
title: Scheduled Task Creation for Persistence
id: a1b2c3d4-5678-90ab-cdef-123456789abc
status: stable
description: |
    Detects creation of scheduled tasks via schtasks.exe, which is commonly
    used by attackers for persistence. Focuses on suspicious characteristics
    like SYSTEM-level execution and encoded commands.
references:
    - https://attack.mitre.org/techniques/T1053/005/
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.persistence
    - attack.t1053.005
    - attack.execution
logsource:
    category: process_creation
    product: windows
detection:
    selection_create:
        Image|endswith: '\schtasks.exe'
        CommandLine|contains: '/create'
    suspicious_indicators:
        CommandLine|contains:
            - '/sc onstart'
            - '/sc onlogon'
            - '/ru SYSTEM'
            - '/ru "NT AUTHORITY\SYSTEM"'
            - 'powershell'
            - 'encodedcommand'
            - 'bypass'
            - 'cmd /c'
            - 'mshta'
            - 'wscript'
            - 'cscript'
            - 'regsvr32'
            - 'rundll32'
    condition: selection_create and suspicious_indicators
falsepositives:
    - IT automation creating legitimate scheduled tasks
    - Software installation creating update tasks
    - SCCM/Intune creating management tasks
level: high
---
# Tuning Notes:
# - Correlate with Task Scheduler EventID 106 (task created) for enrichment
# - Filter known IT automation by ParentImage or specific CommandLine patterns
# - Tasks pointing to temp directories or user profiles are more suspicious
# - Combine with registry monitoring for HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule
```

### Rule 6: Registry Run Key Persistence

```yaml
title: Suspicious Registry Run Key Modification
id: b2c3d4e5-6789-0abc-def1-23456789abcd
status: stable
description: |
    Detects modification of registry Run/RunOnce keys for persistence.
    Filters known legitimate software to focus on suspicious additions.
references:
    - https://attack.mitre.org/techniques/T1547/001/
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.persistence
    - attack.t1547.001
logsource:
    category: registry_set
    product: windows
detection:
    selection:
        TargetObject|contains:
            - '\Software\Microsoft\Windows\CurrentVersion\Run'
            - '\Software\Microsoft\Windows\CurrentVersion\RunOnce'
            - '\Software\Microsoft\Windows\CurrentVersion\RunServices'
    filter_legitimate:
        Details|contains:
            - 'SecurityHealth'
            - 'WindowsDefender'
            - 'OneDrive'
            - 'Teams'
            - 'Outlook'
    filter_paths:
        Details|startswith:
            - '"C:\Program Files\'
            - '"C:\Program Files (x86)\'
    condition: selection and not (filter_legitimate or filter_paths)
falsepositives:
    - New software installation adding legitimate startup entries
    - User-installed applications
level: medium
---
# Tuning Notes:
# - Start with medium level, elevate to high after tuning out legitimate entries
# - Focus on entries pointing to unusual locations (AppData, Temp, ProgramData)
# - Encoded PowerShell or cmd.exe wrappers are high-confidence indicators
# - Correlate with file creation events for the referenced executable
```

## Defense Evasion Rules

### Rule 7: Event Log Clearing

```yaml
title: Security Event Log Cleared
id: c3d4e5f6-7890-abcd-ef12-3456789abcde
status: stable
description: |
    Detects clearing of Windows Security event log, commonly performed by
    attackers to cover tracks. This should be extremely rare in normal operations.
references:
    - https://attack.mitre.org/techniques/T1070/001/
author: Cybersecurity Squad
date: 2026/03/01
tags:
    - attack.defense_evasion
    - attack.t1070.001
logsource:
    product: windows
    service: security
detection:
    selection:
        EventID: 1102
    condition: selection
falsepositives:
    - Legitimate log rotation (should use archival, not clearing)
    - System rebuilds or reimaging
level: critical
---
# Tuning Notes:
# - This rule should have near-zero false positives in mature environments
# - Log clearing should NEVER happen in production -- investigate every alert
# - Also monitor EventID 104 (System log cleared) in System channel
# - Forward logs to SIEM before they can be cleared locally
# - Enable "Audit Audit Policy Change" for additional coverage
```

## Cross-References

- [Detection Coverage Matrix](../../frameworks/detection-coverage-matrix.md) -- ATT&CK mapping
- [Detection Engineering Workflow](../../workflows/detection-engineering-workflow.md) -- rule lifecycle
- [KQL Hunting Queries](kql-hunting-queries.md) -- Microsoft Sentinel queries
- [SPL Hunting Queries](spl-hunting-queries.md) -- Splunk queries
