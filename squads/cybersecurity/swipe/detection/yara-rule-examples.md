# YARA Rule Examples

## Purpose

YARA rules for detecting malware families, suspicious patterns, and malicious documents. Covers rule structure, string pattern design, condition optimization, and performance considerations.

## YARA Rule Structure

```yara
rule RuleName : tag1 tag2
{
    meta:
        author = "Author"
        description = "What this rule detects"
        date = "2026-03-01"
        reference = "URL or report reference"
        hash = "Sample hash"
        tlp = "WHITE"
        severity = "critical|high|medium|low"

    strings:
        $string1 = "plain text"
        $hex1 = { 4D 5A 90 00 }
        $regex1 = /pattern[0-9]+/

    condition:
        uint16(0) == 0x5A4D and 2 of ($string*)
}
```

## Malware Family Rules

### Rule 1: Cobalt Strike Beacon Detection

```yara
rule CobaltStrike_Beacon_Strings
{
    meta:
        author = "Cybersecurity Squad"
        description = "Detects Cobalt Strike beacon payloads via characteristic strings"
        date = "2026-03-01"
        reference = "https://attack.mitre.org/software/S0154/"
        severity = "critical"
        tlp = "WHITE"

    strings:
        // Default Cobalt Strike named pipes
        $pipe1 = "\\\\.\\pipe\\msagent_" ascii
        $pipe2 = "\\\\.\\pipe\\MSSE-" ascii
        $pipe3 = "\\\\.\\pipe\\postex_" ascii
        $pipe4 = "\\\\.\\pipe\\postex_ssh_" ascii

        // Default CS beacon configuration strings
        $config1 = "%s as %s\\%s: %d" ascii
        $config2 = "beacon.x64.dll" ascii
        $config3 = "beacon.dll" ascii
        $config4 = "%02d/%02d/%02d %02d:%02d:%02d" ascii

        // Default malleable C2 URIs (common defaults)
        $uri1 = "/submit.php" ascii
        $uri2 = "/visit.js" ascii
        $uri3 = "/__utm.gif" ascii
        $uri4 = "/pixel" ascii

        // Reflective loader artifacts
        $loader1 = "ReflectiveLoader" ascii
        $loader2 = { 4D 5A 41 52 55 48 89 E5 }  // MZARUH.. (x64 reflective stub)

        // Sleep mask deobfuscation
        $sleep1 = "sleepMask" ascii wide

    condition:
        (uint16(0) == 0x5A4D or uint32(0) == 0x00905A4D) and
        (
            3 of ($pipe*) or
            2 of ($config*) or
            ($loader1 and 1 of ($config*)) or
            ($loader2 and 1 of ($uri*)) or
            4 of them
        )
}

/*
Performance Notes:
- The uint16(0) check prevents scanning non-PE files
- String matching is ordered by specificity (pipes > config > URIs)
- Named pipe strings are most reliable but can be customized
- Malleable C2 profiles change URI patterns; these catch defaults only
- For memory scanning, remove the MZ header check
*/
```

### Rule 2: Mimikatz Detection

```yara
rule Mimikatz_Strings
{
    meta:
        author = "Cybersecurity Squad"
        description = "Detects Mimikatz credential harvesting tool via unique strings"
        date = "2026-03-01"
        reference = "https://github.com/gentilkiwi/mimikatz"
        severity = "critical"

    strings:
        // Mimikatz module names
        $mod1 = "sekurlsa" ascii wide
        $mod2 = "kerberos" ascii wide
        $mod3 = "lsadump" ascii wide
        $mod4 = "dpapi" ascii wide

        // Mimikatz commands
        $cmd1 = "sekurlsa::logonpasswords" ascii wide nocase
        $cmd2 = "sekurlsa::wdigest" ascii wide nocase
        $cmd3 = "lsadump::dcsync" ascii wide nocase
        $cmd4 = "kerberos::golden" ascii wide nocase
        $cmd5 = "kerberos::ptt" ascii wide nocase
        $cmd6 = "privilege::debug" ascii wide nocase

        // Mimikatz author strings
        $author1 = "gentilkiwi" ascii wide
        $author2 = "benjamin@gentilkiwi.com" ascii wide
        $author3 = "Vincent LE TOUX" ascii wide

        // Mimikatz error/output strings
        $out1 = "* Username :" ascii wide
        $out2 = "* Domain   :" ascii wide
        $out3 = "* NTLM     :" ascii wide
        $out4 = "* SHA1     :" ascii wide
        $out5 = "wdigest KO" ascii wide

    condition:
        (
            2 of ($cmd*) or
            1 of ($author*) or
            (2 of ($mod*) and 2 of ($out*)) or
            3 of ($out*)
        )
}

/*
Performance Notes:
- No MZ header check to catch memory-only/injected Mimikatz
- Wide string variants catch Unicode encoding
- nocase for command strings catches case variations
- Author strings are most reliable but trivially removed
- Command strings are most operationally useful
*/
```

