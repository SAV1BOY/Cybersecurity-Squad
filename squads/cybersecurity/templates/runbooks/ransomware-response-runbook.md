# Ransomware Incident Response Runbook

## Purpose

Step-by-step operational runbook for responding to ransomware incidents. Covers detection, containment, eradication, recovery, and strategic decision-making including payment considerations for incident commanders and responders.

## Severity: ALWAYS CRITICAL

All confirmed ransomware incidents are treated as Critical severity with immediate response activation.

---

## Phase 0: Immediate Actions (First 15 Minutes)

### DO IMMEDIATELY

- [ ] **Activate incident response team** (all hands)
- [ ] **Isolate confirmed infected systems** (pull network cables, disable WiFi, quarantine via EDR)
- [ ] **DO NOT power off encrypted systems** (preserve memory for forensic evidence and potential key recovery)
- [ ] **Preserve evidence** (do not wipe or reimage yet)
- [ ] **Screenshot ransom notes** on all affected systems
- [ ] **Document the exact time** of detection and first observed encryption

### DO NOT

- Do NOT communicate over potentially compromised channels (assume attacker has email access)
- Do NOT contact the attacker without legal counsel approval
- Do NOT pay ransom without executive and legal decision
- Do NOT restore from backups until you understand the attack vector
- Do NOT announce publicly until legal and PR are aligned

---

## Phase 1: Assessment (15-60 Minutes)

### Step 1.1: Determine Scope

```
1. How many systems are encrypted? (count endpoint alerts, user reports)
2. Which networks/segments are affected?
3. Are domain controllers compromised?
4. Are backup systems affected?
5. Is encryption still actively spreading?
6. What data was on affected systems?
```

### Step 1.2: Identify Ransomware Variant

| Indicator | How to Check |
|-----------|-------------|
| Ransom note filename | e.g., `README.txt`, `DECRYPT_INSTRUCTIONS.html` |
| File extension | e.g., `.locked`, `.encrypted`, `.ryuk` |
| Encryption behavior | Files renamed, extensions changed, shadow copies deleted |
| Ransom note content | Bitcoin address, Tor link, timer |

