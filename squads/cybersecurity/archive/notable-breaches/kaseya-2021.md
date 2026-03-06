# Kaseya VSA Supply Chain Attack (2021)

## Incident Summary

| Field | Details |
|-------|---------|
| Organization | Kaseya (IT management software vendor) |
| Date | July 2, 2021 (Friday before US Independence Day weekend) |
| Threat Actor | REvil (Sodinokibi) ransomware gang |
| Attack Vector | Zero-day exploitation of Kaseya VSA on-premise servers |
| Vulnerabilities | CVE-2021-30116 (auth bypass), CVE-2021-30119 (XSS), CVE-2021-30120 (2FA bypass) |
| Impact | ~60 MSPs compromised, 1,500+ downstream businesses affected |
| Ransom Demand | $70 million (universal decryptor); individual demands per victim |
| Resolution | Kaseya obtained universal decryptor (circumstances unclear); REvil briefly went dark |

---

## Attack Narrative

### Strategic Timing and Targeting
- Attack launched on Friday, July 2, 2021 -- the start of US Independence Day weekend
- Targeted Kaseya VSA, an IT management and remote monitoring platform used by Managed Service Providers (MSPs)
- By compromising MSPs, the attackers could cascade the attack to all MSP clients simultaneously
- This created a multiplicative effect: ~60 compromised MSPs served ~1,500 downstream organizations

### Technical Attack Chain

**Step 1: Zero-Day Exploitation of Kaseya VSA**
REvil exploited multiple zero-day vulnerabilities in Kaseya VSA on-premise servers:
- Authentication bypass (CVE-2021-30116): allowed unauthenticated access to VSA
- SQL injection enabling credential extraction
- 2FA bypass allowing use of extracted credentials
- Arbitrary file upload enabling code execution on the VSA server

**Step 2: Leveraging VSA Agent Management**
Kaseya VSA is designed to push software and commands to managed endpoints. The attackers:
- Used the legitimate VSA agent update mechanism to deploy ransomware
- Created a fake "Kaseya VSA Agent Hot-fix" update
- The update was pushed to all endpoints managed by each compromised VSA server
- Because VSA agents run with SYSTEM-level privileges, the ransomware executed with full permissions

**Step 3: Defense Evasion**
The ransomware deployment was designed to evade security tools:
- Payload delivered as a legitimate-looking agent update (trusted source)
- Used certutil.exe to decode the payload (LOLBin technique)
- Disabled Windows Defender via PowerShell before executing
- Used side-loading of an old, legitimate Microsoft Defender binary to execute the ransomware DLL
- Some EDR products had exclusions for the Kaseya agent directory

**Step 4: Ransomware Execution**
Once deployed on endpoints:
- REvil ransomware encrypted files across the organization
- Each victim received a unique ransom demand (ranging from $45K to $5M per organization)
- Universal decryptor offered for $70 million

### Scale of Impact
- Swedish grocery chain Coop: ~800 stores closed for nearly a week (POS systems encrypted)
- Schools in New Zealand
- Multiple US medical and dental practices
- Legal firms, accounting firms, small businesses across multiple countries
- Many victims had no direct relationship with Kaseya -- they were clients of MSPs

## Root Cause Analysis

### Primary Failures

**1. Zero-Day Vulnerabilities in Kaseya VSA**
Multiple critical vulnerabilities existed in the on-premise VSA product:
- Authentication bypass should have been caught in security code review
- SQL injection is a well-understood vulnerability class
- These vulnerabilities had actually been reported to Kaseya by DIVD (Dutch Institute for Vulnerability Disclosure) before the attack, and patches were in development but not yet released

**2. MSP as Force Multiplier**
The MSP delivery model created extreme concentration risk:
- Single point of compromise (VSA server) controlled hundreds of endpoints
- MSP clients had minimal visibility into their MSP's security posture
- Trust relationship between MSP and client was exploited as an attack path
- EDR exclusions for management tools created blind spots

**3. Trusted Software Channel Abuse**
- The VSA agent update mechanism was designed to push software to all managed endpoints
- This legitimate capability became the ransomware delivery mechanism
- Endpoint security tools trusted updates from the VSA agent
- There was no additional verification of update integrity at the endpoint level

