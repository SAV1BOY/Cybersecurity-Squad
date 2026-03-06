# Threat Intelligence Report Examples

## Purpose

High-quality threat intelligence report templates for actor profiles, campaign analysis, and IOC sections. Demonstrates intelligence writing standards, analytic rigor, and actionable presentation.

## Report Type 1: Threat Actor Profile

```markdown
# Threat Actor Profile: SCATTERED SPIDER (UNC3944)

**TLP: AMBER**
**Report ID:** TI-2026-0042
**Date:** 2026-03-01
**Confidence:** High
**Last Updated:** 2026-03-01
**Analyst:** [Name]

## Summary

SCATTERED SPIDER is a financially motivated threat group primarily composed of
English-speaking individuals, active since at least 2022. The group targets
large enterprises, particularly in telecommunications, technology, and hospitality
sectors, using sophisticated social engineering and identity-based attacks to
gain initial access, followed by cloud-focused lateral movement for data
extortion and ransomware deployment.

## Attribution

| Attribute | Assessment |
|-----------|-----------|
| Origin | United States, United Kingdom (primary) |
| Motivation | Financial (extortion, data theft, ransomware) |
| Sophistication | High |
| Active Since | Mid-2022 |
| Aliases | UNC3944 (Mandiant), 0ktapus (Group-IB), Muddled Libra (Unit 42) |
| Affiliation | Loose association with ALPHV/BlackCat RaaS |

## Targeting

| Sector | Frequency | Objective |
|--------|-----------|-----------|
| Telecommunications | High | SIM swapping, customer data |
| Technology | High | Source code, cloud infrastructure |
| Hospitality/Gaming | High | Customer databases, financial data |
| Financial Services | Medium | Payment systems, customer PII |
| Retail | Medium | Gift card systems, customer data |

## Tactics, Techniques, and Procedures (TTPs)

### Initial Access
| Technique | MITRE ID | Description |
|-----------|----------|-------------|
| Phishing (voice) | T1566 | Calls to IT help desk impersonating employees |
| SIM swapping | T1078 | Port victim phone numbers to attacker SIM for MFA bypass |
| SMS phishing | T1566.001 | Fake SSO login pages sent via SMS |
| MFA fatigue | T1621 | Repeated push notifications until user accepts |
| Social engineering | T1534 | Target IT support for credential reset |

### Persistence & Lateral Movement
| Technique | MITRE ID | Description |
|-----------|----------|-------------|
| Okta/Azure AD manipulation | T1098 | Register attacker MFA devices, create federated trust |
| Cloud account access | T1078.004 | Use stolen cloud credentials for tenant access |
| VPN access | T1133 | Establish VPN access using compromised identity |
| O365/Google Workspace | T1114.003 | Access email and cloud storage via SSO |

### Impact
| Technique | MITRE ID | Description |
|-----------|----------|-------------|
| Data exfiltration | T1567 | Exfiltrate via cloud storage services |
| Ransomware deployment | T1486 | Deploy ALPHV/BlackCat ransomware |
| Extortion | T1657 | Threaten data leak for ransom payment |

## Indicators of Compromise

### Network Indicators
| Type | Value | Context | First Seen |
|------|-------|---------|------------|
| Domain | login-company[.]com | Phishing landing page | 2025-11-15 |
| Domain | sso-portal-update[.]com | Credential harvesting | 2025-12-01 |
| IP | 192.0.2[.]50 | C2 infrastructure | 2025-11-20 |
| IP | 198.51.100[.]75 | Exfiltration endpoint | 2025-12-05 |

### Behavioral Indicators
- New MFA device registration from unusual location
- Okta admin API calls from non-standard IP
- Large-volume SharePoint/OneDrive downloads
- VPN connection from consumer ISP after MFA device change
- Azure AD conditional access policy modification

## Defensive Recommendations

| Priority | Recommendation | Mitigates |
|----------|---------------|-----------|
| Critical | Implement phishing-resistant MFA (FIDO2/WebAuthn) | MFA bypass, SIM swap |
| Critical | Harden help desk identity verification procedures | Social engineering |
| High | Monitor for anomalous MFA device registrations | Persistence |
| High | Implement conditional access with trusted device/location | Unauthorized access |
| High | Alert on Okta/Azure AD admin API calls from new IPs | Cloud manipulation |
| Medium | Enable number matching for push MFA | MFA fatigue |
| Medium | Monitor for bulk file downloads from cloud storage | Data exfiltration |

## Intelligence Gaps
- Full membership and organizational structure
- Relationship with other cybercrime groups beyond ALPHV
- Current operational infrastructure
- Cryptocurrency wallets and financial flow
```

## Report Type 2: Campaign Analysis

