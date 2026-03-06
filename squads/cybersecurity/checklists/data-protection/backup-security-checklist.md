# Backup Security Checklist

## Purpose

Checklist for securing backup infrastructure covering encryption, access controls, air-gap verification, recovery testing, and immutability requirements. Critical for ransomware resilience.

## Backup Encryption

- [ ] All backups encrypted at rest (AES-256 minimum)
- [ ] Backup encryption keys stored separately from backup media
- [ ] Backup encryption keys escrowed in separate secure location
- [ ] Encryption keys for backups are not stored in Active Directory (ransomware risk)
- [ ] Backup encryption keys rotated annually
- [ ] Key recovery procedure documented and tested
- [ ] Backup data encrypted in transit (TLS 1.2+ for network transfers)
- [ ] Tape backups encrypted before writing (hardware or software encryption)
- [ ] Cloud backup encryption uses customer-managed keys (not provider-only)

## Access Controls

### Backup Infrastructure Access

- [ ] Backup admin accounts are dedicated (separate from domain admin)
- [ ] Backup admin accounts do not have domain admin privileges
- [ ] Backup admin credentials stored in PAM vault
- [ ] MFA required for backup admin access
- [ ] Backup admin access is logged and monitored
- [ ] Backup server management on dedicated management VLAN
- [ ] Backup agent service accounts use least privilege
- [ ] Backup server local admin password managed by LAPS or PAM
- [ ] Number of backup admins minimized and reviewed quarterly

### Backup Data Access

- [ ] Backup data access restricted to backup administrators only
- [ ] Self-service restore capability limited to user's own data
- [ ] Bulk restore requests require manager approval
- [ ] Backup catalog access restricted
- [ ] Backup storage (NAS/SAN) access controlled and logged
- [ ] Cloud backup storage access controlled via IAM policies
- [ ] No anonymous or public access to backup storage

## Air-Gap Verification

### Air-Gap Implementation

| Method | Air-Gap Level | Ransomware Resistance | Verified |
|--------|-------------|----------------------|----------|
| Physical tape, stored offsite | Full air-gap | Highest | [ ] |
| Offline disk/NAS (powered off) | Full air-gap | High | [ ] |
| Cloud immutable storage (object lock) | Logical air-gap | High | [ ] |
| Separate network segment (no routing) | Partial air-gap | Medium-High | [ ] |
| Separate account/subscription | Logical isolation | Medium | [ ] |
| Same network, different credentials | No air-gap | Low | [ ] |

### Air-Gap Verification Checks

- [ ] Air-gapped backup copy exists (at least one copy)
- [ ] Air-gapped backup is not accessible from production network
- [ ] Air-gapped backup credentials are not stored in production AD
- [ ] Air-gapped backup cannot be deleted via production admin accounts
- [ ] Air-gap verification test performed quarterly (attempt access from prod)
- [ ] Air-gapped backup includes all critical systems
- [ ] Air-gapped backup frequency sufficient for RPO requirements
- [ ] Air-gapped backup retention meets minimum requirements (90+ days)

## Recovery Testing

### Regular Recovery Tests

| Test Type | Scope | Frequency | Pass Criteria | Verified |
|-----------|-------|-----------|---------------|----------|
| File-level restore | Random files from each backup set | Monthly | File intact and accessible | [ ] |
| Application restore | Full application stack recovery | Quarterly | App functional within RTO | [ ] |
| System restore | Full server rebuild from backup | Semi-annually | System operational within RTO | [ ] |
| Full DR test | Complete environment recovery | Annually | Business operational within RTO | [ ] |
| Ransomware scenario | Recovery from immutable backup after simulated ransomware | Annually | All data recovered, no ransom | [ ] |

### Recovery Test Checklist

- [ ] Test plan documented before each recovery test
- [ ] Test recovery target is isolated (not production)
- [ ] Recovery time measured and compared to RTO
- [ ] Recovery point measured and compared to RPO
- [ ] Data integrity verified after recovery (checksums, application validation)
- [ ] Application functionality verified after recovery
- [ ] Test results documented and shared with management
- [ ] Issues identified during testing tracked to resolution
- [ ] Recovery procedures updated based on test findings

