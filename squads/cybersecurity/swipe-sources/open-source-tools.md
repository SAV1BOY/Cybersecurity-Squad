# Open-Source Security Tools

## Purpose

This curated catalog of open-source security tools is organized by category with maturity ratings, use cases, and integration notes. Open-source tools form the backbone of modern security operations — from detection to testing to forensics. This list focuses on tools that are actively maintained, well-documented, and production-worthy.

## Maturity Rating Scale

| Rating | Meaning |
|--------|---------|
| Mature | Widely adopted, well-maintained, extensive documentation, stable API, suitable for production |
| Established | Active development, growing community, solid documentation, reliable for most use cases |
| Emerging | Promising but newer, active development, documentation may be incomplete, evaluate before production use |

## Reconnaissance and OSINT

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Amass** | Attack surface mapping, DNS enumeration, subdomain discovery | Mature | https://github.com/owasp-amass/amass |
| **Subfinder** | Fast passive subdomain enumeration | Established | https://github.com/projectdiscovery/subfinder |
| **httpx** | HTTP probing and technology fingerprinting | Established | https://github.com/projectdiscovery/httpx |
| **Shodan CLI** | Internet-connected device search (API key required) | Mature | https://github.com/achillean/shodan-python |
| **theHarvester** | Email, subdomain, and name harvesting from public sources | Mature | https://github.com/laramies/theHarvester |
| **SpiderFoot** | Automated OSINT collection and correlation | Established | https://github.com/smicallef/spiderfoot |
| **Recon-ng** | Modular web reconnaissance framework | Mature | https://github.com/lanmaster53/recon-ng |

## Vulnerability Scanning and Assessment

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Nuclei** | Template-based vulnerability scanner, fast and extensible | Mature | https://github.com/projectdiscovery/nuclei |
| **OpenVAS (Greenbone)** | Full-featured vulnerability scanner | Mature | https://github.com/greenbone/ |
| **Nikto** | Web server vulnerability scanner | Mature | https://github.com/sullo/nikto |
| **Trivy** | Container, filesystem, and IaC vulnerability scanning | Mature | https://github.com/aquasecurity/trivy |
| **Grype** | Container image vulnerability scanner | Established | https://github.com/anchore/grype |
| **Semgrep** | Static analysis for code security (SAST) | Mature | https://github.com/semgrep/semgrep |
| **Checkov** | Infrastructure-as-code static analysis | Established | https://github.com/bridgecrewio/checkov |

## Exploitation and Penetration Testing

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Metasploit Framework** | Exploitation framework, payload generation, post-exploitation | Mature | https://github.com/rapid7/metasploit-framework |
| **Burp Suite Community** | Web application security testing (Community Edition is free) | Mature | https://portswigger.net/burp/communitydownload |
| **SQLMap** | Automated SQL injection detection and exploitation | Mature | https://github.com/sqlmapproject/sqlmap |
| **Impacket** | Network protocol tools, AD attacks, credential harvesting | Mature | https://github.com/fortra/impacket |
| **CrackMapExec / NetExec** | Active Directory and network post-exploitation | Established | https://github.com/Pennyw0rth/NetExec |
| **Responder** | LLMNR/NBT-NS/mDNS poisoner for credential capture | Mature | https://github.com/lgandx/Responder |
| **BloodHound** | Active Directory attack path analysis | Mature | https://github.com/BloodHoundAD/BloodHound |
| **Certipy** | Active Directory Certificate Services exploitation | Established | https://github.com/ly4k/Certipy |

## Defense, Detection, and Monitoring

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Wazuh** | SIEM, EDR, vulnerability detection, compliance | Mature | https://github.com/wazuh/wazuh |
| **Suricata** | Network IDS/IPS, network security monitoring | Mature | https://github.com/OISF/suricata |
| **Zeek (Bro)** | Network analysis framework, connection logging, protocol analysis | Mature | https://github.com/zeek/zeek |
| **YARA** | Malware classification and pattern matching | Mature | https://github.com/VirusTotal/yara |
| **Sigma** | Generic signature format for SIEM detections | Mature | https://github.com/SigmaHQ/sigma |
| **Velociraptor** | Endpoint visibility, DFIR, threat hunting | Established | https://github.com/Velocidex/velociraptor |
| **Osquery** | SQL-based endpoint visibility | Mature | https://github.com/osquery/osquery |
| **CrowdSec** | Collaborative IPS, behavior-based detection | Established | https://github.com/crowdsecurity/crowdsec |
| **Falco** | Cloud-native runtime security (Kubernetes, containers) | Mature | https://github.com/falcosecurity/falco |

## Digital Forensics and Incident Response

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Autopsy / Sleuth Kit** | Disk forensics, file system analysis | Mature | https://github.com/sleuthkit/autopsy |
| **Volatility 3** | Memory forensics framework | Mature | https://github.com/volatilityfoundation/volatility3 |
| **KAPE** | Evidence collection and triage (free, not open-source) | Established | https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape |
| **Plaso / Log2Timeline** | Timeline creation from various log sources | Mature | https://github.com/log2timeline/plaso |
| **Eric Zimmerman Tools** | Windows forensic artifact parsers | Mature | https://ericzimmerman.github.io/ |
| **Chainsaw** | Windows event log analysis and sigma rule matching | Established | https://github.com/WithSecureLabs/chainsaw |
| **RITA** | Network traffic analysis for threat hunting | Established | https://github.com/activecm/rita |

## Cloud Security

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Prowler** | AWS/Azure/GCP security assessment | Mature | https://github.com/prowler-cloud/prowler |
| **ScoutSuite** | Multi-cloud security auditing | Established | https://github.com/nccgroup/ScoutSuite |
| **CloudSploit** | Cloud security configuration monitoring | Established | https://github.com/aquasecurity/cloudsploit |
| **Cartography** | Cloud infrastructure graph and attack surface mapping | Established | https://github.com/lyft/cartography |
| **Steampipe** | SQL-based cloud resource querying | Established | https://github.com/turbot/steampipe |
| **Pacu** | AWS exploitation framework | Established | https://github.com/RhinoSecurityLabs/pacu |

## Password and Credential Tools

| Tool | Purpose | Maturity | URL |
|------|---------|----------|-----|
| **Hashcat** | GPU-accelerated password cracking | Mature | https://github.com/hashcat/hashcat |
| **John the Ripper** | CPU-based password cracking | Mature | https://github.com/openwall/john |
| **Hydra** | Network login brute-forcing | Mature | https://github.com/vanhauser-thc/thc-hydra |
| **KeePassXC** | Password manager (for team credential storage) | Mature | https://github.com/keepassxreboot/keepassxc |

## Tool Selection Criteria

When evaluating a new tool for the squad:

1. **Active maintenance**: Last commit within 6 months, responsive issue tracker
2. **Community size**: Star count is a proxy but check actual contributor diversity
3. **Documentation quality**: If you cannot figure out how to use it in 30 minutes, documentation is insufficient
4. **Integration capability**: Can it output structured data (JSON/CSV) for pipeline integration?
5. **License compatibility**: Verify the license permits your intended use (commercial, modification, redistribution)
6. **Security of the tool itself**: Review the tool's own security posture — a compromised security tool is a supply chain attack

## Cross-References

- See `swipe-sources/training-platforms.md` for platforms where these tools can be practiced
- See `swipe-sources/vulnerability-databases.md` for vulnerability data these tools consume
- See `swipe-sources/conference-talks.md` for talks demonstrating these tools
- See `voice/tone-profiles/technical-operator.md` for documenting tool usage in reports
