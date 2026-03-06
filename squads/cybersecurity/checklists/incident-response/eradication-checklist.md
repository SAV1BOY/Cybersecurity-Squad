# Incident Eradication Checklist

## Purpose / When to Use

Execute this checklist after containment is confirmed and the full scope of compromise is understood. Eradication removes all attacker footholds, persistence mechanisms, malware, and backdoors from the environment. Incomplete eradication is the primary cause of incident recurrence -- every item must be verified, not assumed.

## Prerequisites

- [ ] Containment verified and holding (`containment-checklist.md`)
- [ ] Full scope assessment complete: all compromised systems, accounts, and data identified
- [ ] Malware analysis complete with comprehensive IOC list (hashes, C2, persistence artifacts)
- [ ] Root cause identified: initial access vector understood
- [ ] Forensic evidence preserved from all key systems before eradication begins
- [ ] Eradication plan reviewed and approved by incident commander
- [ ] Rollback plan prepared in case eradication causes service disruption

---

## Phase 1 -- Root Cause Identification

- [ ] Confirm initial access vector with evidence:
  - Phishing: identify the specific email, attachment/link, and delivery timestamp
  - Exploitation: identify the CVE, vulnerable service, and exploit artifacts
  - Credential compromise: identify which credential, how it was obtained, and first unauthorized use
  - Supply chain: identify the compromised software, update, or dependency
  - Insider: identify the individual and method
- [ ] Verify the initial access vector is closed:
  - [ ] Vulnerability patched or mitigated
  - [ ] Phishing email removed from all mailboxes; sender blocked
  - [ ] Compromised credential reset; access path hardened
  - [ ] Compromised supply chain component isolated or updated
- [ ] Document root cause with supporting evidence for post-incident report
- [ ] If root cause cannot be determined: document gap and assess risk of recurrence

## Phase 2 -- Malware Removal

- [ ] Compile master list of all malware artifacts (files, scripts, modified binaries) from analysis
- [ ] Deploy EDR removal actions across all affected endpoints simultaneously
  ```
  Target files: exact paths, hashes
  Action: quarantine (not delete) to preserve evidence copies
  ```
- [ ] Remove malware from locations EDR cannot reach:
  - Network shares and mapped drives
  - Backup systems (scan before any restoration)
  - Email attachments still in transit or quarantine queues
  - Cloud storage (OneDrive, SharePoint, S3 buckets)
  - Container images and registries
- [ ] Verify removal by re-scanning with updated signatures and IOC lists
- [ ] Check for modified system binaries (compare hashes against known-good baselines)
  ```bash
  # Windows: System File Checker
  sfc /scannow
  # Linux: package manager verification
  rpm -Va  # or dpkg --verify
  ```
- [ ] Search for dormant payloads: encrypted blobs, staged downloads, encoded scripts not yet executed

## Phase 3 -- Backdoor Hunting

- [ ] Search for unauthorized remote access mechanisms:
  - [ ] Web shells on all web servers
    ```bash
    # Search for common webshell indicators
    find /var/www -name "*.php" -newer /var/www/index.php -exec grep -l "eval\|base64_decode\|system\|exec\|passthru" {} \;
    find /var/www -name "*.aspx" -exec grep -l "unsafe\|Process\.Start\|cmd\.exe" {} \;
    ```
  - [ ] Unauthorized SSH keys in `~/.ssh/authorized_keys` across all systems
    ```bash
    for user_home in /home/*; do
      diff <(sort "$user_home/.ssh/authorized_keys" 2>/dev/null) <(sort /backup/baseline/authorized_keys_$(basename $user_home) 2>/dev/null)
    done
    ```
  - [ ] Unauthorized VPN accounts or certificates
  - [ ] Rogue RDP/TeamViewer/AnyDesk installations
  - [ ] Reverse tunnels (SSH -R, ngrok, Cloudflare tunnels)
  - [ ] Unauthorized proxy or SOCKS configurations
