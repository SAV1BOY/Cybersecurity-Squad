# Threat Actor Taxonomy

## Purpose

Classification of threat actors by type, motivation, capability, and sophistication level. Provides a structured model for threat intelligence analysis, risk assessment, and defense prioritization.

## Actor Categories

### Category 1: Nation-State / State-Sponsored

| Attribute | Description |
|-----------|-------------|
| Motivation | Espionage (political, military, economic), disruption, sabotage, intelligence gathering |
| Capability | Highest -- custom tooling, zero-days, vast resources, operational patience |
| Sophistication | Advanced -- multi-year campaigns, supply chain attacks, counter-forensics |
| Targets | Government, defense, critical infrastructure, technology, research |
| Persistence | Very high -- will re-compromise after eviction, long dwell times |
| Risk tolerance | Low -- prefer stealth, avoid detection, sophisticated OPSEC |

**Known Groups by Attribution:**

| Region | Groups | Typical Targets | Signature TTPs |
|--------|--------|----------------|---------------|
| China | APT1, APT10, APT41, Volt Typhoon | Technology, defense, telecom, critical infrastructure | Supply chain, living-off-the-land, long dwell |
| Russia | APT28 (Fancy Bear), APT29 (Cozy Bear), Sandworm | Government, energy, elections, military | Destructive attacks, spear-phishing, credential theft |
| North Korea | Lazarus Group, APT38, Kimsuky | Financial (SWIFT), cryptocurrency, defense | Financial theft, destructive wiper, social engineering |
| Iran | APT33, APT34, APT35, MuddyWater | Energy, government, telecom, regional targets | Web shell, DNS hijacking, destructive attacks |

**Defense Priority:** Highest for organizations in targeted sectors. Focus on detection of living-off-the-land techniques, supply chain integrity, and long-dwell detection.

### Category 2: Cybercrime / Financially Motivated

| Attribute | Description |
|-----------|-------------|
| Motivation | Financial gain -- ransomware, extortion, fraud, theft |
| Capability | Medium to High -- use commercial tools, RaaS, exploit kits |
| Sophistication | Variable -- from commodity malware to targeted big-game hunting |
| Targets | Opportunistic (any vulnerable target) or targeted (high-revenue organizations) |
| Persistence | Moderate -- move fast, monetize quickly |
| Risk tolerance | Higher -- willing to cause visible damage for payment |

**Sub-Categories:**

| Sub-Category | Description | Examples | Typical TTPs |
|-------------|-------------|---------|-------------|
| Ransomware operators | Develop and deploy ransomware | LockBit, BlackCat/ALPHV, Cl0p | Double extortion, RaaS model |
| Initial access brokers | Sell access to compromised networks | Various on cybercrime forums | Phishing, exploit scanning, credential stuffing |
| Business email compromise | Email-based financial fraud | Various BEC groups | Social engineering, email spoofing, account takeover |
| Carding/financial fraud | Payment card theft and fraud | Magecart groups, FIN7 | POS malware, web skimmers, credential theft |
| Cryptocurrency theft | Steal cryptocurrency | Lazarus (overlap), various | Exchange attacks, smart contract exploits, social engineering |
| Data brokers | Steal and sell data | Various on dark web | Database breaches, scraping, insider purchase |

**Defense Priority:** High for all organizations. Focus on ransomware defense, phishing prevention, vulnerability management, and backup integrity.

### Category 3: Hacktivism

| Attribute | Description |
|-----------|-------------|
| Motivation | Political, social, or ideological goals -- protest, disruption, embarrassment |
| Capability | Low to Medium -- DDoS tools, web defacement, data leaks |
| Sophistication | Generally low -- script kiddie to moderate |
| Targets | Government, corporations (perceived adversaries), controversial organizations |
| Persistence | Low -- campaign-based, move on after making statement |
| Risk tolerance | High -- seek publicity, no concern about detection |

**Notable Groups:**

| Group | Focus | Typical TTPs |
|-------|-------|-------------|
| Anonymous (collective) | Various political causes | DDoS, defacement, data leaks |
| IT Army of Ukraine | Pro-Ukraine cyber operations | DDoS, data leaks |
| Various ideological groups | Region/cause-specific | Defacement, social media takeover |
| Environmental activists | Corporate environmental targets | DDoS, data leaks, defacement |

**Defense Priority:** Medium. Focus on DDoS mitigation, web application security, and data leak prevention. Higher priority if organization is in a controversial sector.

### Category 4: Insider Threat

| Attribute | Description |
|-----------|-------------|
| Motivation | Financial gain, revenge, ideology, coercion, negligence |
| Capability | High -- legitimate access, knowledge of systems and processes |
| Sophistication | Variable -- from inadvertent to highly sophisticated |
| Targets | Own organization's data, systems, and reputation |
| Persistence | N/A -- already inside |
| Risk tolerance | Variable -- negligent insiders unaware, malicious insiders cautious |

**Sub-Types:**

