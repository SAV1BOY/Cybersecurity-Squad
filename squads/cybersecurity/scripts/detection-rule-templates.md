# Detection Rule Templates

## Purpose

Provide ready-to-use detection rule templates in industry-standard formats: Sigma (SIEM-agnostic), YARA (file/memory scanning), and Snort/Suricata (network detection). These templates cover common attack techniques mapped to MITRE ATT&CK, enabling rapid detection deployment for new threats.

## Formats Covered
- **Sigma**: SIEM-agnostic detection rules (convertible to Splunk, Elastic, Sentinel, etc.)
- **YARA**: Pattern-matching rules for files and memory
- **Snort/Suricata**: Network intrusion detection rules

---

## Sigma Rules

### Template Structure
```yaml
title: [Descriptive Title]
id: [UUID - generate with uuidgen]
status: [experimental|test|stable]
description: [What this rule detects and why it matters]
references:
    - [URL to technique documentation or advisory]
author: [Your name/team]
date: [YYYY/MM/DD]
modified: [YYYY/MM/DD]
tags:
    - attack.[tactic]
    - attack.t[technique_id]
logsource:
    category: [process_creation|network_connection|file_event|etc]
    product: [windows|linux|etc]
    service: [sysmon|security|etc]
detection:
    selection:
        [field]: [value]
    condition: selection
falsepositives:
    - [Known legitimate scenarios that may trigger]
level: [informational|low|medium|high|critical]
```

### Sigma: Suspicious PowerShell Encoded Command (T1059.001)

```yaml
title: Suspicious PowerShell Encoded Command Execution
id: 9d15044a-7154-4c01-b67e-7adc2f3a5e12
status: stable
description: Detects execution of PowerShell with encoded commands, commonly used by attackers to obfuscate malicious scripts.
references:
    - https://attack.mitre.org/techniques/T1059/001/
author: Cybersecurity Squad
date: 2026/03/06
tags:
    - attack.execution
    - attack.t1059.001
logsource:
    category: process_creation
    product: windows
detection:
    selection_powershell:
        Image|endswith:
            - '\powershell.exe'
            - '\pwsh.exe'
    selection_encoded:
        CommandLine|contains:
            - '-enc '
            - '-EncodedCommand'
            - '-ec '
            - '-encodedcommand'
    filter_legitimate:
        ParentImage|endswith:
            - '\sccm\\'
            - '\ccm\\'
    condition: selection_powershell and selection_encoded and not filter_legitimate
falsepositives:
    - Legitimate administration scripts using encoded commands
    - Configuration management tools (SCCM)
level: high
```

### Sigma: LSASS Memory Access (Credential Dumping - T1003.001)

```yaml
title: LSASS Memory Access by Non-System Process
id: b4f8c3d2-a91e-4f5c-b7d1-3e8c6a9f2b54
status: stable
description: Detects processes accessing LSASS memory, indicating credential dumping attempts (Mimikatz, ProcDump, etc.).
references:
    - https://attack.mitre.org/techniques/T1003/001/
author: Cybersecurity Squad
date: 2026/03/06
tags:
    - attack.credential_access
    - attack.t1003.001
logsource:
    category: process_access
    product: windows
detection:
    selection:
        TargetImage|endswith: '\lsass.exe'
        GrantedAccess|contains:
            - '0x1010'
            - '0x1038'
            - '0x1410'
            - '0x1438'
            - '0x1F0FFF'
            - '0x1F1FFF'
            - '0x1FFFFF'
    filter_system:
        SourceImage|endswith:
            - '\svchost.exe'
            - '\lsass.exe'
            - '\csrss.exe'
            - '\MsMpEng.exe'
            - '\vmtoolsd.exe'
            - '\MRT.exe'
    condition: selection and not filter_system
falsepositives:
    - Legitimate security software performing memory scanning
    - System management tools
level: critical
```

### Sigma: Shadow Copy Deletion (T1490)

```yaml
title: Shadow Copy Deletion via Command Line
id: c8f4a7e1-2b3d-4e9f-a6c5-1d2e3f4a5b6c
status: stable
description: Detects deletion of volume shadow copies, commonly performed before ransomware encryption to prevent recovery.
references:
    - https://attack.mitre.org/techniques/T1490/
author: Cybersecurity Squad
date: 2026/03/06
tags:
    - attack.impact
    - attack.t1490
logsource:
    category: process_creation
    product: windows
detection:
    selection_vssadmin:
        Image|endswith: '\vssadmin.exe'
        CommandLine|contains: 'delete shadows'
    selection_wmic:
        Image|endswith: '\wmic.exe'
        CommandLine|contains:
            - 'shadowcopy delete'
            - 'shadowcopy where'
    selection_powershell:
        Image|endswith:
            - '\powershell.exe'
            - '\pwsh.exe'
        CommandLine|contains:
            - 'Get-WmiObject Win32_ShadowCopy'
            - 'Remove-WmiObject'
            - 'Win32_ShadowCopy'
    selection_bcdedit:
        Image|endswith: '\bcdedit.exe'
        CommandLine|contains:
            - 'recoveryenabled no'
            - 'bootstatuspolicy ignoreallfailures'
    condition: selection_vssadmin or selection_wmic or selection_powershell or selection_bcdedit
falsepositives:
    - Legitimate backup software managing shadow copies
    - System administrators performing maintenance
level: critical
```