- [ ] Check for firmware-level implants on critical infrastructure (if nation-state threat suspected)
- [ ] Review cloud environment for attacker-created access:
  - New IAM users, roles, or policies
  - Lambda functions or cloud functions with backdoor code
  - Modified trust relationships or federation configurations
  - New S3 bucket policies granting external access

## Phase 4 -- Persistence Mechanism Cleanup

- [ ] Systematically check and clean all Windows persistence locations:
  - [ ] Registry Run/RunOnce keys (HKCU and HKLM)
  - [ ] Scheduled Tasks (`schtasks /query /fo csv /v`)
  - [ ] Services (`sc query state= all` -- look for unusual binaries)
  - [ ] WMI Event Subscriptions (`Get-WMIObject -Namespace root\Subscription -Class __EventFilter`)
  - [ ] Startup folders
  - [ ] DLL search-order hijack locations
  - [ ] COM object hijacks (CLSID registry modifications)
  - [ ] AppInit_DLLs, Image File Execution Options debugger keys
  - [ ] Print monitor DLLs, LSA authentication/notification packages
  - [ ] Boot Execute entries, Winlogon helper DLLs
  - [ ] Group Policy Objects (check for modified GPOs that deploy malware)
- [ ] Systematically check and clean all Linux persistence locations:
  - [ ] Cron jobs (all users + system crontabs)
  - [ ] Systemd services and timers
  - [ ] init.d scripts, rc.local
  - [ ] Shell profile modifications (.bashrc, .profile, .bash_profile)
  - [ ] LD_PRELOAD and /etc/ld.so.preload
  - [ ] PAM module modifications
  - [ ] Kernel modules (`lsmod`, compare against baseline)
- [ ] Check for modified DNS configurations that redirect traffic to attacker infrastructure
- [ ] Verify Active Directory for persistence:
  - [ ] AdminSDHolder ACL modifications
  - [ ] DCSync-capable permissions on unexpected accounts
  - [ ] Skeleton key detection (test authentication with master password)
  - [ ] Golden/Silver ticket indicators (reset KRBTGT if suspected)
  - [ ] Rogue domain controllers or replication partners
  - [ ] Modified Group Policy that could re-deploy malware

## Phase 5 -- Indicator Sweep

- [ ] Run environment-wide sweep with complete IOC set:
  ```
  File hashes (SHA-256): sweep via EDR
  Network indicators: sweep via SIEM/proxy/DNS logs (90-day lookback)
  Host indicators: sweep via EDR live query or SCCM
  ```
- [ ] YARA scan critical systems with rules from malware analysis
- [ ] Search for IOC variants (modified filenames, similar-but-different C2 domains)
- [ ] Review sweep results and investigate any new findings
- [ ] If new compromised systems discovered: expand eradication scope, update containment
- [ ] Perform negative confirmation: explicitly verify clean status of high-value assets
- [ ] Document sweep coverage: which systems were scanned, which could not be reached

## Phase 6 -- Eradication Verification

- [ ] Re-scan all affected systems 24 hours after eradication
- [ ] Verify no C2 communication from any network segment (check DNS logs, proxy logs, netflow)
- [ ] Confirm all compromised accounts remain secured (check for re-compromise)
- [ ] Validate that the initial access vector remains closed
- [ ] Run automated vulnerability scan on affected systems to confirm patches applied
- [ ] Obtain sign-off from incident commander that eradication is complete
- [ ] Document any residual risk or systems that could not be fully verified
- [ ] Transition to recovery phase (`recovery-checklist.md`)

---

## Cross-References

- Containment: `checklists/incident-response/containment-checklist.md`
- Recovery: `checklists/incident-response/recovery-checklist.md`
- Malware analysis: `checklists/malware/static-analysis-checklist.md`
- Malware response: `checklists/malware/malware-response-checklist.md`
- Forensics: `checklists/forensics-collection-quality.md`
- Threat hunting: `checklists/threat-hunt-quality.md`
- NIST SP 800-61r2: Section 3.3.4 -- Eradication and Recovery