### Rule 3: Ransomware Indicators

```yara
rule Generic_Ransomware_Indicators
{
    meta:
        author = "Cybersecurity Squad"
        description = "Detects generic ransomware indicators: ransom notes, encryption behavior"
        date = "2026-03-01"
        severity = "critical"

    strings:
        // Common ransom note strings
        $ransom1 = "Your files have been encrypted" ascii wide nocase
        $ransom2 = "bitcoin" ascii wide nocase
        $ransom3 = "decrypt" ascii wide nocase
        $ransom4 = "ransom" ascii wide nocase
        $ransom5 = "your personal id" ascii wide nocase
        $ransom6 = ".onion" ascii wide
        $ransom7 = "tor browser" ascii wide nocase
        $ransom8 = "wallet address" ascii wide nocase

        // Volume shadow copy deletion
        $shadow1 = "vssadmin" ascii wide nocase
        $shadow2 = "delete shadows" ascii wide nocase
        $shadow3 = "wmic shadowcopy" ascii wide nocase
        $shadow4 = "bcdedit" ascii wide nocase
        $shadow5 = "recoveryenabled no" ascii wide nocase

        // Common encryption library markers
        $crypto1 = "CryptEncrypt" ascii
        $crypto2 = "CryptGenKey" ascii
        $crypto3 = "CryptImportKey" ascii
        $crypto4 = "RSA" ascii
        $crypto5 = "AES" ascii

        // File extension enumeration patterns
        $enum1 = ".doc" ascii
        $enum2 = ".xls" ascii
        $enum3 = ".pdf" ascii
        $enum4 = ".jpg" ascii
        $enum5 = ".sql" ascii
        $enum6 = ".mdb" ascii

    condition:
        uint16(0) == 0x5A4D and
        (
            (3 of ($ransom*) and 1 of ($shadow*)) or
            (2 of ($ransom*) and 2 of ($crypto*) and 3 of ($enum*)) or
            (2 of ($shadow*) and 2 of ($crypto*))
        )
}

/*
Performance Notes:
- MZ header check limits to PE files
- Condition requires combination of indicators to reduce false positives
- Shadow copy deletion + ransom note is high-confidence
- Crypto APIs alone are too noisy (legitimate software uses them)
- File extension lists help identify file-targeting behavior
*/
```

## Suspicious Document Rules

### Rule 4: Macro-Enabled Document with Suspicious Patterns

```yara
rule Suspicious_Office_Macro
{
    meta:
        author = "Cybersecurity Squad"
        description = "Detects Office documents with suspicious VBA macro patterns"
        date = "2026-03-01"
        severity = "high"

    strings:
        // Office magic bytes
        $ole_magic = { D0 CF 11 E0 A1 B1 1A E1 }

        // Suspicious VBA patterns
        $vba1 = "Shell" ascii wide
        $vba2 = "WScript.Shell" ascii wide
        $vba3 = "PowerShell" ascii wide nocase
        $vba4 = "Environ" ascii wide
        $vba5 = "URLDownloadToFile" ascii wide
        $vba6 = "CreateObject" ascii wide
        $vba7 = "AutoOpen" ascii wide
        $vba8 = "Document_Open" ascii wide
        $vba9 = "Workbook_Open" ascii wide
        $vba10 = "CallByName" ascii wide

        // Obfuscation indicators
        $obf1 = "Chr(" ascii wide
        $obf2 = "ChrW(" ascii wide
        $obf3 = "StrReverse" ascii wide
        $obf4 = "Replace(" ascii wide

        // Execution patterns
        $exec1 = "cmd /c" ascii wide nocase
        $exec2 = "cmd.exe" ascii wide nocase
        $exec3 = "certutil" ascii wide nocase
        $exec4 = "bitsadmin" ascii wide nocase
        $exec5 = "mshta" ascii wide nocase
        $exec6 = "regsvr32" ascii wide nocase

    condition:
        $ole_magic at 0 and
        1 of ($vba7, $vba8, $vba9) and   // Auto-execution trigger
        (
            (2 of ($vba1, $vba2, $vba3, $vba5, $vba6) and 1 of ($exec*)) or
            (2 of ($obf*) and 1 of ($exec*)) or
            ($vba5 and 1 of ($exec*))     // URLDownloadToFile + execution
        )
}

/*
Performance Notes:
- OLE magic byte check at offset 0 limits to OLE documents
- Auto-execution check (AutoOpen etc.) is essential for reducing FPs
- Obfuscation + execution is high confidence
- URLDownloadToFile is a strong indicator but may appear in legitimate macros
- For OOXML documents (.docx/.xlsx), check for ZIP magic and vbaProject.bin
*/
```