### Sigma: Suspicious Service Installation (T1543.003)

```yaml
title: Suspicious Windows Service Installation
id: d7e5f2a1-3c4b-5d6e-8f9a-0b1c2d3e4f5a
status: stable
description: Detects installation of Windows services from suspicious locations, indicating persistence or lateral movement.
references:
    - https://attack.mitre.org/techniques/T1543/003/
author: Cybersecurity Squad
date: 2026/03/06
tags:
    - attack.persistence
    - attack.t1543.003
logsource:
    product: windows
    service: system
detection:
    selection:
        EventID: 7045
    filter_suspicious_path:
        ImagePath|contains:
            - '\Temp\\'
            - '\tmp\\'
            - '\\AppData\\'
            - '\\Users\\Public\\'
            - '\\ProgramData\\'
            - 'cmd.exe /c'
            - 'powershell'
            - 'mshta'
    condition: selection and filter_suspicious_path
falsepositives:
    - Legitimate software installations in user directories
    - Configuration management deployments
level: high
```

### Sigma: DCSync Attack Detection (T1003.006)

```yaml
title: DCSync Attack - Directory Replication Request
id: e8f6a3b2-4d5c-6e7f-9a0b-1c2d3e4f5a6b
status: stable
description: Detects DCSync attacks where a non-domain controller requests directory replication, indicating credential theft via DRS.
references:
    - https://attack.mitre.org/techniques/T1003/006/
author: Cybersecurity Squad
date: 2026/03/06
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
            - '1131f6aa-9c07-11d1-f79f-00c04fc2dcd2'
            - '1131f6ad-9c07-11d1-f79f-00c04fc2dcd2'
            - '89e95b76-444d-4c62-991a-0facbeda640c'
    filter_dc:
        SubjectUserName|endswith: '$'
    condition: selection and not filter_dc
falsepositives:
    - Legitimate replication from domain controllers
    - Azure AD Connect synchronization
level: critical
```

## YARA Rules

### YARA: Cobalt Strike Beacon Detection

```yara
rule CobaltStrike_Beacon_Indicators
{
    meta:
        description = "Detects Cobalt Strike beacon indicators in memory or files"
        author = "Cybersecurity Squad"
        date = "2026-03-06"
        reference = "https://attack.mitre.org/software/S0154/"
        severity = "critical"

    strings:
        $pipe1 = "\\\\.\\pipe\\msagent_" ascii
        $pipe2 = "\\\\.\\pipe\\MSSE-" ascii
        $pipe3 = "\\\\.\\pipe\\postex_" ascii
        $pipe4 = "\\\\.\\pipe\\status_" ascii
        $config1 = { 00 01 00 01 00 02 ?? ?? 00 02 00 01 00 02 ?? ?? }
        $beacon_dll = "beacon.dll" ascii
        $beacon_x64 = "beacon.x64.dll" ascii
        $sleep_mask = { 4C 8B 53 08 45 8B 0A 45 8B 5A 04 4D 8D 52 08 45 85 C9 }
        $ua1 = "Mozilla/5.0 (compatible; MSIE" ascii
        $watermark = { 00 00 00 00 ?? ?? ?? ?? 00 00 00 00 }

    condition:
        uint16(0) == 0x5A4D and
        (
            2 of ($pipe*) or
            $config1 or
            any of ($beacon*) or
            ($sleep_mask and $ua1)
        )
}
```

### YARA: Web Shell Detection

```yara
rule Generic_WebShell_Indicators
{
    meta:
        description = "Detects common web shell indicators across PHP, JSP, and ASPX"
        author = "Cybersecurity Squad"
        date = "2026-03-06"
        severity = "high"

    strings:
        // PHP web shells
        $php1 = "<?php eval(" ascii nocase
        $php2 = "<?php assert(" ascii nocase
        $php3 = "<?php system(" ascii nocase
        $php4 = "<?php passthru(" ascii nocase
        $php5 = "<?php shell_exec(" ascii nocase
        $php6 = "base64_decode($_" ascii nocase
        $php7 = "gzinflate(base64_decode" ascii nocase
        $php8 = "str_rot13(" ascii nocase

        // JSP web shells
        $jsp1 = "Runtime.getRuntime().exec" ascii
        $jsp2 = "ProcessBuilder" ascii
        $jsp3 = "getParameter(\"cmd\")" ascii nocase

        // ASPX web shells
        $aspx1 = "Process.Start" ascii
        $aspx2 = "cmd.exe /c" ascii nocase
        $aspx3 = "Request[\"cmd\"]" ascii nocase
        $aspx4 = "Request.Form[\"" ascii

        // Generic indicators
        $gen1 = "whoami" ascii nocase
        $gen2 = "uname -a" ascii nocase
        $gen3 = "net user" ascii nocase

    condition:
        filesize < 500KB and
        (
            2 of ($php*) or
            2 of ($jsp*) or
            2 of ($aspx*) or
            (1 of ($php*, $jsp*, $aspx*) and 1 of ($gen*))
        )
}
```