Use: [ID Ransomware](https://id-ransomware.malwarehunterteam.com/) or [No More Ransom](https://www.nomoreransom.org/) to identify variant and check for available decryptors.

### Step 1.3: Assess Business Impact

| System Category | Status | Business Impact |
|----------------|--------|----------------|
| Domain controllers | [Affected/Safe] | [Authentication, all IT services] |
| Email systems | [Affected/Safe] | [Communication] |
| ERP/Financial systems | [Affected/Safe] | [Revenue, operations] |
| Customer-facing systems | [Affected/Safe] | [Revenue, reputation] |
| Backup infrastructure | [Affected/Safe] | [Recovery capability] |
| Safety/OT systems | [Affected/Safe] | [Physical safety] |

---

## Phase 2: Containment (1-4 Hours)

### Step 2.1: Network Containment

- [ ] Isolate affected network segments at switch/firewall level
- [ ] Block lateral movement ports (SMB 445, RDP 3389, WinRM 5985-5986)
- [ ] Disable compromised accounts (especially admin/service accounts)
- [ ] Block C2 infrastructure (known attacker IPs/domains)
- [ ] Disable VPN access until investigation determines entry point
- [ ] Consider isolating entire environment if spread is uncontrolled

### Step 2.2: Identity Containment

- [ ] Reset KRBTGT password (twice, 12+ hours apart, to invalidate all Kerberos tickets)
- [ ] Reset all domain admin passwords
- [ ] Reset all service account passwords
- [ ] Disable any suspicious new accounts
- [ ] Review and remove unauthorized group memberships

### Step 2.3: Preserve Evidence

```
For each affected system:
1. Memory capture (if system is still running)
   - Use WinPMem, DumpIt, or Magnet RAM Capture
2. Disk image (after memory capture)
   - Full forensic image to external drive
3. Log collection
   - Security event logs
   - System event logs
   - PowerShell logs
   - EDR telemetry
4. Network captures
   - Firewall logs
   - NetFlow data
   - DNS query logs
```

---

## Phase 3: Investigation (4-48 Hours)

### Step 3.1: Determine Entry Vector

| Common Entry Vectors | Investigation Steps |
|---------------------|-------------------|
| Phishing email | Search email logs for delivery, analyze attachments |
| Exposed RDP | Check for brute force in auth logs, check for exposed RDP ports |
| VPN credential compromise | Review VPN logs for anomalous logins |
| Exploited vulnerability | Check for unpatched internet-facing services |
| Supply chain compromise | Review recent software deployments and updates |
| Insider threat | Review user activity logs, physical access |

### Step 3.2: Determine Dwell Time

```
Attackers typically establish presence days to weeks before encryption.
Investigate:
1. When was first unauthorized access?
2. What reconnaissance was performed?
3. Were credentials harvested (Mimikatz, DCSync)?
4. Was data exfiltrated before encryption (double extortion)?
5. Were backups targeted and destroyed?
6. What persistence mechanisms were deployed?
```

### Step 3.3: Data Exfiltration Assessment

```
CRITICAL: Determine if data was exfiltrated (double extortion)
1. Check for large outbound data transfers (NetFlow, proxy logs)
2. Check for archive creation (7z, rar, zip) on compromised systems
3. Check for use of exfiltration tools (rclone, megasync, filezilla)
4. Check for cloud storage access (Mega, Google Drive, Dropbox)
5. If exfiltrated: identify what data was taken (triggers breach notification)
```

---

## Phase 4: Eradication (24-72 Hours)

### Step 4.1: Identify All Compromised Systems

- [ ] Complete scan of all endpoints for IOCs
- [ ] Review all domain controllers for backdoors
- [ ] Check for scheduled tasks, services, registry persistence
- [ ] Verify backup integrity (are backups clean?)

### Step 4.2: Clean Environment

- [ ] Rebuild compromised systems from known-good images
- [ ] Rebuild domain controllers if compromised (forest recovery)
- [ ] Apply patches that address the entry vector
- [ ] Harden configurations before reconnecting

---

## Phase 5: Recovery (Days to Weeks)

### Step 5.1: Backup Verification

- [ ] Identify most recent clean backup (pre-compromise)
- [ ] Test backup integrity in isolated environment
- [ ] Prioritize recovery order by business criticality

### Step 5.2: Recovery Order

| Priority | Systems | Target RTO |
|----------|---------|-----------|
| 1 | Domain controllers, DNS, DHCP | [Hours] |
| 2 | Email, communication systems | [Hours] |
| 3 | Core business applications | [Hours-Days] |
| 4 | Financial/ERP systems | [Days] |
| 5 | User workstations | [Days-Weeks] |
| 6 | Non-critical systems | [Weeks] |

### Step 5.3: Hardening Before Reconnection

- [ ] Patch all known vulnerabilities before systems go live
- [ ] Implement MFA on all remote access
- [ ] Deploy EDR on all endpoints
- [ ] Enable enhanced logging and monitoring
- [ ] Segment network based on risk zones
- [ ] Test detection rules for the specific TTPs used

---

## Phase 6: Ransom Payment Decision

### Decision Framework

**This decision involves executive leadership, legal counsel, cyber insurance, and law enforcement.**

| Factor | Consideration |
|--------|--------------|
| Backup availability | Can we recover without paying? |
| Decryptor reliability | Do victims report working decryptors for this variant? |
| Data exfiltration | Will payment prevent data publication? (often not guaranteed) |
| Legal restrictions | Is this group sanctioned (OFAC)? Payment may be illegal. |
| Insurance coverage | Does policy cover ransom payment? |
| Precedent | Payment funds future attacks |
| Law enforcement | FBI/CISA may have decryptor or ongoing investigation |

### Report to Law Enforcement

- [ ] FBI IC3 (ic3.gov) or local FBI field office
- [ ] CISA (cisa.gov/report)
- [ ] Relevant ISAC for your industry

---

## Phase 7: Post-Incident (Within 14 Days)

- [ ] Complete incident report
- [ ] Blameless post-incident review
- [ ] Update incident response plan based on lessons learned
- [ ] Brief executive leadership and board
- [ ] Notify regulators and affected parties if data was exfiltrated (see breach notification template)
- [ ] Implement long-term security improvements

---

## Cross-References

- See `frameworks/nist-800-61-incident-response.md` for IR framework
- See `workflows/incident-response-workflow.md` for general IR process
- See `templates/communications/breach-notification-template.md` for notifications
- See `reference/psychology/decision-making-under-pressure.md` for crisis decisions
- See `templates/runbooks/cloud-incident-runbook.md` for cloud-specific ransomware
