# Live Memory Capture and Analysis Task

## Purpose

Capture and analyze volatile memory (RAM) from live systems to identify running malware, injected code, network connections, encryption keys, and other artifacts that exist only in memory and are lost upon system shutdown. Memory forensics is often the only way to detect fileless malware, process injection, and in-memory-only payloads.

## Task Owner
Digital forensics analyst with memory analysis expertise.

## Prerequisites
- Memory acquisition tools: WinPmem, LiME (Linux), MacPmem, Magnet RAM Capture, Belkasoft RAM Capturer
- Analysis framework: Volatility 3 (primary), Rekall (legacy), MemProcFS
- Sufficient storage for memory dumps (system RAM size + overhead)
- YARA rules for malware detection
- Symbol files for target OS version (Volatility ISF files)

---

## Phase 1: Memory Acquisition

### 1.1 Acquisition Planning
- [ ] Determine target system OS, version, and RAM size
- [ ] Select appropriate acquisition tool for the OS
- [ ] Prepare destination media (USB drive or network share with sufficient space)
- [ ] Ensure acquisition tool is pre-compiled and ready (do not install on target)
- [ ] Document system state before acquisition (uptime, running applications)

### 1.2 Critical Rule
**Memory acquisition must be performed BEFORE disk imaging or system shutdown.** Powering off the system destroys all volatile evidence. Every second of delay risks evidence loss through normal memory management.

### 1.3 Acquisition Methods

**Windows:**
```bash
# WinPmem (recommended, kernel driver-based)
winpmem_mini_x64.exe output.raw

# Magnet RAM Capture (GUI-based, minimal footprint)
# Launch MRC.exe, select output path, capture

# DumpIt (single-click acquisition)
DumpIt.exe
```

**Linux:**
```bash
# LiME (Linux Memory Extractor) - kernel module
sudo insmod lime.ko "path=/evidence/memory.lime format=lime"

# Using /proc/kcore (less reliable, may miss pages)
sudo dd if=/proc/kcore of=/evidence/memory.raw bs=1M
```

**macOS:**
```bash
# MacPmem (requires kernel extension approval)
sudo ./MacPmem -o /evidence/memory.raw
```

### 1.4 Acquisition Validation
- [ ] Verify dump file size approximately equals system RAM
- [ ] Calculate SHA-256 hash of memory dump immediately
- [ ] Record acquisition timestamp and tool version
- [ ] Document any errors during acquisition
- [ ] Transfer to forensic workstation for analysis

## Phase 2: Memory Analysis

### 2.1 Initial Profiling
Identify the operating system and memory layout:
```bash
# Volatility 3 - OS identification
vol -f memory.raw windows.info
vol -f memory.raw linux.info
vol -f memory.raw mac.info

# Verify kernel version and build information
vol -f memory.raw windows.info | grep -i "kernel\|build\|version"
```

### 2.2 Process Analysis
Identify running processes and their relationships:

```bash
# List all processes with PID, PPID, timestamps
vol -f memory.raw windows.pslist
vol -f memory.raw windows.pstree    # Tree view showing parent-child

# Find hidden processes (DKOM detection)
vol -f memory.raw windows.psscan    # Scans for EPROCESS structures
# Compare pslist vs psscan - differences indicate hidden processes

# Process command lines
vol -f memory.raw windows.cmdline

# Process environment variables
vol -f memory.raw windows.envars
```

**Analysis Focus:**
- [ ] Identify processes with suspicious names or unusual parent processes
- [ ] Check for processes running from temp directories, user profiles, or unusual paths
- [ ] Look for legitimate process names with wrong PID hierarchy (svchost.exe not child of services.exe)
- [ ] Identify processes with abnormally high memory usage
- [ ] Check process creation timestamps for anomalous timing

### 2.3 Code Injection Detection

```bash
# Detect injected code and hollowed processes
vol -f memory.raw windows.malfind

# Check for loaded DLLs per process
vol -f memory.raw windows.dlllist --pid [PID]

# Detect unlinked DLLs (loaded but hidden)
vol -f memory.raw windows.ldrmodules

# Check process memory protections (RWX regions are suspicious)
vol -f memory.raw windows.vadinfo --pid [PID]
```

**Analysis Focus:**
- [ ] MZ headers in non-image VAD regions (injected executables)
- [ ] Regions with PAGE_EXECUTE_READWRITE protection
- [ ] Processes with unlinked DLLs (InLoadOrder, InMemoryOrder, InInitOrder mismatches)
- [ ] Shellcode patterns in process memory
- [ ] Hollowed processes (legitimate image with replaced code)

