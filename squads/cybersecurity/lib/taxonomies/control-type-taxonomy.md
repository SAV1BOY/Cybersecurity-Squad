# Security Control Type Taxonomy

## Purpose

Classification of security controls by function (preventive, detective, corrective, compensating) with mapping to NIST, CIS, and ISO frameworks. Provides a reference for control selection during risk treatment.

## Control Function Categories

### Preventive Controls

Controls that prevent security incidents from occurring.

| Control | Description | Implementation Examples | NIST CSF | CIS Control | ISO 27001 |
|---------|-------------|------------------------|----------|-------------|-----------|
| Access control | Restrict access to authorized users | RBAC, ABAC, least privilege | PR.AC | 5, 6 | A.9 |
| Authentication | Verify identity before granting access | MFA, certificates, biometrics | PR.AC-7 | 6.3, 6.4 | A.9.4 |
| Encryption | Protect data confidentiality | AES-256 at rest, TLS in transit | PR.DS-1,2 | 3.10 | A.10 |
| Network segmentation | Isolate network zones | VLANs, firewalls, micro-segmentation | PR.AC-5 | 12 | A.13.1 |
| Input validation | Prevent injection attacks | Parameterized queries, allowlists | PR.DS | 16 | A.14.2 |
| Patch management | Eliminate known vulnerabilities | Automated patching, vulnerability scanning | PR.IP-12 | 7 | A.12.6 |
| Security awareness | Reduce human-factor risk | Training, phishing simulation | PR.AT | 14 | A.7.2 |
| Application allowlisting | Prevent unauthorized execution | AppLocker, WDAC, SRP | PR.IP | 2 | A.12.5 |
| Email filtering | Block malicious email | Anti-spam, sandboxing, DMARC | PR.PT | 9 | A.13.2 |
| Web filtering | Block malicious web content | Proxy, URL filtering, browser isolation | PR.PT | 9 | A.13.1 |
| Physical access control | Prevent unauthorized physical access | Badge readers, biometrics, guards | PR.AC | 3 | A.11 |
| Change management | Prevent unauthorized changes | CAB review, approval workflows | PR.IP-3 | 4 | A.12.1 |

### Detective Controls

Controls that detect security incidents during or after occurrence.

| Control | Description | Implementation Examples | NIST CSF | CIS Control | ISO 27001 |
|---------|-------------|------------------------|----------|-------------|-----------|
| Log monitoring | Detect anomalous activity | SIEM, log aggregation, correlation | DE.CM | 8 | A.12.4 |
| Intrusion detection | Detect network-based attacks | IDS/IPS, NDR | DE.CM-1 | 13 | A.13.1 |
| Endpoint detection | Detect host-based threats | EDR, antivirus, HIDS | DE.CM-4 | 10 | A.12.2 |
| File integrity monitoring | Detect unauthorized file changes | OSSEC, Tripwire, AIDE | DE.CM-7 | 3 | A.12.4 |
| Vulnerability scanning | Detect vulnerable systems | Nessus, Qualys, cloud-native | DE.CM-8 | 7 | A.12.6 |
| User behavior analytics | Detect anomalous user behavior | UEBA, machine learning | DE.AE | 6 | A.12.4 |
| Data loss prevention | Detect data exfiltration | DLP endpoint, network, cloud | DE.CM-7 | 3 | A.13.2 |
| Threat hunting | Proactively search for threats | Hypothesis-driven hunting, IOC sweeps | DE.AE | 8 | A.12.4 |
| Security assessments | Identify control weaknesses | Penetration testing, red teaming | DE.DP | 18 | A.18.2 |
| Audit logging | Record activity for review | Audit trails, database activity monitoring | DE.CM | 8 | A.12.4 |
| Anomaly detection | Detect deviations from normal | ML-based, statistical | DE.AE-1 | 8 | A.12.4 |
| Physical surveillance | Detect physical security events | CCTV, motion sensors | DE.CM-2 | 3 | A.11.1 |

### Corrective Controls

Controls that minimize the impact of security incidents and restore normal operations.

| Control | Description | Implementation Examples | NIST CSF | CIS Control | ISO 27001 |
|---------|-------------|------------------------|----------|-------------|-----------|
| Incident response | Respond to and contain incidents | IR plan, IR team, playbooks | RS.RP | 17 | A.16 |
| Backup and recovery | Restore data and systems | Immutable backups, DR sites | RC.RP | 11 | A.12.3 |
| Containment | Limit incident spread | Network isolation, account lockout | RS.MI | 17 | A.16.1 |
| Eradication | Remove threat from environment | Malware removal, reimaging | RS.MI | 17 | A.16.1 |
| Forensics | Investigate and learn from incidents | Forensic imaging, log analysis | RS.AN | 17 | A.16.1 |
| Business continuity | Maintain operations during incident | BCP, failover, alternate sites | RC.RP | 11 | A.17 |
| Communication | Coordinate response stakeholders | War room, notification procedures | RS.CO | 17 | A.16.1 |
| Lessons learned | Improve from incidents | Post-incident review, process updates | RC.IM | 17 | A.16.1 |
| Account recovery | Restore compromised accounts | Password reset, MFA re-enrollment | RS.MI | 6 | A.9 |
| Patch deployment (emergency) | Remediate exploited vulnerability | Emergency patching, virtual patching | RS.MI | 7 | A.12.6 |

