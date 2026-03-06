# Incident Type Taxonomy

## Purpose

Classification taxonomy for security incidents covering malware, unauthorized access, denial of service, data breach, and insider threat categories with severity modifiers for consistent incident classification.

## Primary Incident Categories

### Category 1: Malware

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| Ransomware | Encryption of files/systems for ransom | SEV-1/SEV-2 | File encryption, ransom note, shadow copy deletion | Isolate, preserve, assess scope |
| Wiper | Destructive malware destroying data | SEV-1 | Mass file deletion, MBR overwrite, boot failure | Isolate immediately, DR activation |
| Trojan/RAT | Remote access trojan providing persistent access | SEV-2 | C2 beacon, process injection, credential access | Isolate, investigate C2, scope |
| Cryptominer | Unauthorized cryptocurrency mining | SEV-3/SEV-4 | High CPU, known mining pool connections | Remove, investigate entry vector |
| Worm | Self-propagating malware | SEV-1/SEV-2 | Rapid spread, network scanning, exploit attempts | Segment network, block propagation |
| Rootkit | Kernel/firmware-level persistent malware | SEV-1 | Hidden processes, integrity failures, boot anomalies | Isolate, reimage, firmware check |
| Botnet | System enrolled in botnet | SEV-2/SEV-3 | C2 traffic, DDoS participation, spam relay | Isolate, remove, monitor network |
| Fileless malware | In-memory-only execution | SEV-2 | PowerShell abuse, WMI events, registry persistence | Memory capture, endpoint forensics |
| Adware/PUP | Unwanted but not actively malicious | SEV-4 | Browser modifications, pop-ups, bundled software | Remove, educate user |

### Category 2: Unauthorized Access

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| External intrusion | Unauthorized access from external attacker | SEV-1/SEV-2 | Anomalous external access, exploit evidence | Contain, investigate scope and method |
| Account compromise | Legitimate account taken over | SEV-2/SEV-3 | Impossible travel, credential stuffing, MFA bypass | Reset credentials, revoke sessions |
| Privilege escalation | Attacker elevates privileges | SEV-1/SEV-2 | Admin actions by non-admin, exploit of priv esc vuln | Revoke elevated access, patch |
| Unauthorized system access | Access to system without authorization | SEV-3 | Access from unauthorized source, policy violation | Restrict access, review authorization |
| Physical intrusion | Unauthorized physical access | SEV-2/SEV-3 | Badge anomaly, tailgating, forced entry | Physical security response, assess impact |
| Wireless intrusion | Unauthorized wireless access | SEV-3 | Rogue AP, evil twin, WPA cracking | Locate, disable, assess exposure |

### Category 3: Denial of Service

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| Volumetric DDoS | Flood-based attack overwhelming bandwidth | SEV-2/SEV-3 | Bandwidth saturation, upstream congestion | DDoS mitigation, ISP coordination |
| Application-layer DDoS | Targeted application exhaustion | SEV-2 | HTTP flood, slow requests, connection exhaustion | WAF, rate limiting, scaling |
| Amplification attack | Reflected/amplified traffic | SEV-2/SEV-3 | DNS/NTP/SSDP amplification traffic | BCP38 filtering, mitigation service |
| Ransom DDoS | DDoS with extortion demand | SEV-2 | Threat email + DDoS attack | DDoS mitigation, law enforcement |
| Resource exhaustion | Internal resource depletion (intentional) | SEV-3 | Disk full, memory exhaustion, fork bomb | Identify source, remediate |
| Service disruption (attack-caused) | Service outage resulting from attack | SEV-1/SEV-2 | Service unavailable, attack evidence | Restore service, investigate cause |

### Category 4: Data Breach / Data Exposure

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| Data exfiltration | Confirmed data theft by attacker | SEV-1 | DLP alerts, large outbound transfers, C2 | Contain, assess data classification |
| Accidental exposure | Unintentional data publication | SEV-2/SEV-3 | Public S3 bucket, email misdirection | Remove access, assess exposure |
| Database breach | Unauthorized database access/extraction | SEV-1 | SQL injection, DB access anomaly, export | Isolate database, assess data |
| PII breach | Personal data compromised | SEV-1/SEV-2 | Any breach involving personal data | Legal notification, regulatory assessment |
| Credential leak | Credentials exposed publicly | SEV-2 | Credentials on GitHub, paste site, dark web | Rotate credentials, assess impact |
| IP theft | Intellectual property stolen | SEV-1 | Source code, designs, trade secrets accessed | Contain, legal coordination |
| Payment card breach | PCI data compromised | SEV-1 | Card data exposed, POS compromise | PCI forensic investigation, card brand notification |

