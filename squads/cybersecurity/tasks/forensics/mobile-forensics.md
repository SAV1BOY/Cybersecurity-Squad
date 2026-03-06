# Mobile Device Forensic Acquisition and Analysis

## Purpose

Provide structured methodology for forensic acquisition and analysis of mobile devices (iOS and Android) involved in security incidents, insider investigations, or legal proceedings. Mobile devices contain dense concentrations of communications, location, authentication, and behavioral data critical to investigations.

## Task Owner
Digital forensics analyst with mobile forensics training and certification.

## Prerequisites
- Mobile forensic tool suite: Cellebrite UFED, Magnet AXIOM, GrayKey (iOS), MSAB XRY
- Open source tools: MVT (Mobile Verification Toolkit), ADB, libimobiledevice
- Faraday bag/cage (prevent remote wipe during acquisition)
- Device-specific cables and adapters
- Legal authorization for device examination (consent, warrant, or corporate policy)

---

## Phase 1: Pre-Acquisition

### 1.1 Legal Authorization
- [ ] Confirm legal basis for device examination
  - Corporate-owned device: company policy authorizing examination
  - Personal device: employee consent, search warrant, or court order
  - BYOD: review BYOD agreement for examination provisions
- [ ] Document authorization in case file before touching device
- [ ] Engage legal counsel for any ambiguity

### 1.2 Device Assessment
- [ ] Identify device make, model, and OS version
- [ ] Determine device ownership (corporate, personal, BYOD)
- [ ] Assess device state: powered on/off, locked/unlocked, damaged
- [ ] Check for MDM enrollment (may enable remote wipe capability)
- [ ] Identify encryption status (FDE is standard on modern iOS and Android)
- [ ] Document IMEI, serial number, phone number if visible

### 1.3 Device Isolation
Prevent evidence tampering or remote wipe:
- [ ] Place device in Faraday bag immediately upon seizure
- [ ] Alternatively, enable airplane mode (if accessible without unlocking)
- [ ] If powered on and unlocked, disable WiFi, cellular, and Bluetooth
- [ ] Do NOT power off an unlocked device (re-locking may prevent access)
- [ ] If MDM is enrolled, coordinate with MDM admin to prevent remote wipe
- [ ] Photograph device screen if displaying relevant information

## Phase 2: Forensic Acquisition

### 2.1 Acquisition Types

| Type | Description | Data Recovered | Tools |
|------|-------------|---------------|-------|
| Full Filesystem | Complete filesystem extraction | Maximum: all files, databases, deleted data | Cellebrite, GrayKey (with exploit) |
| Advanced Logical | Enhanced logical extraction | Apps, databases, media, some deleted | Cellebrite, AXIOM |
| Logical | Backup-based extraction | User data, contacts, messages, media | iTunes backup, ADB backup |
| Cloud | Cloud account data extraction | Synced data from iCloud, Google | Cellebrite Cloud, Magnet AXIOM Cloud |
| Manual | Photograph screen contents | Only visible data | Camera |

### 2.2 iOS Acquisition
```
Priority order for iOS:
1. Full filesystem (requires exploit/jailbreak capability - GrayKey, Cellebrite Premium)
2. Advanced logical via iTunes backup (requires passcode or MDM bypass)
3. Cloud acquisition (iCloud - requires credentials or token)
4. Logical via libimobiledevice (if device is paired/trusted)
```

- [ ] Check for existing trusted computer pairing (lockdown records)
- [ ] If passcode known: create encrypted iTunes backup (captures keychain)
- [ ] If passcode unknown: attempt exploitation tools (GrayKey, Cellebrite)
- [ ] Extract and decrypt backup with forensic tool
- [ ] Verify acquisition completeness against device storage capacity

### 2.3 Android Acquisition
```
Priority order for Android:
1. Full filesystem via root/exploit (Cellebrite, MSAB)
2. ADB-based extraction (if USB debugging enabled and authorized)
3. Samsung Smart Switch backup (Samsung devices)
4. Cloud acquisition (Google account)
5. Chip-off / JTAG (destructive, last resort for damaged devices)
```

