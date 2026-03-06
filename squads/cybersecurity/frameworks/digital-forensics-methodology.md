# Digital Forensics Methodology

## Purpose

Structured digital forensics methodology ensuring evidence integrity, legal admissibility, and thorough analysis. Covers the complete forensic lifecycle from identification through presentation, with chain of custody controls.

## Forensic Principles

1. **Preserve the original** -- Never work directly on original evidence
2. **Document everything** -- Every action, decision, and finding must be recorded
3. **Maintain chain of custody** -- Unbroken, documented evidence handling
4. **Use validated tools** -- Forensic tools must be tested and accepted
5. **Reproducibility** -- Another examiner should reach the same conclusions
6. **Proportionality** -- Scope of examination must be proportionate to the incident

## Phase 1: Identification

### Evidence Source Identification

| Source Type | Examples | Volatility |
|------------|---------|------------|
| Memory (RAM) | Running processes, network connections, encryption keys | Highest |
| Network traffic | Active sessions, DNS cache, ARP table | High |
| Running processes | Process list, open files, loaded modules | High |
| Temporary files | Swap, temp dirs, browser cache | Medium |
| Disk storage | File systems, deleted files, slack space | Low |
| Log files | System logs, application logs, audit trails | Low |
| Cloud artifacts | API logs, storage access logs, IAM events | Low (but may expire) |
| Mobile devices | App data, call logs, messages, location | Low |
| Network devices | Firewall logs, flow data, DHCP leases | Variable |

### Order of Volatility (RFC 3227)
1. CPU registers and cache
2. Routing tables, ARP cache, process tables, kernel statistics
3. Memory (RAM)
4. Temporary file systems
5. Disk storage
6. Remote logging and monitoring data
7. Physical configuration and network topology
8. Archival media

## Phase 2: Preservation

### Live System Preservation

```
Priority Actions (before shutdown):
1. Record date/time and timezone
2. Capture RAM (using DumpIt, WinPMEM, LiME)
3. Capture network state (netstat, routing table, ARP)
4. Capture running processes (process list, loaded DLLs)
5. Capture logged-on users and active sessions
6. DO NOT shutdown -- pull power plug (prevents shutdown scripts)
   Exception: Encrypted volumes that will lock -- coordinate with legal
```

### Disk Imaging

| Method | Tool | Verification | Use Case |
|--------|------|-------------|----------|
| Bit-for-bit image | dd, dc3dd, FTK Imager | MD5 + SHA-256 dual hash | Standard forensic image |
| Logical image | FTK Imager, X-Ways | Hash of each file | When full image not feasible |
| Targeted collection | KAPE, CyLR, Velociraptor | Hash manifest | Remote/triage collection |
| Cloud snapshot | AWS EBS snapshot, Azure disk snapshot | Provider hash + analyst verification | Cloud workloads |

### Write Blocking
- Hardware write blocker required for physical media
- Software write blocking acceptable for virtual/cloud only if validated
- Verify write blocker functionality before each use with test media
- Document write blocker serial number and validation in case notes

## Phase 3: Collection

### Collection Standards

| Requirement | Standard | Documentation |
|-------------|----------|--------------|
| Evidence container | Antistatic bags, tamper-evident seals | Photograph sealed evidence |
| Labeling | Unique evidence ID, date, collector, description | Evidence label form |
| Transportation | Secure transport, no extreme temperatures | Transport log |
| Storage | Locked evidence room/safe, access log | Storage log |
| Digital evidence | Encrypted storage, access controls | Access log |

### Chain of Custody Form

```
Evidence ID: [unique identifier]
Case Number: [case ID]
Description: [item description, serial numbers, model]
Date/Time Collected: [timestamp UTC]
Collected By: [name, title]
Location Collected: [physical/logical location]
Hash Values: MD5: [hash] | SHA-256: [hash]

Transfer Log:
| Date/Time | Released By | Received By | Purpose | Location |
|-----------|------------|-------------|---------|----------|
| [timestamp] | [name] | [name] | [reason] | [location] |
```

## Phase 4: Examination

### Filesystem Analysis

