# Ransomware Preparedness Workflow

## Purpose

Establish a comprehensive ransomware readiness program that covers prevention, detection, response, and recovery. This workflow ensures the organization can withstand, detect, and recover from ransomware attacks with minimal business impact. Built from lessons learned in incidents like NotPetya, Colonial Pipeline, and Kaseya VSA.

## Scope

All endpoints, servers, cloud workloads, backup infrastructure, and network segments. Covers both commodity ransomware and targeted human-operated ransomware (HumOR) campaigns.

## Prerequisites

- Asset inventory current (see `data/registries/asset-registry.md`)
- Incident response workflow operational (see `workflows/incident-response-workflow.md`)
- Backup infrastructure documented and accessible
- EDR deployed to all endpoints

---

## Phase 1: Ransomware Risk Assessment (Week 1-2)

### 1.1 Attack Surface Evaluation
- [ ] Identify internet-facing RDP, VPN, and remote access services
- [ ] Audit exposed SMB shares, NFS mounts, and file services
- [ ] Enumerate admin accounts with broad access (see `tasks/discovery/identity-and-privilege-mapping.md`)
- [ ] Map lateral movement paths from initial access to crown jewels
- [ ] Assess email gateway and web proxy filtering effectiveness

### 1.2 Current Control Assessment
- [ ] Validate EDR detection rules for known ransomware families
- [ ] Test email filtering against ransomware delivery vectors (macro docs, ISO, LNK)
- [ ] Verify network segmentation between IT and OT environments
- [ ] Check Group Policy restrictions on script execution (PowerShell, WScript, CScript)
- [ ] Assess privilege access management maturity

## Phase 2: Backup Validation and Hardening (Week 3-5)

### 2.1 Backup Architecture Review
- [ ] Verify 3-2-1 backup rule: 3 copies, 2 media types, 1 offsite
- [ ] Implement immutable/WORM backup storage (air-gapped or cloud object lock)
- [ ] Ensure backup credentials are separate from production Active Directory
- [ ] Test backup encryption key management and escrow
- [ ] Document RTOs and RPOs for all critical systems

### 2.2 Recovery Testing
- [ ] Conduct full bare-metal restore test for 3 critical servers
- [ ] Test Active Directory forest recovery procedure
- [ ] Validate database restore and integrity check process
- [ ] Test cloud workload snapshot restore
- [ ] Time each recovery and compare against stated RTO
- [ ] Document gaps and remediation actions

### 2.3 Backup Monitoring
- [ ] Alert on backup job failures within 1 hour
- [ ] Monitor for unauthorized access to backup infrastructure
- [ ] Detect backup deletion or retention policy changes
- [ ] Validate backup integrity with weekly hash verification

## Phase 3: Detection Rule Deployment (Week 6-8)

### 3.1 Pre-Ransomware Indicators
Deploy detection for precursor activities commonly seen before ransomware deployment:
- [ ] Mass credential harvesting (Mimikatz, LSASS dumps, DCSync)
- [ ] Cobalt Strike / Sliver / Brute Ratel beacon patterns
- [ ] Lateral movement via PsExec, WMI, WinRM across multiple hosts
- [ ] Service account anomalous logons outside business hours
- [ ] Group Policy modification (potential for GPO-based deployment)
- [ ] Shadow copy deletion (vssadmin, wmic, PowerShell)

### 3.2 Ransomware Execution Indicators
- [ ] High-entropy file write bursts (file extension changes en masse)
- [ ] Ransom note file creation patterns (README.txt, DECRYPT.html variants)
- [ ] Known ransomware process names and mutex patterns
- [ ] Encryption library loading by unusual processes
- [ ] Mass file rename operations exceeding baseline thresholds

### 3.3 Data Exfiltration Indicators
Modern ransomware uses double extortion; detect data staging and exfiltration:
- [ ] Large archive creation (7z, RAR, ZIP) on servers
- [ ] Unusual outbound data volume to cloud storage (Mega, Dropbox, rclone)
- [ ] DNS tunneling patterns
- [ ] FTP/SCP transfers from non-standard hosts

## Phase 4: Response Procedures (Week 9-11)

### 4.1 Immediate Containment (First 30 Minutes)
1. Isolate affected hosts at the network level (switch port disable, EDR isolation)
2. Disable compromised accounts immediately
3. Block known C2 domains/IPs at firewall and DNS
4. Preserve forensic evidence: memory dump, disk image of patient zero
5. Activate incident response team and bridge call

### 4.2 Scoping (Hours 1-4)
1. Query EDR for ransomware binary hash across all endpoints
2. Search SIEM for lateral movement from patient zero
3. Identify all systems that communicated with known C2 infrastructure
4. Determine if data exfiltration occurred (check proxy logs, DLP alerts)
5. Establish timeline of attacker activity

### 4.3 Decision Framework: To Pay or Not to Pay
- Consult legal counsel on OFAC sanctions screening for threat actor
- Assess whether backups are viable for recovery
- Calculate business impact of extended downtime vs. ransom payment
- Engage law enforcement (FBI IC3, CISA) regardless of payment decision
- Document decision rationale for board and regulators

### 4.4 Eradication
- [ ] Identify and remove all persistence mechanisms
- [ ] Reset all compromised credentials (broad reset if scope unclear)
- [ ] Patch exploited vulnerabilities
- [ ] Rebuild compromised systems from clean images
- [ ] Validate clean state with forensic scan before reconnection

## Phase 5: Recovery and Hardening (Week 12+)

### 5.1 Phased Recovery
1. Restore Active Directory and DNS first
2. Bring up authentication infrastructure (MFA, RADIUS)
3. Restore critical business applications per priority list
4. Validate data integrity post-restore
5. Monitor restored systems intensively for 30 days

### 5.2 Post-Incident Hardening
- [ ] Implement application allowlisting on servers
- [ ] Deploy LAPS or equivalent for local admin passwords
- [ ] Enable Credential Guard on Windows endpoints
- [ ] Segment backup networks from production
- [ ] Implement canary files for early ransomware detection

## Readiness Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Backup restore success rate | 100% | _____% |
| Mean time to detect ransomware precursors | < 1 hour | _____ |
| Recovery time for critical systems | < 4 hours | _____ |
| Immutable backup coverage | 100% of critical data | _____% |
| Ransomware tabletop frequency | Quarterly | _____ |

## Cross-References

- `workflows/incident-response-workflow.md` — IR activation
- `workflows/data-breach-response.md` — If data exfiltration confirmed
- `archive/notable-breaches/notpetya-2017.md` — NotPetya lessons
- `archive/notable-breaches/kaseya-2021.md` — Supply chain ransomware
- `scripts/detection-rule-templates.md` — Sigma rules for ransomware detection

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
