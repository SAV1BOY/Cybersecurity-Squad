# Disk Forensic Image Acquisition and Analysis Task

## Purpose

Provide a structured, forensically sound methodology for acquiring and analyzing disk images from compromised or suspect systems. Proper disk forensics preserves evidence integrity for incident response, legal proceedings, and root cause analysis while extracting maximum intelligence from storage media.

## Task Owner
Digital forensics analyst. All work must be conducted under direction of legal counsel when litigation or law enforcement involvement is anticipated.

## Prerequisites
- Forensic workstation with adequate storage (target disk size x 2.5 minimum)
- Write-blocker (hardware preferred: Tableau, CRU WiebeTech)
- Forensic imaging software (FTK Imager, dc3dd, ewfacquire)
- Analysis software (Autopsy, X-Ways Forensics, EnCase, Sleuth Kit)
- Chain of custody forms
- Sterile destination media (forensic-wiped drives)

---

## Phase 1: Evidence Acquisition

### 1.1 Pre-Acquisition Documentation
- [ ] Record date, time, timezone, and analyst name
- [ ] Photograph the system (front, back, serial numbers, connections)
- [ ] Document system state: powered on/off, screen contents, running indicators
- [ ] Record serial numbers, make, model of all storage media
- [ ] Note any connected external devices (USB, network cables)
- [ ] Initialize chain of custody form

### 1.2 Live System Considerations
If the system is powered on:
- [ ] Capture live memory FIRST before shutdown (see `tasks/forensics/memory-forensics.md`)
- [ ] Capture running process list, network connections, logged-in users
- [ ] Capture system time and compare to authoritative time source
- [ ] Document any encryption indicators (BitLocker, FileVault, LUKS)
- [ ] If full-disk encryption is active, image while system is live or capture keys
- [ ] Perform controlled shutdown (avoid normal shutdown if malware suspected)

### 1.3 Forensic Imaging
- [ ] Connect target drive to forensic workstation via hardware write-blocker
- [ ] Verify write-blocker is functioning (check indicator lights, test with write command)
- [ ] Create forensic image using validated tool:

**Preferred Formats:**
- E01 (EnCase Evidence File): compressed, supports metadata, industry standard
- Raw/dd: universal compatibility, no compression
- AFF4: open format with compression and metadata

**Imaging Command Examples:**
```bash
# Using dc3dd (enhanced dd with hashing)
dc3dd if=/dev/sdX of=/evidence/case001/disk.dd hash=sha256 log=/evidence/case001/imaging.log

# Using ewfacquire (E01 format)
ewfacquire /dev/sdX -t /evidence/case001/disk -f encase6 -c deflate -S 2G

# Using FTK Imager CLI
ftkimager /dev/sdX /evidence/case001/disk.E01 --e01 --compress 6
```

- [ ] Verify image integrity: compare source and image hash values
- [ ] Create a second copy of the image (working copy vs. evidence copy)
- [ ] Document hash values in chain of custody and case notes
- [ ] Store evidence copy in secure, access-controlled location

### 1.4 Chain of Custody
Maintain continuous chain of custody documentation:
```
Chain of Custody Record
========================
Case Number: [CASE-YYYY-NNN]
Evidence Item: [Description, serial number]
Acquired By: [Name, role]
Acquisition Date/Time: [ISO 8601]
Hash (SHA-256): [Hash value]
Storage Location: [Secure evidence locker, safe, etc.]

Transfer Log:
Date/Time | From | To | Purpose | Signature
```

## Phase 2: Forensic Analysis

### 2.1 Filesystem Analysis
- [ ] Mount image read-only on forensic workstation
- [ ] Identify filesystem type(s): NTFS, ext4, APFS, HFS+
- [ ] Recover deleted files and directory entries
- [ ] Identify hidden or alternate data streams (NTFS ADS)
- [ ] Examine file metadata (MAC timestamps: Modified, Accessed, Created/Changed)
- [ ] Identify suspicious files by location, name, or timestamp anomaly