### Recovery Metrics

| Metric | Target | Last Test Result | Verified |
|--------|--------|-----------------|----------|
| RTO achievement | Within defined RTO | [result] | [ ] |
| RPO achievement | Within defined RPO | [result] | [ ] |
| File recovery success rate | 100% | [result] | [ ] |
| System recovery success rate | 100% | [result] | [ ] |
| Recovery test completion | All scheduled tests | [result] | [ ] |

## Immutability

### Immutability Configuration

- [ ] At least one backup copy is immutable (WORM / write-once-read-many)
- [ ] Immutability period cannot be shortened by backup administrators
- [ ] Immutability period meets retention requirements (minimum 30 days, recommended 90+)
- [ ] Immutable backups cover all critical systems
- [ ] Immutability mechanism is vendor-supported and validated
- [ ] Object lock or compliance lock enabled on cloud backup storage
- [ ] Retention lock enabled on tape/disk backup appliance

### Immutability Verification

- [ ] Attempted deletion of immutable backup fails (tested)
- [ ] Attempted modification of immutable backup fails (tested)
- [ ] Immutability cannot be disabled by backup admin alone (requires dual control or vendor involvement)
- [ ] Clock/time cannot be manipulated to expire immutability early
- [ ] Immutability status is monitored and alerted if changed

### Cloud-Specific Immutability

| Provider | Feature | Configuration |
|----------|---------|---------------|
| AWS S3 | Object Lock (Governance or Compliance mode) | Compliance mode recommended |
| Azure Blob | Immutable Blob Storage (legal hold or time-based) | Time-based retention policy |
| GCP Cloud Storage | Retention policy with lock | Locked retention policy |
| Veeam | Hardened Repository (Linux immutable flag) | Immutable backup repository |
| Commvault | WORM storage | WORM lock enabled |

## Backup Monitoring

### Backup Job Monitoring

- [ ] All backup job success/failure monitored
- [ ] Failed backup job alerts sent to operations team
- [ ] Consecutive failed backups escalated to management
- [ ] Backup job duration monitored (alert if significantly longer than normal)
- [ ] Backup size monitored (alert on unexpected size changes)
- [ ] Backup schedule compliance tracked (all jobs running on time)
- [ ] Backup agent health monitored on all protected systems

### Security Monitoring

| Alert | Severity | Condition |
|-------|----------|-----------|
| Backup job deleted | Critical | Any deletion of backup job |
| Retention policy changed | Critical | Retention shortened or immutability modified |
| Backup admin login outside hours | High | After-hours access to backup console |
| Bulk deletion of backup data | Critical | Mass deletion of backup sets |
| Backup agent uninstalled | High | Agent removed from protected system |
| Backup encryption disabled | Critical | Encryption setting changed |
| New admin account created | High | New backup admin created |
| Backup storage capacity warning | Medium | <20% remaining capacity |

## Ransomware-Specific Backup Hardening

### Anti-Ransomware Backup Measures

- [ ] 3-2-1-1-0 rule implemented (3 copies, 2 media, 1 offsite, 1 immutable, 0 errors)
- [ ] Backup infrastructure not domain-joined (separate auth)
- [ ] Backup admin workstation is a dedicated PAW
- [ ] Network segmentation isolates backup infrastructure from production
- [ ] Backup protocols restricted at firewall (only required ports/protocols)
- [ ] Canary files included in backup scope (detect encryption before backup)
- [ ] Backup integrity checking enabled (detect corrupted backups)
- [ ] Rapid recovery capability tested (can restore critical systems within RTO)
- [ ] Backup documentation available offline (printed or separate system)
- [ ] DR site or cloud recovery environment pre-configured

## Cross-References

- [Ransomware Defense Framework](../../frameworks/ransomware-defense-framework.md) -- ransomware response
- [Encryption Audit Checklist](encryption-audit-checklist.md) -- encryption standards
- [Data Retention Checklist](data-retention-checklist.md) -- retention alignment
- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity for backup failures
