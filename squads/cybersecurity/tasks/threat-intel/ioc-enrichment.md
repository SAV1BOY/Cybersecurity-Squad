# Indicator of Compromise Enrichment and Correlation Task

## Purpose

Transform raw indicators of compromise (IOCs) into actionable, contextualized intelligence by enriching them with metadata, assessing confidence and relevance, correlating across sources, and integrating into detection and response systems. Raw IOCs without context are noise; enriched IOCs are intelligence.

## Task Owner
Threat intelligence analyst, with automation support from security engineering.

## Frequency
Continuous as new IOCs are received; batch enrichment for bulk feeds daily.

---

## IOC Types and Sources

### 1.1 Indicator Types

| Type | Examples | Primary Use |
|------|---------|-------------|
| IP Address | C2 servers, scanning sources, attacker infrastructure | Firewall/IDS blocking, SIEM correlation |
| Domain | C2 domains, phishing domains, DGA domains | DNS blocking, proxy filtering |
| URL | Malware delivery URLs, phishing pages | Web proxy blocking, email filtering |
| File Hash | MD5, SHA-1, SHA-256 of malware samples | EDR detection, file reputation |
| Email Address | Phishing sender addresses | Email gateway blocking |
| Email Subject | Phishing campaign subject lines | Email filtering rules |
| Certificate | SSL certificate fingerprints (C2 communication) | Network detection |
| User Agent | Malware user agent strings | Proxy/WAF detection |
| Registry Key | Persistence mechanisms | EDR/host detection |
| Mutex | Malware mutex names | Host detection |
| YARA Rule | Pattern-based malware detection | File scanning, memory scanning |

### 1.2 IOC Sources
- Threat intelligence platform feeds (commercial and open source)
- ISAC sharing (FS-ISAC, H-ISAC sector alerts)
- MISP sharing communities
- Incident response findings (internal)
- Malware analysis outputs
- Security vendor advisories
- Government advisories (CISA, FBI Flash)
- Open source feeds (Abuse.ch, AlienVault OTX, PhishTank)

## Enrichment Process

### 2.1 Automated Enrichment
For each IOC, automatically query enrichment sources:

**IP Address Enrichment:**
- [ ] WHOIS registration data (registrant, ASN, hosting provider)
- [ ] Geolocation (country, city, ISP)
- [ ] Reputation scores (VirusTotal, AbuseIPDB, Shodan)
- [ ] Historical DNS resolution (passive DNS)
- [ ] Open ports and services (Shodan, Censys)
- [ ] Related malware samples (VirusTotal relations)
- [ ] Threat intelligence platform context (tagged campaigns, actors)

**Domain Enrichment:**
- [ ] WHOIS registration (creation date, registrant, registrar)
- [ ] DNS records (A, MX, NS, TXT)
- [ ] Passive DNS history (IP resolution history)
- [ ] Domain age (newly registered domains are higher risk)
- [ ] SSL certificate details
- [ ] Reputation scores (VirusTotal, URLScan.io)
- [ ] Categorization (malware, phishing, C2, legitimate)
- [ ] Related domains (shared infrastructure, registration patterns)

**File Hash Enrichment:**
- [ ] VirusTotal detection ratio and vendor names
- [ ] Sandbox analysis results (ANY.RUN, Joe Sandbox, Hybrid Analysis)
- [ ] Malware family classification
- [ ] YARA rule matches
- [ ] Associated C2 infrastructure
- [ ] First seen / last seen dates
- [ ] File metadata (PE info, compilation timestamp, packer detection)

### 2.2 Contextual Enrichment
Add human-analyst context:
- [ ] Associated threat actor or campaign (if known)
- [ ] MITRE ATT&CK technique mapping
- [ ] Kill chain phase (delivery, exploitation, C2, exfiltration)
- [ ] Targeted sector or geography
- [ ] Related IOCs (pivot from one indicator to associated indicators)
- [ ] Confidence assessment (see below)

### 2.3 Confidence Scoring

