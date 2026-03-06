# Equifax Data Breach (2017)

## Incident Summary

| Field | Details |
|-------|---------|
| Organization | Equifax Inc. (credit reporting agency) |
| Date Discovered | July 29, 2017 |
| Date Disclosed | September 7, 2017 |
| Records Affected | 147.9 million Americans, 15.2 million UK citizens, ~19,000 Canadians |
| Data Exposed | Names, SSNs, birth dates, addresses, driver's license numbers, credit card numbers (209,000) |
| Attack Vector | Apache Struts vulnerability (CVE-2017-5638) |
| Root Cause | Failure to patch known critical vulnerability within 48 hours of advisory |
| Financial Impact | $1.4 billion+ in costs; $700M FTC settlement |

---

## Attack Timeline

### Pre-Compromise
- **March 7, 2017**: Apache Struts CVE-2017-5638 disclosed. Remote code execution via crafted Content-Type header. CVSS 10.0.
- **March 8, 2017**: US-CERT advisory issued. Equifax IT staff received notification.
- **March 9, 2017**: Equifax internal email directed patching. Patch was not applied to all systems.
- **March 15, 2017**: Equifax ran vulnerability scans but failed to detect the unpatched web portal.

### Compromise
- **May 13, 2017**: Attackers exploit CVE-2017-5638 on consumer dispute portal.
- **May-July 2017**: Attackers move laterally, accessing 48+ databases. Extract data in small batches to avoid detection.
- **May-July 2017**: Attackers operate for 76 days undetected.

### Discovery and Response
- **July 29, 2017**: Equifax updates expired SSL inspection certificate on network monitoring tool. Immediately detects suspicious traffic. System had been blind for 19 months due to expired cert.
- **July 30, 2017**: Suspicious traffic blocked; forensic investigation begins.
- **August 2, 2017**: Equifax notifies FBI.
- **September 7, 2017**: Public disclosure.

## Root Cause Analysis

### Primary Failures

**1. Patch Management Failure**
The single most critical failure. A known, actively exploited vulnerability with a CVSS score of 10.0 was not patched for over two months despite:
- US-CERT advisory distribution
- Internal Equifax security email
- Availability of the patch on the day of disclosure

**2. Network Monitoring Blindspot**
An SSL inspection certificate on Equifax's network monitoring tool expired in January 2016. For 19 months, encrypted traffic was not being inspected. The breach was detected within hours of certificate renewal, proving that the existing detection capability would have caught the attack much sooner.

**3. Inadequate Network Segmentation**
Once attackers gained access through the web portal, they were able to move laterally to 48 databases containing consumer data. Insufficient segmentation allowed a single compromised web server to become a gateway to the organization's most sensitive data.

**4. Stored Credentials in Plaintext**
Attackers found database credentials stored in plaintext configuration files on the compromised web server. This provided direct access to backend databases without needing to escalate privileges further.

**5. Inadequate Vulnerability Scanning**
Equifax's vulnerability scans failed to detect the unpatched Apache Struts instance. The scanning scope did not cover all internet-facing assets, or the scanner did not have the proper plugin to detect the vulnerability.

## Lessons for Defensive Operations

### Patch Management
- **Critical CVEs must have emergency patch SLAs** (24-48 hours for CVSS 9.0+, especially with known exploitation)
- Asset inventory must be comprehensive; you cannot patch what you do not know about
- Vulnerability scanning must validate patch deployment, not just policy compliance
- Apache Struts and similar web application framework patches require application restart, making them operationally challenging but not optional

### Network Security
- **SSL inspection certificates must be monitored with automated alerting before expiration**
- Network segmentation must isolate web-facing applications from backend databases
- East-west traffic monitoring is as important as perimeter monitoring
- Data stores containing PII must be in isolated network segments with strict access controls

### Credential Management
- Never store database credentials in plaintext configuration files
- Use secrets management solutions (HashiCorp Vault, AWS Secrets Manager)
- Implement credential rotation on a regular schedule
- Database access should require application-level authentication, not just network access

### Detection and Response
- Network monitoring tools must be monitored themselves (meta-monitoring)
- DLP controls should detect bulk extraction of PII-type data
- Database query auditing should flag anomalous access patterns
- 76-day dwell time is unacceptable for a breach of this magnitude

## Regulatory Impact

- **FTC Settlement**: $700 million (largest data breach settlement at the time)
- **Consumer Fund**: $425 million for affected individuals
- **Congressional Hearings**: CEO testified before multiple committees
- **Executive Consequences**: CIO and CSO "retired" immediately after disclosure; CEO departed
- **New Regulations**: Accelerated passage of breach notification laws in several states
- **Industry Impact**: Prompted reassessment of credit bureau security across the industry

## ATT&CK Mapping

| Tactic | Technique | Specifics |
|--------|-----------|-----------|
| Initial Access | T1190 Exploit Public-Facing Application | Apache Struts CVE-2017-5638 |
| Credential Access | T1552 Unsecured Credentials | Plaintext credentials in config files |
| Lateral Movement | T1021 Remote Services | Database access from web server |
| Collection | T1005 Data from Local System | Database queries for consumer data |
| Exfiltration | T1041 Exfiltration Over C2 Channel | Data exfiltrated in encrypted streams |

## Cross-References

- `tasks/governance/compliance-gap-analysis.md` — Compliance assessment
- `frameworks/vuln-triage-playbook.md` — Vulnerability prioritization
- `tasks/threat-intel/vulnerability-intelligence.md` — Vulnerability monitoring
- `workflows/data-breach-response.md` — Breach response workflow
- `workflows/security-metrics-reporting.md` — Patch compliance metrics