### 2.4 Network Analysis

```bash
# Active network connections and listening sockets
vol -f memory.raw windows.netscan
vol -f memory.raw windows.netstat

# Linux equivalent
vol -f memory.raw linux.sockstat
```

**Analysis Focus:**
- [ ] Connections to known malicious IPs/domains
- [ ] Unexpected outbound connections from system processes
- [ ] Connections on unusual ports
- [ ] Multiple connections to the same destination (beaconing pattern)
- [ ] Correlate network connections with process list

### 2.5 Registry and Persistence Analysis (Windows)

```bash
# Registry hives from memory
vol -f memory.raw windows.registry.hivelist

# Check common persistence keys
vol -f memory.raw windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion\Run"
vol -f memory.raw windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion\RunOnce"

# Services
vol -f memory.raw windows.svcscan
```

### 2.6 Kernel-Level Analysis

```bash
# Loaded kernel drivers
vol -f memory.raw windows.driverscan
vol -f memory.raw windows.modules

# SSDT hooks (System Service Descriptor Table)
vol -f memory.raw windows.ssdt

# Callbacks
vol -f memory.raw windows.callbacks

# Linux kernel modules
vol -f memory.raw linux.lsmod
```

**Analysis Focus:**
- [ ] Unknown or unsigned kernel drivers
- [ ] Rootkit indicators (hooked functions, hidden modules)
- [ ] Recently loaded drivers (correlate with incident timeline)

### 2.7 Credential Extraction

```bash
# Windows credential extraction (for IR use only, under legal authority)
vol -f memory.raw windows.hashdump
vol -f memory.raw windows.lsadump
vol -f memory.raw windows.cachedump

# Search for cleartext credentials in memory
vol -f memory.raw windows.strings | grep -i "password\|credential"
```

**Note:** Credential extraction should only be performed for incident response purposes, under appropriate legal authorization, to identify compromised accounts requiring reset.

### 2.8 YARA Scanning

```bash
# Scan memory with YARA rules for known malware signatures
vol -f memory.raw yarascan --yara-rules /rules/malware_rules.yar
vol -f memory.raw yarascan --yara-rules /rules/webshells.yar
vol -f memory.raw yarascan --yara-rules /rules/cobalt_strike.yar
```

## Phase 3: Artifact Extraction

### 3.1 File Extraction
```bash
# Dump suspicious process executables
vol -f memory.raw windows.dumpfiles --pid [PID]

# Dump specific process memory
vol -f memory.raw windows.memmap --pid [PID] --dump

# Extract cached files from memory
vol -f memory.raw windows.filescan | grep -i ".exe\|.dll\|.ps1\|.bat"
```

### 3.2 Extracted Artifact Analysis
- [ ] Submit extracted executables to VirusTotal/sandbox
- [ ] Perform static analysis: strings, imports, entropy
- [ ] Identify packing or obfuscation
- [ ] Extract configuration data from malware (C2 addresses, encryption keys)
- [ ] Generate YARA rules from unique malware strings

## Phase 4: Reporting

### 4.1 Memory Forensics Report
Document findings including:
- [ ] System identification and memory acquisition details
- [ ] Suspicious processes with full analysis
- [ ] Injected code and malware identification
- [ ] Network connections of interest
- [ ] Persistence mechanisms discovered
- [ ] Credentials potentially compromised
- [ ] IOCs extracted (hashes, IPs, domains, strings)
- [ ] Timeline correlation with disk forensics

### 4.2 IOC Output
- [ ] Generate IOC list from memory analysis (hashes, mutex names, C2 addresses)
- [ ] Feed IOCs to enrichment pipeline (see `tasks/threat-intel/ioc-enrichment.md`)
- [ ] Create detection rules based on behavioral indicators found in memory

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Companion disk analysis
- `tasks/forensics/network-forensics.md` — Network evidence correlation
- `workflows/incident-response-workflow.md` — IR integration
- `scripts/forensic-triage-scripts.md` — Automated triage including memory
- `tasks/threat-intel/ioc-enrichment.md` — IOC processing from findings

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | evidence-standard, nist-800-61-incident-response |
| Checklists | forensics-collection-quality, evidence-chain-quality |
| Templates | reports/postmortem-template |
| Registry | data/registries/incident-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: chris-sanders + shannon-runner
