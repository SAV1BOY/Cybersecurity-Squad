# Threat Intelligence Feeds and Sources

## Purpose

This curated list provides the squad with vetted threat intelligence sources organized by type, quality, and use case. Not all intel is equal — this guide rates each source and explains when and how to use it. The goal is signal over noise: fewer, higher-quality feeds that actually inform defensive decisions rather than an overwhelming firehose of low-fidelity indicators.

## Tier 1: Authoritative Government and Standards Sources

These are the foundational sources. Every security team should monitor these.

### CISA (Cybersecurity and Infrastructure Security Agency)
- **URL**: https://www.cisa.gov/
- **Key Products**: Known Exploited Vulnerabilities (KEV) catalog, ICS advisories, cybersecurity alerts
- **Quality**: Authoritative, high signal-to-noise
- **Update Frequency**: KEV updated as new exploited vulnerabilities are confirmed; advisories as needed
- **Use Case**: Patch prioritization (KEV is the single best input for "what to patch first"), sector-specific threat awareness
- **Integration**: KEV catalog available as JSON/CSV for automated ingestion into vulnerability management platforms

### MITRE ATT&CK
- **URL**: https://attack.mitre.org/
- **Key Products**: Enterprise, Mobile, and ICS matrices; technique descriptions; group profiles; software profiles
- **Quality**: Gold standard for TTP classification
- **Update Frequency**: Quarterly major releases, ongoing updates
- **Use Case**: Detection engineering (map detections to techniques), threat modeling, adversary emulation, gap analysis
- **Integration**: STIX/TAXII format, ATT&CK Navigator for coverage visualization

### US-CERT / CISA Alerts and Advisories
- **URL**: https://www.cisa.gov/news-events/cybersecurity-advisories
- **Quality**: High, government-vetted
- **Use Case**: Situational awareness, sector-specific threat intelligence, joint advisories with Five Eyes partners

### NIST National Vulnerability Database (NVD)
- **URL**: https://nvd.nist.gov/
- **Quality**: Comprehensive, authoritative CVE enrichment
- **Use Case**: CVSS scoring, CPE matching, vulnerability research
- **Note**: NVD has experienced processing delays; supplement with vendor advisories for time-sensitive vulnerabilities

## Tier 2: Commercial and Vendor Threat Intelligence

### Mandiant (Google Cloud)
- **URL**: https://www.mandiant.com/resources/blog
- **Quality**: Excellent — deep incident response and APT research
- **Strengths**: APT group tracking, nation-state attribution, malware analysis
- **Use Case**: Strategic threat intelligence, adversary profiling, IR playbook development

### CrowdStrike Intelligence
- **URL**: https://www.crowdstrike.com/blog/
- **Quality**: High — strong adversary tracking methodology
- **Strengths**: Adversary naming convention (BEAR/PANDA/KITTEN/SPIDER), eCrime tracking
- **Use Case**: Adversary-focused defense, eCrime trends, targeted threat assessment

### Microsoft Threat Intelligence
- **URL**: https://www.microsoft.com/en-us/security/blog/
- **Quality**: High — unparalleled visibility into Windows/Azure/O365 ecosystem
- **Strengths**: Nation-state tracking, supply chain threats, identity-based attacks
- **Use Case**: Microsoft ecosystem defense, identity threat intelligence

### Google Threat Analysis Group (TAG)
- **URL**: https://blog.google/threat-analysis-group/
- **Quality**: High — focused on state-sponsored threats and zero-days
- **Use Case**: Zero-day awareness, surveillance vendor tracking

### Recorded Future
- **Quality**: High — strong OSINT and dark web intelligence
- **Strengths**: Automated intelligence from open, dark, and technical sources
- **Use Case**: Brand monitoring, credential exposure, third-party risk

## Tier 3: Open Source and Community Intelligence

### AlienVault OTX (Open Threat Exchange)
- **URL**: https://otx.alienvault.com/
- **Quality**: Variable — community-contributed, requires curation
- **Use Case**: IOC sharing, community pulse analysis, supplementary indicators
- **Caveat**: Validate before blocking — community IOCs can include false positives

### Abuse.ch Platforms
- **URLhaus**: https://urlhaus.abuse.ch/ (malicious URLs)
- **MalwareBazaar**: https://bazaar.abuse.ch/ (malware samples)
- **ThreatFox**: https://threatfox.abuse.ch/ (IOCs)
- **Feodo Tracker**: https://feodotracker.abuse.ch/ (botnet C2)
- **Quality**: High for their specific domains
- **Use Case**: Automated blocklist generation, malware analysis, C2 detection

### VirusTotal
- **URL**: https://www.virustotal.com/
- **Quality**: Essential multi-scanner aggregation
- **Use Case**: Sample analysis, IOC enrichment, relationship mapping
- **Caveat**: Do not upload sensitive files. Use hashes for lookup when possible.

## Tier 4: Social Media and Researcher Channels

### Security Twitter/X Accounts Worth Following
- **@GossiTheDog** (Kevin Beaumont) — Vulnerability exploitation tracking, real-time threat awareness
- **@MalwareJake** (Jake Williams) — IR insights, practical security analysis
- **@SwiftOnSecurity** — Security operations, defense insights, accessible education
- **@caborundorern** — Threat intelligence, APT tracking
- **@UK_Daniel_Card** — Practical security leadership and operations
- **Quality**: Variable, fast — often first to report active exploitation
- **Caveat**: Social media is a lead, not a source. Verify before acting.

### Mastodon / InfoSec Exchange
- **URL**: https://infosec.exchange/
- **Quality**: Growing community of security professionals, strong signal
- **Use Case**: Real-time threat discussion, vulnerability disclosure awareness

## Information Sharing and Analysis Centers (ISACs)

ISACs provide sector-specific threat intelligence and collaboration:

| ISAC | Sector | URL |
|------|--------|-----|
| FS-ISAC | Financial Services | https://www.fsisac.com/ |
| H-ISAC | Healthcare | https://h-isac.org/ |
| IT-ISAC | Information Technology | https://www.it-isac.org/ |
| E-ISAC | Electricity | https://www.eisac.com/ |
| MS-ISAC | State/Local Government | https://www.cisecurity.org/ms-isac |
| Auto-ISAC | Automotive | https://automotiveisac.com/ |

**Quality**: High, sector-relevant, peer-vetted
**Use Case**: Sector-specific threat awareness, indicator sharing, incident coordination

## Feed Integration Best Practices

1. **Curate aggressively**: More feeds does not equal better intelligence. Each feed requires maintenance, tuning, and false positive management.
2. **Automate IOC ingestion** into SIEM/SOAR/TIP with confidence scoring and expiration dates.
3. **Tag feed sources** so analysts can assess the reliability of an indicator in context.
4. **Set retention policies**: IOCs older than 90 days should be reviewed for continued relevance.
5. **Measure feed value**: Track which feeds generate true positive detections vs. noise. Drop feeds that do not contribute.

## Cross-References

- See `voice/calibration/attribution-calibration.md` for using threat intel in attribution
- See `voice/calibration/confidence-calibration.md` for assessing intel source confidence
- See `swipe-sources/security-blogs-and-research.md` for research-oriented sources
- See `swipe-sources/vulnerability-databases.md` for vulnerability-specific intelligence