### Category 5: Insider Threat

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| Malicious insider (data theft) | Intentional data theft by employee | SEV-1/SEV-2 | Bulk data access, USB usage, personal email | Legal + HR coordination, monitor |
| Malicious insider (sabotage) | Intentional system/data destruction | SEV-1 | Data deletion, configuration changes, logic bombs | Contain, legal, preserve evidence |
| Negligent insider | Accidental security violation | SEV-3/SEV-4 | Policy violation, mishandling, misconfiguration | Educate, remediate, assess impact |
| Compromised insider | Employee account/device compromised | SEV-2 | Phishing victim, malware on device | Treat as external compromise + insider |
| Departing employee data theft | Data taken before/during departure | SEV-2 | Data hoarding, USB, personal email transfers | HR coordination, access review |
| Fraud | Financial fraud leveraging internal access | SEV-2 | Unauthorized transactions, approval bypass | Legal, financial investigation |

### Category 6: Policy Violation

| Sub-Type | Description | Typical Severity | Key Indicators | Initial Response |
|----------|-------------|-----------------|----------------|-----------------|
| Acceptable use violation | Violation of AUP | SEV-4 | Inappropriate usage, unauthorized software | HR notification, remediate |
| Shadow IT | Unauthorized cloud/SaaS usage | SEV-3/SEV-4 | Unknown cloud services, data in unapproved apps | CASB detection, risk assessment |
| Configuration violation | System misconfigured against policy | SEV-3/SEV-4 | Compliance scan failure, drift detection | Remediate, investigate root cause |
| Third-party policy violation | Vendor violates security requirements | SEV-3 | Vendor audit failure, breach notification | Vendor management, contract review |

## Severity Modifiers

### Factors That Increase Severity

| Modifier | Effect | Example |
|----------|--------|---------|
| Regulated data involved | +1 severity level | PII, PHI, PCI data compromised |
| Active exploitation ongoing | +1 severity level | Attacker still present in environment |
| Internet-facing system | +1 severity level | Web server vs. internal system |
| Critical business system | +1 severity level | Revenue-generating, safety-critical |
| Multiple systems affected | +1 severity level | Worm spreading, lateral movement |
| Evidence of data exfiltration | +1 severity level | Confirmed data leaving network |
| Executive/VIP target | +1 severity level | CEO email compromised |
| Public visibility | +1 severity level | Defacement, media attention |

### Factors That Decrease Severity

| Modifier | Effect | Example |
|----------|--------|---------|
| Contained to single system | -1 severity level | Malware isolated on one workstation |
| No sensitive data accessible | -1 severity level | System processes only public data |
| Compensating controls effective | -1 severity level | WAF blocked exploitation attempt |
| Development/test environment | -1 severity level | Unless contains production data |
| Detected and contained quickly | -1 severity level | <1 hour containment |
| Known false positive pattern | Close incident | After verification |

## Classification Decision Tree

```
1. What happened?
   -> Identify primary category (Malware, Unauthorized Access, etc.)

2. What sub-type?
   -> Select specific sub-type within category

3. Base severity?
   -> Assign based on sub-type typical severity

4. Apply modifiers:
   -> Check increasing factors (regulated data, active exploitation, etc.)
   -> Check decreasing factors (contained, no sensitive data, etc.)
   -> Adjust severity level accordingly

5. Final classification:
   -> Category.SubType.Severity
   -> Example: "Malware.Ransomware.SEV-1"
   -> Example: "UnauthorizedAccess.AccountCompromise.SEV-2"
```

## Incident Metrics by Category

| Category | Metric | Target |
|----------|--------|--------|
| All incidents | Mean time to detect (MTTD) | <24 hours |
| All incidents | Mean time to contain (MTTC) | <4 hours (SEV-1), <24 hours (SEV-2) |
| All incidents | Mean time to recover (MTTR) | <24 hours (SEV-1), <72 hours (SEV-2) |
| Malware | Containment rate | >95% prevented from spreading |
| Unauthorized Access | Detection rate | >80% detected before impact |
| Data Breach | Notification timeline | Per regulatory requirement |
| Insider Threat | Detection to investigation | <5 business days |

## Cross-References

- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity definitions
- [Incident Response Workflow](../../workflows/incident-response-workflow.md) -- response procedures
- [Incident Registry](../../data/registries/incident-registry.md) -- tracking
- [Threat Actor Taxonomy](threat-actor-taxonomy.md) -- actor classification