| Confidence Level | Score | Criteria |
|-----------------|-------|----------|
| Confirmed | 90-100 | Validated through internal analysis or multiple trusted sources |
| Probable | 70-89 | Reported by trusted source with corroborating evidence |
| Possible | 50-69 | Reported by single source, plausible but unconfirmed |
| Doubtful | 30-49 | Limited evidence, potential for false positive |
| Improbable | 0-29 | Likely false positive, contradicting evidence |

Assign Traffic Light Protocol (TLP) marking for sharing:
- TLP:RED — Named recipients only
- TLP:AMBER+STRICT — Organization only
- TLP:AMBER — Organization and clients
- TLP:GREEN — Community sharing
- TLP:CLEAR — Public

## Correlation and Analysis

### 3.1 Internal Correlation
- [ ] Search SIEM for any historical matches against new IOCs
- [ ] Check EDR telemetry for file hash or process matches
- [ ] Query proxy logs for domain/URL matches
- [ ] Search DNS logs for domain resolution attempts
- [ ] Check email gateway logs for sender address matches
- [ ] Correlate with active incidents or investigations

### 3.2 Cross-IOC Correlation
- [ ] Identify shared infrastructure between IOCs (same ASN, registrar, SSL cert)
- [ ] Map IOC clusters to campaigns or threat actors
- [ ] Identify patterns: domain generation algorithms, infrastructure rotation
- [ ] Build relationship graphs between related indicators
- [ ] Update campaign tracking (see `tasks/threat-intel/campaign-tracking.md`)

### 3.3 False Positive Assessment
Before deploying IOCs for blocking/alerting:
- [ ] Check if IP/domain hosts legitimate services (CDN, shared hosting)
- [ ] Verify domain is not a sinkhole or researcher infrastructure
- [ ] Check for overlap with organizational legitimate traffic
- [ ] Assess age of IOC (stale IOCs may be repurposed for legitimate use)
- [ ] Validate against known false positive databases

## Integration and Deployment

### 4.1 Detection Integration
Based on enrichment results, deploy IOCs to appropriate systems:

| Confidence | Action | System |
|------------|--------|--------|
| 90-100 | Auto-block + alert | Firewall, proxy, EDR, email gateway |
| 70-89 | Alert only (analyst review before block) | SIEM watchlist |
| 50-69 | Hunt query (proactive search) | SIEM search, EDR hunt |
| < 50 | Intelligence tracking only | TI platform |

### 4.2 IOC Lifecycle Management
- [ ] Set expiration dates for all deployed IOCs (default: 90 days)
- [ ] Review and extend high-confidence IOCs quarterly
- [ ] Remove expired IOCs from blocking systems
- [ ] Archive historical IOCs for future correlation
- [ ] Track IOC hit rates (deployed IOCs that actually matched)

### 4.3 Sharing
- [ ] Contribute enriched IOCs back to sharing communities (MISP, ISAC)
- [ ] Respect TLP markings on received IOCs
- [ ] Share detection rules derived from IOCs (Sigma, YARA formats)
- [ ] Collaborate with peers on IOC validation

## Automation Architecture

### 5.1 Enrichment Pipeline
```
IOC Ingestion -> Dedup -> Auto-Enrich -> Confidence Score ->
  -> High Confidence: Auto-deploy to blocking + SIEM
  -> Medium Confidence: Queue for analyst review
  -> Low Confidence: Store in TI platform only
```

### 5.2 Tools
- TI platform: MISP, OpenCTI, or commercial (ThreatConnect, Anomali)
- Enrichment: VirusTotal API, Shodan API, PassiveTotal, AbuseIPDB
- Automation: SOAR playbooks for enrichment workflows
- Visualization: Maltego, link analysis tools for relationship mapping

## Cross-References

- `tasks/threat-intel/daily-threat-briefing.md` — Briefing consumption of enriched IOCs
- `tasks/threat-intel/campaign-tracking.md` — Campaign correlation
- `tasks/threat-intel/threat-actor-profiling.md` — Actor attribution
- `workflows/detection-engineering-workflow.md` — IOC-to-detection rule pipeline
- `scripts/detection-rule-templates.md` — Detection rule formats
- `data/registries/detection-rules-registry.md` — Rule registry