### 2.2 Timeline Analysis
Build a comprehensive timeline of system activity:
- [ ] Extract filesystem timestamps (all files, including deleted)
- [ ] Parse event logs (Windows Event Log, syslog, application logs)
- [ ] Extract browser history and download records
- [ ] Parse prefetch files (Windows) for program execution evidence
- [ ] Extract shellbags, recent documents, jump lists (Windows)
- [ ] Parse bash/zsh history (Linux/macOS)
- [ ] Merge all timeline sources into unified chronological timeline

**Tools for timeline creation:**
```bash
# Using Sleuth Kit + Plaso
log2timeline.py /evidence/case001/timeline.plaso /evidence/case001/disk.E01
psort.py -o l2tcsv /evidence/case001/timeline.plaso -w /evidence/case001/timeline.csv
```

### 2.3 Artifact Analysis by OS

**Windows Artifacts:**
- [ ] Registry hives: SAM, SYSTEM, SOFTWARE, SECURITY, NTUSER.DAT, UsrClass.dat
- [ ] Event logs: Security, System, Application, PowerShell, Sysmon
- [ ] Prefetch files (program execution evidence with timestamps and count)
- [ ] Amcache.hve (program execution and installation history)
- [ ] ShimCache/AppCompatCache (program execution evidence)
- [ ] SRUM database (system resource usage monitoring)
- [ ] Windows Search database (ESE database)
- [ ] Recycle Bin contents ($I and $R files)
- [ ] Shadow copies (Volume Shadow Service)
- [ ] Scheduled tasks and services

**Linux Artifacts:**
- [ ] /var/log/ (auth.log, syslog, cron, daemon)
- [ ] /etc/passwd, /etc/shadow, /etc/group
- [ ] Crontab entries (user and system)
- [ ] SSH authorized_keys and known_hosts
- [ ] Shell history files (.bash_history, .zsh_history)
- [ ] /tmp and /dev/shm for staging artifacts
- [ ] Systemd service files and journal logs
- [ ] Package manager logs (apt, yum)

**macOS Artifacts:**
- [ ] Unified Logs (log show/log collect)
- [ ] Launch Agents and Launch Daemons
- [ ] Quarantine database
- [ ] Spotlight metadata
- [ ] KnowledgeC database (user activity)
- [ ] TCC database (privacy permissions)

### 2.4 Malware and Indicator Discovery
- [ ] Identify suspicious executables (entropy analysis, unsigned binaries)
- [ ] Extract and hash all executables for VirusTotal submission
- [ ] Search for known malware indicators (strings, YARA rules)
- [ ] Identify persistence mechanisms (autoruns, services, scheduled tasks)
- [ ] Analyze suspicious scripts (PowerShell, batch, Python, shell)
- [ ] Check for data staging artifacts (compressed archives, encrypted files)

## Phase 3: Reporting

### 3.1 Forensic Report Structure
```
1. Executive Summary
2. Scope and Objectives
3. Evidence Items (with chain of custody reference)
4. Methodology and Tools Used
5. Findings
   a. Timeline of Events
   b. Malware/Tool Analysis
   c. Data Access and Exfiltration Evidence
   d. Persistence Mechanisms
   e. Lateral Movement Evidence
6. Indicators of Compromise
7. Conclusions
8. Recommendations
9. Appendices (full timeline, hash lists, tool output)
```

### 3.2 Evidence Preservation
- [ ] Archive all forensic images and working files
- [ ] Maintain evidence per retention policy (typically 7 years for legal matters)
- [ ] Document final chain of custody disposition
- [ ] Store analysis notes and working files with case record

## Cross-References

- `tasks/forensics/memory-forensics.md` — Companion memory analysis
- `tasks/forensics/network-forensics.md` — Network evidence correlation
- `workflows/incident-response-workflow.md` — IR integration
- `workflows/insider-threat-investigation.md` — Insider investigation evidence
- `scripts/forensic-triage-scripts.md` — Automated triage scripts