**4. Holiday Weekend Timing**
- Attack launched when IT staff would be minimal
- Reduced detection and response capability
- Longer dwell time before containment
- Maximum business disruption during recovery

## Lessons for Defensive Operations

### Supply Chain and MSP Risk

**For Organizations Using MSPs:**
- [ ] Understand what management tools your MSP deploys on your systems
- [ ] Know what permissions those tools have (typically SYSTEM/root)
- [ ] Require MSP to demonstrate their own security posture (SOC 2, penetration tests)
- [ ] Ensure your EDR covers MSP management tool directories (no blanket exclusions)
- [ ] Have a plan for rapid MSP tool isolation if compromise is suspected
- [ ] Maintain independent backup infrastructure not accessible via MSP tools
- [ ] Include MSP compromise scenario in incident response planning

**For MSPs:**
- [ ] Segment VSA/RMM servers from the internet where possible
- [ ] Apply patches to management tools with highest priority
- [ ] Monitor management tool servers for anomalous behavior
- [ ] Implement MFA on all management console access
- [ ] Restrict agent update capabilities to authorized personnel
- [ ] Maintain offline backups of client environments
- [ ] Have pre-planned communication and isolation procedures

### Software Supply Chain Security
- Management software with SYSTEM-level agent access is a tier-1 supply chain risk
- Validate integrity of software updates before deployment (code signing, hash verification)
- Monitor management tool behavior for anomalous commands or updates
- Implement application allowlisting that validates even "trusted" software updates
- Maintain SBOM for all management and monitoring tools

### Detection and Response
- [ ] Monitor management tool processes for unusual child processes
- [ ] Alert on certutil.exe or other LOLBins executed by management agents
- [ ] Detect Defender/AV disablement commands
- [ ] Monitor for mass file encryption patterns across managed endpoints
- [ ] Pre-stage ransomware incident response procedures (see `workflows/ransomware-preparedness.md`)
- [ ] Practice disconnecting management tools rapidly

### Timing-Aware Security
- Ensure 24/7/365 security monitoring coverage
- Increase alerting sensitivity during holiday periods
- Pre-position incident response resources before long weekends
- Attackers deliberately target periods of reduced staffing

## Broader Implications

### Industry Impact
- Demonstrated the catastrophic potential of MSP supply chain attacks
- Led to CISA guidance on MSP security practices
- Accelerated discussion of software supply chain security regulation
- Raised awareness of concentration risk in IT service delivery

### Regulatory Response
- CISA and FBI joint advisory on MSP supply chain threats
- Executive Order 14028 (May 2021) already addressed supply chain; Kaseya validated concerns
- Increased scrutiny of RMM tool security by insurance underwriters
- MSP security requirements added to many cyber insurance policies

### REvil Aftermath
- REvil infrastructure went offline July 13, 2021 (11 days after attack)
- Kaseya obtained universal decryptor July 22, 2021
- REvil re-emerged briefly in September 2021
- Russian authorities arrested 14 alleged REvil members in January 2022

## ATT&CK Mapping

| Tactic | Technique | Specifics |
|--------|-----------|-----------|
| Initial Access | T1195.002 Supply Chain: Software Supply Chain | Kaseya VSA zero-day exploitation |
| Execution | T1072 Software Deployment Tools | VSA agent update mechanism |
| Defense Evasion | T1562.001 Disable Security Tools | Defender disabled via PowerShell |
| Defense Evasion | T1574.002 DLL Side-Loading | Legitimate Microsoft binary side-loaded ransomware DLL |
| Defense Evasion | T1140 Deobfuscate/Decode Files | certutil.exe to decode payload |
| Impact | T1486 Data Encrypted for Impact | REvil ransomware encryption |

## Cross-References

- `workflows/ransomware-preparedness.md` — Ransomware defense and recovery
- `workflows/third-party-risk-assessment.md` — Vendor and MSP risk assessment
- `tasks/governance/vendor-security-review.md` — Vendor security evaluation
- `archive/notable-breaches/notpetya-2017.md` — Another supply chain attack
- `archive/regulatory-milestones/executive-order-14028.md` — Supply chain executive order
- `workflows/incident-response-workflow.md` — Incident response procedures
