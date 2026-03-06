# Target Corporation Data Breach (2013)

## Incident Summary

| Field | Details |
|-------|---------|
| Organization | Target Corporation (US retailer) |
| Date of Compromise | November 27 - December 15, 2013 |
| Date Discovered | December 12, 2013 (by DOJ notification) |
| Date Disclosed | December 19, 2013 |
| Records Affected | 40 million credit/debit card accounts; 70 million customer records (PII) |
| Data Exposed | Card numbers, expiration dates, CVVs, names, addresses, phone numbers, email addresses |
| Attack Vector | Third-party HVAC vendor credential compromise |
| Root Cause | Insufficient vendor access segmentation; unmonitored POS environment |
| Financial Impact | $292 million in costs; $18.5M multi-state AG settlement; $67M Visa settlement; $39.4M bank settlement |

---

## Attack Timeline

### Initial Access via Third Party
- **Prior to November 2013**: Attackers send phishing emails to Fazio Mechanical Services (HVAC vendor with Target network access for electronic billing and contract management).
- **Fazio Compromise**: Citadel banking trojan installed on Fazio systems. Credentials for Target vendor portal harvested.
- **Network Entry**: Attackers use Fazio credentials to access Target's vendor portal. From there, pivot to internal network.

### Lateral Movement and POS Compromise
- **November 15-27, 2013**: Attackers move laterally from the vendor portal network to the POS (Point-of-Sale) network segment. There was no effective segmentation between vendor-accessible networks and the POS environment.
- **November 27, 2013** (Thanksgiving weekend): RAM-scraping malware ("Kaptoxa" / BlackPOS variant) deployed to POS terminals across 1,797 Target stores.
- **November 27 - December 15, 2013**: Malware captures card data from POS terminal memory during the peak holiday shopping season.

### Data Exfiltration
- Data staged on compromised internal servers
- Exfiltrated to external FTP servers (Russia, Brazil)
- Attackers created multiple hop points to obscure exfiltration path

### Detection Failure
- **November 30, 2013**: FireEye IDS alerts trigger on malware activity. Alerts were generated and sent to Target's security operations center in Minneapolis and to a team in Bangalore.
- **Response**: No action taken on the alerts. The alerts were not escalated or investigated.
- **December 2, 2013**: Additional FireEye alerts fire. Still no response.
- **December 12, 2013**: DOJ contacts Target about the breach. Target begins internal investigation.
- **December 15, 2013**: Malware removed from POS systems.
- **December 19, 2013**: Public disclosure.

## Root Cause Analysis

### Primary Failures

**1. Third-Party Access Without Segmentation**
Fazio Mechanical, an HVAC vendor, had network access to Target for billing purposes. This access was not segmented from the POS network. A vendor needing access to a billing portal should never be a network hop away from POS terminals processing 40 million card transactions.

**2. Ignored Security Alerts**
FireEye IDS generated alerts on the malware activity. These alerts were received by both the US-based SOC and the Bangalore team. Neither team investigated or escalated. The $1.6 million FireEye deployment worked exactly as designed; the human process around it failed completely.

**3. Inadequate POS Security**
- POS terminals were running Windows Embedded, vulnerable to RAM-scraping malware
- No application whitelisting on POS terminals (malware should not have executed)
- No network monitoring of POS-to-internal communications
- No file integrity monitoring on POS systems

**4. Lateral Movement Was Trivial**
Once inside the network, attackers found minimal barriers between network zones. The vendor portal, corporate network, and POS network were insufficiently segmented, allowing lateral movement without additional authentication or authorization challenges.

**5. Data Exfiltration Went Undetected**
Large volumes of card data exfiltrated to external FTP servers over multiple weeks. No DLP controls flagged the outbound data transfer. No anomaly detection on network traffic volume.

## Lessons for Defensive Operations

### Third-Party Risk Management
- **Vendor network access must be tightly segmented** with zero trust principles
- Vendor access should be limited to specific systems and protocols needed for their function
- MFA should be required for all vendor remote access
- Vendor access should be time-limited and auditable
- Regular vendor security assessments are not optional (see `workflows/third-party-risk-assessment.md`)

### Network Segmentation
- POS/payment networks must be isolated from all other network segments
- Implement microsegmentation between vendor, corporate, and payment zones
- Monitor all cross-segment traffic with alerts on anomalies
- Test segmentation regularly with penetration testing

### Alert Response
- **Alerts without investigation are worthless security theater**
- Establish clear alert triage procedures with SLAs
- Implement alert escalation automation (if not triaged within X minutes, escalate)
- Measure and report on alert response metrics
- Conduct regular tabletop exercises using real alert scenarios

### POS / Payment Security
- Deploy application whitelisting on all POS terminals
- Implement P2PE (Point-to-Point Encryption) to protect card data in memory
- Deploy file integrity monitoring on POS systems
- Segment POS management traffic from card data traffic
- Monitor POS terminals for unauthorized process execution

### Data Exfiltration Prevention
- Deploy DLP controls on network egress
- Monitor outbound traffic for anomalous volume or destinations
- Block outbound FTP/SFTP from non-authorized systems
- Implement egress filtering with allow-list approach

## Impact and Legacy

- **CEO resignation**: Gregg Steinhafel resigned May 2014
- **CIO resignation**: Beth Jacob resigned March 2014
- **Target hired first CISO**: Created dedicated CISO role post-breach
- **Industry impact**: Accelerated EMV chip card adoption in the US
- **PCI DSS scrutiny**: Increased focus on segmentation validation in PCI assessments
- **Third-party risk**: Catalyzed industry focus on vendor risk management programs

## ATT&CK Mapping

| Tactic | Technique | Specifics |
|--------|-----------|-----------|
| Initial Access | T1199 Trusted Relationship | HVAC vendor credential compromise |
| Initial Access | T1566 Phishing | Phishing email to Fazio Mechanical |
| Lateral Movement | T1021 Remote Services | Movement from vendor network to POS |
| Execution | T1059 Command and Scripting | Malware deployment to POS systems |
| Collection | T1005 Data from Local System | RAM scraping of card data from POS memory |
| Exfiltration | T1048 Exfiltration Over Alternative Protocol | FTP to external servers |

## Cross-References

- `workflows/third-party-risk-assessment.md` — Vendor risk management
- `tasks/governance/vendor-security-review.md` — Vendor assessment task
- `workflows/insider-threat-investigation.md` — Compromised credential investigation
- `workflows/detection-engineering-workflow.md` — Alert process improvement
- `frameworks/detection-coverage-matrix.md` — Detection coverage validation