| Type | Motivation | Indicators | Detection Approach |
|------|-----------|-----------|-------------------|
| Malicious (espionage) | Financial, ideological | Unusual data access, communication with competitors | UEBA, DLP, financial monitoring |
| Malicious (sabotage) | Revenge, disgruntlement | After-hours access, unauthorized changes, data deletion | Behavioral monitoring, access controls |
| Negligent | None (careless) | Policy violations, misconfiguration, phishing victim | Training, automation, guardrails |
| Compromised | N/A (externally manipulated) | Account anomalies matching external attack patterns | Treat as external compromise |
| Departing | Opportunistic | Data hoarding before resignation, USB usage, personal email | Enhanced monitoring on notice, DLP |

**Defense Priority:** High for all organizations. Focus on UEBA, DLP, access controls, and separation of duties.

### Category 5: Terrorist Organizations

| Attribute | Description |
|-----------|-------------|
| Motivation | Cause maximum disruption, fear, destruction for political/religious goals |
| Capability | Generally low, but potentially supported by nation-states |
| Sophistication | Low to medium -- developing capabilities |
| Targets | Critical infrastructure, government, high-profile targets |
| Persistence | Variable -- may be one-time destructive |
| Risk tolerance | Extremely high -- seek maximum impact regardless of consequences |

**Defense Priority:** Critical for critical infrastructure and government. Focus on destructive attack prevention, ICS/OT security, and physical-cyber convergence.

### Category 6: Competitors / Corporate Espionage

| Attribute | Description |
|-----------|-------------|
| Motivation | Competitive advantage, trade secret theft, market intelligence |
| Capability | Medium -- may hire hackers, use commercial tools, or recruit insiders |
| Sophistication | Medium -- targeted but resource-constrained vs. nation-states |
| Targets | Competitors' intellectual property, pricing, strategy |
| Persistence | Moderate -- sustained interest in specific data |
| Risk tolerance | Low -- avoid detection and legal consequences |

**Defense Priority:** High for organizations with valuable IP. Focus on trade secret protection, insider threat detection, and supply chain security.

## Capability Assessment Model

### Sophistication Levels

| Level | Label | Indicators | Example Actors |
|-------|-------|-----------|---------------|
| 1 | Script Kiddie | Uses publicly available tools without modification | Opportunistic attackers |
| 2 | Commodity | Uses commercial/criminal tools (RaaS, exploit kits) | Many cybercrime groups |
| 3 | Skilled | Modifies tools, develops custom scripts, adapts TTPs | Advanced cybercrime, some hacktivists |
| 4 | Advanced | Develops custom malware, discovers vulnerabilities, sophisticated OPSEC | Advanced cybercrime, some state-sponsored |
| 5 | Elite | Develops zero-days, conducts supply chain attacks, years-long operations | Top-tier nation-state actors |

### Resource Assessment

| Resource | Level 1-2 | Level 3 | Level 4-5 |
|----------|-----------|---------|-----------|
| Funding | Minimal | Moderate (criminal proceeds) | Extensive (state budget) |
| Personnel | Individual or small group | Small team (5-20) | Large teams (50+) |
| Infrastructure | Shared/rented | Dedicated C2, bulletproof hosting | Multi-layered, global infrastructure |
| Tools | Public tools | Modified/commercial tools | Custom tooling, zero-days |
| Intelligence | Open source | Criminal intelligence sharing | State intelligence apparatus |
| Time | Hours to days | Weeks to months | Months to years |

## Threat Actor Profiling Template

```
Name/Designation: [Actor name or internal designation]
Aliases: [Known aliases from different vendors]
Category: [Nation-state / Cybercrime / Hacktivist / Insider / etc.]
Motivation: [Primary motivation]
Sophistication Level: [1-5]
Active Since: [First observed]
Status: [Active / Dormant / Disbanded]
Geographic Origin: [Country/Region, confidence level]

Targeting:
  Industries: [Targeted sectors]
  Geographies: [Targeted regions]
  Organization Size: [Large enterprise, SMB, etc.]

Capabilities:
  Initial Access: [Preferred methods]
  Tooling: [Known tools and malware]
  Infrastructure: [C2 patterns, hosting]
  Exfiltration: [Data theft methods]

Known Campaigns:
  [Campaign name]: [Date, targets, objectives, outcome]

IOCs:
  [List of current indicators]

Relevance to Our Organization: [High/Medium/Low with justification]

Recommended Defenses:
  [Specific controls mapped to this actor's TTPs]
```

## Actor-Control Mapping

| Actor Type | Priority Defensive Controls |
|-----------|---------------------------|
| Nation-state | Advanced EDR, network segmentation, threat hunting, supply chain security, zero trust |
| Ransomware | Immutable backups, network segmentation, MFA, email security, EDR, patch management |
| BEC | Email authentication (DMARC), security awareness, payment verification, MFA |
| Hacktivist | DDoS protection, web application security, data leak prevention |
| Insider | UEBA, DLP, PAM, access certification, separation of duties |
| Competitor | Trade secret protection, NDA enforcement, insider threat program, counterintelligence |

## Cross-References

- [Threat Intelligence Framework](../../frameworks/threat-intelligence-framework.md) -- intelligence methodology
- [Attack Technique Taxonomy](attack-technique-taxonomy.md) -- TTP classification
- [Adversary Simulation Framework](../../frameworks/adversary-simulation-framework.md) -- emulation approach
- [Incident Type Taxonomy](incident-type-taxonomy.md) -- incident classification
- [Threat Intelligence Report Examples](../../swipe/reports/threat-intelligence-report-examples.md) -- actor profiles