| Artifact | Location (Windows) | Location (Linux) | Intelligence Value |
|----------|-------------------|-------------------|-------------------|
| Timeline (MFT/inode) | $MFT, $UsnJrnl | inode timestamps | File creation, modification, access |
| Deleted files | Unallocated space, $Recycle.Bin | unlinked inodes, journal | Destroyed evidence recovery |
| Prefetch | C:\Windows\Prefetch | N/A | Program execution history |
| Event logs | C:\Windows\System32\winevt | /var/log/ | System events, authentication |
| Registry | C:\Windows\System32\config | N/A | Configuration, persistence, USB history |
| Browser artifacts | AppData\Local\[browser] | ~/.mozilla, ~/.config | Web activity, downloads |
| Shellbags | NTUSER.DAT, UsrClass.dat | N/A | Folder access history |
| SRUM | C:\Windows\System32\sru | N/A | Application resource usage |

### Memory Analysis

| Artifact | Tool/Plugin | Intelligence Value |
|----------|------------|-------------------|
| Process list | Volatility pslist, psscan | Running/hidden processes |
| Network connections | Volatility netscan | Active C2 connections |
| DLL injection | Volatility dlllist, ldrmodules | Code injection detection |
| Command history | Volatility cmdscan, consoles | Attacker commands |
| Registry hives | Volatility hivelist, printkey | In-memory registry (may differ from disk) |
| Encryption keys | Volatility bitlocker, truecrypt | Decrypt locked volumes |
| Malware strings | Volatility yarascan | IOC extraction from memory |

## Phase 5: Analysis

### Analysis Approaches

| Approach | Method | When to Use |
|----------|--------|------------|
| Timeline analysis | Create super-timeline (plaso/log2timeline) | Understanding sequence of events |
| Keyword searching | Index and search for terms | Finding specific data or IOCs |
| Hash analysis | Compare against known-good/known-bad | Identifying known malware or OS files |
| Signature analysis | YARA rules, AV scanning | Malware identification |
| Behavioral analysis | Sandbox execution, API monitoring | Unknown malware analysis |
| Network analysis | PCAP review, flow analysis | C2 communication, exfiltration |
| Log correlation | SIEM, manual timeline merge | Multi-source event reconstruction |

### Anti-Forensics Detection

| Technique | Indicators | Counter-Measures |
|-----------|-----------|-----------------|
| Timestomping | $STDINFO != $FILENAME timestamps in MFT | Compare MFT entries, use $UsnJrnl |
| Log clearing | Event ID 1102 (Windows), empty auth.log | Remote log collection, SIEM |
| Secure deletion | Overwrite patterns, wiping tool artifacts | Recover from VSS, journal, slack space |
| Steganography | Unusual file sizes, entropy analysis | Steg detection tools, entropy scanning |
| Encryption | Encrypted volumes, containers | Memory analysis for keys, legal compulsion |
| Process hollowing | Suspicious parent-child, memory anomalies | Memory analysis, process comparison |

## Phase 6: Presentation

### Forensic Report Structure

1. **Executive Summary** -- Non-technical overview, key findings, impact
2. **Scope and Authorization** -- Legal authority, scope of examination
3. **Evidence Inventory** -- All evidence items with chain of custody
4. **Methodology** -- Tools used, procedures followed, validation
5. **Findings** -- Detailed technical findings with supporting evidence
6. **Timeline** -- Chronological reconstruction of events
7. **Conclusions** -- Analyst opinions based on evidence
8. **Appendices** -- Hash values, tool output, raw data

### Legal Admissibility Checklist

- [ ] Evidence collected under proper legal authority
- [ ] Chain of custody unbroken and documented
- [ ] Write blocking used and verified
- [ ] Forensic images verified with cryptographic hashes
- [ ] Tools are industry-accepted and validated
- [ ] Examiner is qualified and can testify to methods
- [ ] Documentation supports independent reproduction
- [ ] Findings are based on evidence, not speculation

## Cross-References

- [Incident Response Workflow](../workflows/incident-response-workflow.md) -- IR integration
- [Incident Severity Classification](incident-severity-classification.md) -- severity definitions
- [YARA Rule Examples](../swipe/detection/yara-rule-examples.md) -- malware signatures
- [Insider Threat Runbook](../swipe/runbooks/insider-threat-runbook.md) -- insider investigation