### Compensating Controls

Controls that provide alternative protection when primary controls are not feasible.

| Scenario | Primary Control | Compensating Control | Justification |
|----------|----------------|---------------------|---------------|
| Legacy system cannot patch | Patch management | Network isolation + IPS + enhanced monitoring | System cannot be updated without breaking functionality |
| Application cannot implement MFA | Multi-factor authentication | IP allowlisting + enhanced logging + short session timeout | Third-party app with no MFA support |
| Cannot encrypt legacy database | Encryption at rest | Network segmentation + access controls + audit logging | Database does not support TDE |
| Cannot disable deprecated protocol | Protocol elimination | Network monitoring + IDS rules + access restriction | Business-critical application dependency |
| Cannot implement WAF | Web application firewall | Code-level input validation + IDS + rate limiting | Architecture does not support WAF |
| Cannot deploy EDR on OT systems | Endpoint detection | Network monitoring + allow-listing + physical isolation | Vendor-restricted OT environment |

### Deterrent Controls

Controls that discourage potential attackers or policy violators.

| Control | Description | Implementation |
|---------|-------------|---------------|
| Warning banners | Notify users of monitoring | Login banners, system access warnings |
| Security policies | Define consequences | AUP, disciplinary policy, NDA |
| Visible security measures | Show security presence | CCTV cameras, badge readers, guards |
| Audit communication | Users know actions are logged | Regular communication about monitoring |
| Legal notices | Legal consequences for violations | Terms of service, compliance requirements |
| Honey tokens | Detect and deter unauthorized access | Decoy files, credentials, accounts |

## Control Implementation Maturity

| Level | Description | Indicators |
|-------|-------------|------------|
| 0 - Absent | Control not implemented | No evidence of control |
| 1 - Ad Hoc | Informal, inconsistent | Manual, person-dependent |
| 2 - Defined | Documented, not consistently followed | Procedure exists, compliance variable |
| 3 - Managed | Consistently implemented and measured | Metrics collected, regular review |
| 4 - Optimized | Automated, continuously improved | Automated enforcement, feedback loop |
| 5 - Adaptive | Dynamically adjusts to threat landscape | AI/ML-driven, real-time adaptation |

## Control Selection Criteria

| Factor | Consideration |
|--------|--------------|
| Risk reduction | How much does this control reduce the identified risk? |
| Cost | Implementation and ongoing operational cost |
| Operational impact | Impact on business operations and user experience |
| Compliance | Does regulation require this specific control? |
| Coverage | Does this control address multiple risks? |
| Measurability | Can control effectiveness be measured? |
| Maintainability | Is the control sustainable long-term? |
| Integration | Does the control integrate with existing infrastructure? |
| Defense in depth | Does this control layer with existing controls? |

## Framework Cross-Reference Matrix

| Control Domain | NIST CSF | NIST 800-53 | CIS v8 | ISO 27001 | MITRE D3FEND |
|---------------|----------|-------------|--------|-----------|-------------|
| Identity | PR.AC | AC, IA | 5, 6 | A.9 | D3-AA |
| Data protection | PR.DS | SC, MP | 3 | A.8, A.10 | D3-DE |
| Network security | PR.AC, PR.PT | SC, SI | 12, 13 | A.13 | D3-NI |
| Endpoint security | PR.IP | SI, CM | 2, 10 | A.12 | D3-PE |
| Monitoring | DE.CM | AU, SI | 8 | A.12.4 | D3-DA |
| Incident response | RS.RP | IR | 17 | A.16 | D3-IRE |
| Recovery | RC.RP | CP | 11 | A.17 | D3-RE |
| Governance | ID.GV | PM, PL | 1 | A.5, A.6 | -- |
| Risk management | ID.RM | RA | 1 | A.8.2 | -- |
| Awareness | PR.AT | AT | 14 | A.7.2 | -- |

## Cross-References

- [NIST CSF](../../frameworks/nist-csf.md) -- NIST Cybersecurity Framework
- [CIS Controls v8](../../frameworks/cis-controls-v8.md) -- CIS Controls mapping
- [NIST 800-53 Controls](../../frameworks/nist-800-53-controls.md) -- detailed control catalog
- [Risk Scoring Model](../../frameworks/risk-scoring-model.md) -- risk-based control selection