### Rule 5: Webshell Detection

```yara
rule Generic_Webshell
{
    meta:
        author = "Cybersecurity Squad"
        description = "Detects common webshell patterns in PHP, ASP, and JSP files"
        date = "2026-03-01"
        severity = "critical"

    strings:
        // PHP webshell indicators
        $php1 = "<?php eval(" ascii nocase
        $php2 = "<?php assert(" ascii nocase
        $php3 = "<?php system(" ascii nocase
        $php4 = "<?php passthru(" ascii nocase
        $php5 = "<?php shell_exec(" ascii nocase
        $php6 = "$_GET['cmd']" ascii nocase
        $php7 = "$_POST['cmd']" ascii nocase
        $php8 = "$_REQUEST['cmd']" ascii nocase
        $php9 = "base64_decode($_" ascii nocase
        $php10 = "gzinflate(base64_decode" ascii nocase
        $php11 = "preg_replace('/.*/" ascii

        // ASP/ASPX webshell indicators
        $asp1 = "eval(Request" ascii nocase
        $asp2 = "Execute(Request" ascii nocase
        $asp3 = "CreateObject(\"Wscript.Shell\")" ascii nocase
        $asp4 = "cmd.exe /c" ascii nocase
        $asp5 = "Process.Start" ascii nocase
        $asp6 = "Runtime.getRuntime().exec" ascii nocase

        // JSP webshell indicators
        $jsp1 = "Runtime.getRuntime().exec" ascii
        $jsp2 = "ProcessBuilder" ascii
        $jsp3 = "request.getParameter(\"cmd\")" ascii

        // Common webshell features
        $feat1 = "uname -a" ascii
        $feat2 = "whoami" ascii
        $feat3 = "file_get_contents" ascii
        $feat4 = "file_put_contents" ascii

    condition:
        filesize < 500KB and
        (
            2 of ($php*) or
            2 of ($asp*) or
            2 of ($jsp*) or
            (1 of ($php*, $asp*, $jsp*) and 2 of ($feat*))
        )
}

/*
Performance Notes:
- Filesize limit (500KB) eliminates large legitimate files
- False positives possible in development/test environments
- Deploy on web server directories specifically
- Combine with file integrity monitoring for new file detection
- For obfuscated webshells, add entropy calculation in external tooling
*/
```

## Performance Optimization Guidelines

| Technique | Benefit | Example |
|-----------|---------|---------|
| Magic byte check | Skip non-target file types | `uint16(0) == 0x5A4D` |
| Filesize limit | Skip oversized files | `filesize < 10MB` |
| String ordering | Fail fast on specific strings | Put rare strings first in condition |
| Hex patterns over regex | Faster matching | `{ 4D 5A }` vs `/MZ/` |
| Avoid excessive wildcards | Prevent backtracking | Use fixed-length wildcards `{4D 5A [2-4] 00}` |
| Module use | Efficient PE analysis | `pe.imports("kernel32.dll", "CreateRemoteThread")` |
| Tag organization | Rule management | Group by malware family, technique |

## Rule Testing Checklist

- [ ] Test against known malware samples (true positives)
- [ ] Test against clean file corpus (false positives)
- [ ] Measure scan performance (time per file, total scan time)
- [ ] Validate on target platform (Windows/Linux)
- [ ] Verify with multiple YARA versions
- [ ] Document known false positive sources
- [ ] Set appropriate severity and TLP

## Cross-References

- [Digital Forensics Methodology](../../frameworks/digital-forensics-methodology.md) -- evidence analysis
- [Sigma Rule Examples](sigma-rule-examples.md) -- host-based detection
- [Snort/Suricata Rules](snort-suricata-rules.md) -- network detection
- [Detection Coverage Matrix](../../frameworks/detection-coverage-matrix.md) -- coverage mapping
