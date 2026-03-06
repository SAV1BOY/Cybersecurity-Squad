# SolarWinds Supply Chain Attack (2020) — Case Study

## Incident Summary
- **Date**: Discovered December 2020 (active since March 2020)
- **Attacker**: APT29 / Cozy Bear (attributed to Russian SVR)
- **Vector**: Software supply chain compromise of SolarWinds Orion
- **Impact**: ~18,000 organizations installed trojanized update; ~100 actively exploited
- **Victims**: US Treasury, Commerce, DHS, FireEye, Microsoft, and more

## Attack Chain (Kill Chain Mapping)

### 1. Initial Compromise
- Compromised SolarWinds build environment (likely via credentials or insider)
- Injected SUNBURST backdoor into Orion build process
- Malicious code signed with legitimate SolarWinds certificates

### 2. Delivery & Installation
- Trojanized update (2019.4 HF 5 through 2020.2.1) distributed via normal update channel
- SUNBURST DLL loaded by legitimate SolarWinds process
- 14-day dormancy period before activating C2

### 3. Command & Control
- DNS-based C2 using encoded subdomains of avsvmcloud[.]com
- Switched to HTTPS C2 after initial reconnaissance
- C2 traffic mimicked legitimate Orion API communications
- Used steganography in HTTP responses

### 4. Lateral Movement & Exploitation
- TEARDROP and RAINDROP loaders deployed additional payloads
- SAML token forging (GoldenSAML) for cloud access
- Targeted high-value email accounts and documents
- Created additional persistence in Azure AD/M365

## Detection Failures
- Signed binary trusted by endpoint protection
- Network traffic blended with legitimate SolarWinds traffic
- 9-month dwell time before detection
- Only discovered because FireEye detected its own Red Team tools were stolen

## What Finally Worked
- FireEye's internal monitoring of Red Team tool usage
- Behavioral analysis of anomalous SAML token activity
- Retroactive threat hunting across historical DNS logs
- Collaborative investigation between private sector and government

## Lessons for Defense

### Supply Chain Security
- Verify build pipeline integrity (reproducible builds)
- Monitor for behavioral changes in trusted software
- Implement software bill of materials (SBOM)
- Limit trust scope of third-party software

### Detection Engineering
- Monitor SAML token anomalies (audience, lifetime, issuer)
- Track service principal credential changes in cloud
- Detect anomalous DNS query patterns (entropy analysis)
- Hunt for process injection in trusted binaries

### Incident Response
- Pre-position forensic capabilities for cloud environments
- Maintain offline backup of authentication infrastructure
- Plan for scenarios where your tools are compromised
- Coordinate cross-organization response for supply chain events

## MITRE ATT&CK Techniques
- T1195.002 — Supply Chain Compromise: Software Supply Chain
- T1071.001 — Application Layer Protocol: Web
- T1568.002 — Dynamic Resolution: Domain Generation
- T1606.002 — Forge Web Credentials: SAML Tokens
- T1078.004 — Valid Accounts: Cloud Accounts

## Cross-References
- `frameworks/supply-chain-attack-defense.md`
- `archive/attack-evolution/evolution-of-supply-chain-attacks.md`
- `checklists/cloud/cloud-identity-audit-checklist.md`