- [ ] Check if USB debugging is enabled (Settings > Developer Options)
- [ ] If ADB accessible, extract via ADB:
```bash
# List installed packages
adb shell pm list packages

# Extract app data (requires root or backup)
adb backup -apk -shared -all -f device_backup.ab

# Logical file pull (requires appropriate permissions)
adb pull /sdcard/ /evidence/sdcard/
```
- [ ] For full filesystem: use commercial tool with exploit capability
- [ ] For encrypted devices: passcode or biometric required

### 2.4 Cloud Acquisition
- [ ] iCloud: extract with known Apple ID credentials or authentication token
- [ ] Google Account: extract with known credentials or account token
- [ ] Third-party apps: WhatsApp backup (Google Drive/iCloud), Signal, Telegram
- [ ] Email accounts synced to device
- [ ] Document all cloud sources accessed and extraction timestamps

## Phase 3: Analysis

### 3.1 Communication Analysis
- [ ] SMS/MMS messages (including deleted if filesystem extraction)
- [ ] iMessage / RCS conversations
- [ ] Messaging apps: WhatsApp, Signal, Telegram, Slack, Teams
- [ ] Email accounts and messages
- [ ] Call logs (incoming, outgoing, missed, duration)
- [ ] Voicemail recordings
- [ ] FaceTime / video call history

### 3.2 Location Analysis
- [ ] GPS data from photos (EXIF metadata)
- [ ] Significant locations / frequent locations (iOS)
- [ ] Google Location History / Timeline
- [ ] WiFi connection history (reveals locations visited)
- [ ] Cell tower connection logs
- [ ] App-specific location data (Maps, ride-sharing, fitness)
- [ ] Bluetooth connections (reveals proximity to other devices)

### 3.3 Application Analysis
- [ ] Installed applications inventory (including recently deleted)
- [ ] Application data and databases (SQLite analysis)
- [ ] Browser history, bookmarks, cached pages
- [ ] Cloud storage apps (Dropbox, Google Drive, OneDrive) - local cache
- [ ] Social media apps data
- [ ] VPN applications and connection history
- [ ] Password manager data (if accessible)
- [ ] Financial/banking application data

### 3.4 Security-Relevant Artifacts

**iOS Specific:**
- [ ] KnowledgeC database (detailed user activity timeline)
- [ ] Health database (device unlock, movement patterns)
- [ ] Screen Time data (app usage patterns)
- [ ] Siri suggestions / interaction data
- [ ] AirDrop history
- [ ] Keychain items (if encrypted backup captured)

**Android Specific:**
- [ ] Google Activity data
- [ ] Package installation history
- [ ] Accounts and sync data
- [ ] Notification history
- [ ] Clipboard history
- [ ] USB connection history

### 3.5 Spyware and Malware Detection
- [ ] Run MVT (Mobile Verification Toolkit) against extraction:
```bash
# iOS analysis
mvt-ios check-backup --output /evidence/mvt_results /evidence/ios_backup

# Android analysis
mvt-android check-adb --output /evidence/mvt_results
```
- [ ] Check for known spyware indicators (Pegasus, Predator, Hermit)
- [ ] Look for unusual device administrator apps
- [ ] Check for certificate authority installations
- [ ] Review app permissions for overly permissive applications
- [ ] Check for modified system partitions (rooted/jailbroken)

## Phase 4: Timeline Construction

- [ ] Build unified timeline from all data sources:
  - Communications (messages, calls, emails)
  - Location data (GPS, WiFi, cell tower)
  - Application activity
  - Device events (unlock, lock, power, charging)
  - Web browsing
  - File creation/modification
- [ ] Correlate mobile timeline with other investigation evidence
- [ ] Identify patterns, gaps, and anomalies in activity

## Phase 5: Reporting

### 5.1 Report Contents
- [ ] Device identification and acquisition method
- [ ] Extraction type and completeness assessment
- [ ] Relevant communications (filtered by investigation scope)
- [ ] Location history relevant to investigation timeline
- [ ] Application data findings
- [ ] Malware/spyware detection results
- [ ] Timeline of relevant activity
- [ ] IOCs extracted (if malware found)
- [ ] Evidence integrity documentation (hashes, chain of custody)

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Computer forensics correlation
- `tasks/forensics/cloud-forensics.md` — Cloud evidence for mobile-synced data
- `workflows/insider-threat-investigation.md` — Insider investigation evidence
- `workflows/incident-response-workflow.md` — IR integration
- `scripts/forensic-triage-scripts.md` — Triage automation