### YARA: Ransomware Note Detection

```yara
rule Ransomware_Note_Generic
{
    meta:
        description = "Detects common ransomware note indicators"
        author = "Cybersecurity Squad"
        date = "2026-03-06"
        severity = "critical"

    strings:
        $ransom1 = "Your files have been encrypted" ascii nocase
        $ransom2 = "All your files are encrypted" ascii nocase
        $ransom3 = "decrypt your files" ascii nocase
        $ransom4 = "bitcoin" ascii nocase
        $ransom5 = "Tor browser" ascii nocase
        $ransom6 = "personal decryption" ascii nocase
        $ransom7 = "pay the ransom" ascii nocase
        $ransom8 = ".onion" ascii
        $ransom9 = "DO NOT try to decrypt" ascii nocase
        $ransom10 = "unique decryption key" ascii nocase

    condition:
        filesize < 100KB and 3 of them
}
```

## Snort/Suricata Rules

### Suricata: DNS Tunneling Detection

```
# DNS tunneling - high entropy subdomain queries
alert dns any any -> any any (msg:"SUSPICIOUS DNS Tunneling - High Entropy Subdomain"; dns.query; content:"."; pcre:"/^[a-zA-Z0-9]{30,}\./"; threshold:type both, track by_src, count 10, seconds 60; classtype:trojan-activity; sid:1000001; rev:1;)

# DNS tunneling - TXT record query volume
alert dns any any -> any any (msg:"SUSPICIOUS DNS TXT Record Query Volume"; dns.query; dns.type:16; threshold:type both, track by_src, count 20, seconds 60; classtype:trojan-activity; sid:1000002; rev:1;)
```

### Suricata: Beaconing Detection

```
# C2 beaconing - regular interval HTTP connections
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"SUSPICIOUS Potential C2 Beaconing - Regular HTTP"; flow:established,to_server; http.method; content:"GET"; threshold:type both, track by_src, count 30, seconds 300; classtype:trojan-activity; sid:1000003; rev:1;)
```

### Suricata: Exfiltration Detection

```
# Large outbound data transfer
alert tcp $HOME_NET any -> $EXTERNAL_NET any (msg:"POLICY Large Outbound Data Transfer"; flow:established,to_server; dsize:>1000000; threshold:type both, track by_src, count 5, seconds 60; classtype:policy-violation; sid:1000004; rev:1;)

# Data exfiltration via ICMP
alert icmp $HOME_NET any -> $EXTERNAL_NET any (msg:"SUSPICIOUS ICMP Tunnel - Large Payload"; dsize:>100; threshold:type both, track by_src, count 50, seconds 60; classtype:trojan-activity; sid:1000005; rev:1;)
```

### Suricata: Exploitation Indicators

```
# Log4Shell exploitation attempt
alert http any any -> $HOME_NET any (msg:"EXPLOIT Log4Shell JNDI Injection Attempt"; flow:established,to_server; content:"${jndi:"; nocase; fast_pattern; classtype:attempted-admin; sid:1000006; rev:1;)

# Web shell upload attempt
alert http any any -> $HOME_NET any (msg:"SUSPICIOUS Web Shell Upload Attempt"; flow:established,to_server; http.method; content:"POST"; http.uri; content:".php"; file.data; content:"<?php"; classtype:web-application-attack; sid:1000007; rev:1;)
```

## Sigma Rule Conversion

### Converting Sigma to Platform-Specific Rules
```bash
# Using sigmac or sigma-cli
# Convert to Splunk
sigma convert -t splunk -p sysmon rule.yml

# Convert to Elastic
sigma convert -t elasticsearch -p ecs-windows rule.yml

# Convert to Microsoft Sentinel
sigma convert -t microsoft365defender rule.yml

# Batch convert directory
sigma convert -t splunk -p sysmon -r rules_directory/
```

## Cross-References

- `workflows/detection-engineering-workflow.md` — Detection rule lifecycle
- `workflows/red-team-purple-team-cycle.md` — Detection validation
- `scripts/log-analysis-queries.md` — Investigation queries
- `frameworks/detection-coverage-matrix.md` — ATT&CK coverage tracking
- `data/registries/detection-rules-registry.md` — Rule registry
- `tasks/threat-intel/ioc-enrichment.md` — IOC-based rule creation