```markdown
# Campaign Analysis: Operation CloudHopper (Active Campaign)

**TLP: AMBER+STRICT**
**Report ID:** TI-2026-0089
**Date:** 2026-02-28
**Confidence:** Moderate-High
**Classification:** Actionable Intelligence

## Campaign Summary

Active campaign targeting managed service providers (MSPs) and their downstream
customers via supply chain compromise. The campaign leverages trusted MSP
access to deploy remote access tools and exfiltrate sensitive data from
multiple victim organizations simultaneously.

## Timeline

| Date | Event | Confidence |
|------|-------|-----------|
| 2025-10-01 | First observed MSP compromise via spear-phishing | High |
| 2025-10-15 | Lateral movement to MSP management tools | High |
| 2025-11-01 | First downstream customer compromise identified | High |
| 2025-12-01 | Second MSP compromised via similar methodology | Moderate |
| 2026-01-15 | Campaign linked to known APT group via infrastructure overlap | Moderate |
| 2026-02-15 | Additional IOCs identified from partner intelligence | High |

## Attack Flow

```
Phase 1: MSP Compromise
  Spear-phish MSP admin -> Credential theft -> MFA bypass (token theft)
  -> Access MSP management platform

Phase 2: Downstream Pivot
  Use MSP remote management tools -> Deploy secondary RAT on customer
  -> Establish independent C2 channel

Phase 3: Objectives
  Discovery (AD, file shares) -> Credential harvesting
  -> Data staging -> Exfiltration via encrypted channel
```

## Technical Analysis

### Malware Analysis
| Component | Hash (SHA-256) | Type | Function |
|-----------|---------------|------|----------|
| Stage 1 loader | a1b2c3d4...e5f6 | DLL sideload | Initial execution, anti-analysis |
| Stage 2 RAT | f7g8h9i0...j1k2 | Custom backdoor | Full C2, file operations |
| Credential tool | l3m4n5o6...p7q8 | Modified Mimikatz | LSASS dump, token manipulation |

### Infrastructure
| Component | Details | Hosting |
|-----------|---------|---------|
| C2 Primary | updates.legit-service[.]com:443 | Cloud provider, US region |
| C2 Secondary | cdn-static.another-service[.]net:8443 | VPS, Singapore |
| Exfil endpoint | storage.cloud-backup-svc[.]com | Cloud storage |
| Phishing | portal.msp-partner-login[.]com | Bulletproof hosting |

## IOC Section

### STIX Bundle Reference
Full STIX 2.1 bundle available at: [internal TIP link]

### Detection Signatures

**Sigma Rule - Suspicious MSP Tool Usage:**
```yaml
title: Suspicious Remote Management Tool Execution
status: experimental
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        ParentImage|endswith:
            - '\ConnectWise\*.exe'
            - '\Datto\*.exe'
        Image|endswith:
            - '\cmd.exe'
            - '\powershell.exe'
    filter:
        CommandLine|contains:
            - 'known-legitimate-script'
    condition: selection and not filter
level: high
```

## Relevance Assessment

| Factor | Assessment | Rationale |
|--------|-----------|-----------|
| Sector targeting | High relevance | Our industry actively targeted |
| TTP overlap | Medium relevance | Some TTPs match our environment |
| IOC overlap | Check required | Run IOC sweep against our telemetry |
| Exposure | Medium | We use MSPs in scope of this campaign |

## Recommended Actions

| Action | Priority | Owner | Deadline |
|--------|----------|-------|----------|
| Sweep for IOCs across all telemetry | Critical | SOC | 24 hours |
| Contact MSP vendors for assurance | High | Vendor Mgmt | 48 hours |
| Review MSP access controls and monitoring | High | IT Security | 1 week |
| Implement detection rules provided | High | Detection Eng | 48 hours |
| Brief executive team on supply chain risk | Medium | CISO | 1 week |
```

## Report Type 3: Strategic Intelligence Brief

```markdown
# Quarterly Threat Landscape Brief -- Q1 2026

**TLP: GREEN**
**Audience:** Executive Leadership, Board Risk Committee
**Period:** January - March 2026

## Key Themes

### 1. AI-Augmented Social Engineering
Threat actors are increasingly using generative AI for voice cloning and
deepfake video in social engineering campaigns. Help desk compromise attacks
now incorporate real-time voice synthesis.

**Our Exposure:** Medium -- mitigated by out-of-band verification procedures.
**Recommendation:** Update identity verification to include challenge-response
protocols not defeatable by AI.

### 2. Cloud-Native Ransomware
New ransomware variants target cloud storage directly, encrypting S3 buckets
and Azure Blob containers using customer-managed keys under attacker control.

**Our Exposure:** High -- significant cloud storage footprint.
**Recommendation:** Implement object lock and versioning on all critical buckets.

### 3. Supply Chain Targeting Intensification
[Continued analysis...]

## Threat Actor Activity Relevant to Our Sector

| Actor | Activity Level | Targeting | Risk to Us |
|-------|---------------|-----------|-----------|
| [Actor 1] | High | Our sector, our geography | High |
| [Actor 2] | Medium | Adjacent sector | Medium |
| [Actor 3] | Low (dormant) | Previously targeted us | Monitor |

## Recommended Strategic Investments
1. [Investment area with justification]
2. [Investment area with justification]
3. [Investment area with justification]
```

## Cross-References

- [Threat Intelligence Framework](../../frameworks/threat-intelligence-framework.md) -- methodology
- [Threat Actor Taxonomy](../../lib/taxonomies/threat-actor-taxonomy.md) -- actor classification
- [Attack Technique Taxonomy](../../lib/taxonomies/attack-technique-taxonomy.md) -- TTP mapping
- [Sigma Rule Examples](../detection/sigma-rule-examples.md) -- detection rules
