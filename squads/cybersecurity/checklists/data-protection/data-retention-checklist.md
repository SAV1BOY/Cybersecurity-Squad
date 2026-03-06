# Data Retention Review Checklist

## Purpose

Checklist for reviewing data retention practices covering policy compliance, automated deletion, legal hold management, and verification procedures.

## Retention Policy Review

### Policy Documentation

- [ ] Data retention policy exists, is approved, and current (reviewed within 12 months)
- [ ] Retention periods defined for all data categories
- [ ] Regulatory requirements mapped to data categories
- [ ] Business requirements documented for retention beyond regulatory minimum
- [ ] Policy covers all storage locations (on-premises, cloud, SaaS, backups)
- [ ] Policy addresses structured and unstructured data
- [ ] Policy is accessible to data owners and custodians
- [ ] Policy has clear ownership and review cycle

### Retention Schedule

| Data Category | Regulatory Basis | Retention Period | Destruction Method | Owner | Verified |
|--------------|-----------------|-----------------|-------------------|-------|----------|
| Financial records | SOX, tax law | 7 years | Secure deletion | Finance | [ ] |
| Employee records | Labor law | Duration + 7 years | Secure deletion | HR | [ ] |
| Customer PII | GDPR, CCPA | Duration of relationship + 3 years | Cryptographic erasure | Legal | [ ] |
| Health records | HIPAA | 6 years from last activity | NIST 800-88 Purge | Compliance | [ ] |
| Payment card data | PCI DSS | As needed for business | Secure deletion | Finance | [ ] |
| Email | Business need | 3-7 years | Auto-purge | IT | [ ] |
| Security logs | Compliance + incident | 1-3 years | Standard deletion | Security | [ ] |
| Backup data | Recovery need | 90 days to 1 year | Media destruction | IT | [ ] |
| Website analytics | Business need | 26 months (GDPR guidance) | Platform deletion | Marketing | [ ] |
| Contracts | Legal | Duration + 7 years | Secure deletion | Legal | [ ] |

## Automated Deletion

### Automation Implementation

- [ ] Automated retention enforcement deployed for major data stores
- [ ] Retention policies configured in email system (auto-archive/delete)
- [ ] Retention policies configured in cloud storage (lifecycle policies)
- [ ] Retention policies configured in databases (automated purge jobs)
- [ ] Retention policies configured in SaaS applications
- [ ] Automated deletion logs are maintained for audit evidence
- [ ] Automation is tested before production deployment
- [ ] Automation does not delete data under legal hold

### Automation Checks

| Platform | Retention Policy | Automation Status | Last Verified |
|----------|-----------------|-------------------|---------------|
| Microsoft 365 (email) | Retention labels + policies | [ ] Configured | [ ] |
| SharePoint/OneDrive | Retention labels + policies | [ ] Configured | [ ] |
| AWS S3 | Lifecycle policies | [ ] Configured | [ ] |
| Azure Blob Storage | Lifecycle management | [ ] Configured | [ ] |
| GCP Cloud Storage | Lifecycle rules | [ ] Configured | [ ] |
| Production databases | Scheduled purge jobs | [ ] Configured | [ ] |
| Data warehouse | Partition management | [ ] Configured | [ ] |
| Backup system | Retention policy on backup sets | [ ] Configured | [ ] |
| Log management (SIEM) | Index retention policies | [ ] Configured | [ ] |

### Edge Cases

- [ ] Deleted user accounts: data ownership transferred before deletion
- [ ] Decommissioned systems: data migrated or destroyed per policy
- [ ] Merged/acquired company data: retention policy applied to acquired data
- [ ] Third-party/vendor data: vendor contracts specify retention obligations
- [ ] Temporary/project data: cleanup process after project completion
- [ ] Development/test data: production data in non-prod environments has same retention
- [ ] Shadow IT data: discovered unauthorized data stores addressed

## Legal Hold Management

### Legal Hold Process

- [ ] Legal hold policy documented and approved by legal counsel
- [ ] Legal hold issuance process defined (who can issue, how)
- [ ] Legal hold notification template exists
- [ ] Legal hold acknowledgment tracked (recipients confirm receipt)
- [ ] Legal hold scope clearly defined (custodians, date range, data types)
- [ ] Legal hold overrides retention deletion (no auto-delete of held data)
- [ ] Legal hold preserved data is protected from modification
- [ ] Legal hold status tracked centrally
- [ ] Legal hold release process documented (with legal counsel approval)
- [ ] Released data returns to normal retention processing

### Legal Hold Checklist

| Hold Activity | Requirement | Verified |
|--------------|-------------|----------|
| Hold notification sent | Within 48 hours of legal trigger | [ ] |
| Custodians identified | All relevant data custodians listed | [ ] |
| Hold acknowledged | All custodians confirm in writing | [ ] |
| Auto-deletion suspended | Retention policies paused for held data | [ ] |
| Scope documented | Data types, date range, systems specified | [ ] |
| Hold register updated | Central register shows active holds | [ ] |
| Periodic reminder | Quarterly reminder to custodians | [ ] |
| Hold release approved | Legal counsel written approval | [ ] |
| Auto-deletion resumed | Retention policies re-enabled | [ ] |

## Verification

### Retention Compliance Verification

- [ ] Quarterly sample audit of data stores for retention compliance
- [ ] Verify data older than retention period has been deleted
- [ ] Verify legal hold data has NOT been deleted
- [ ] Verify destruction certificates generated for physical media
- [ ] Verify automated deletion logs match expected deletions
- [ ] Verify backup retention aligns with data retention policy
- [ ] Verify SaaS application data retention meets policy

### Verification Procedures

| Verification | Method | Frequency | Owner |
|-------------|--------|-----------|-------|
| Email retention | Sample mailboxes for age compliance | Quarterly | IT |
| File share retention | Scan for files beyond retention | Quarterly | IT |
| Database retention | Query for records beyond retention | Quarterly | DBA |
| Cloud storage retention | Review lifecycle policy compliance | Quarterly | Cloud team |
| Backup retention | Verify oldest backup set age | Monthly | Backup team |
| Physical media destruction | Review destruction certificates | Semi-annually | IT |
| Legal hold integrity | Verify held data exists and is intact | Quarterly | Legal |

### Data Discovery (for Retention Gaps)

- [ ] Data discovery scan performed annually to identify unknown data stores
- [ ] Discovered data classified and retention policy applied
- [ ] Data in unauthorized locations (shadow IT) identified and addressed
- [ ] Personal devices checked for corporate data (if applicable per policy)
- [ ] Departed employee data reviewed and processed per policy
- [ ] Contractor data stores reviewed at contract end

## Destruction Verification

### Destruction Methods by Data Type

| Data Type | Destruction Method | Standard | Evidence |
|-----------|-------------------|----------|----------|
| Digital (standard) | Secure deletion (overwrite) | NIST 800-88 Clear | Deletion log |
| Digital (sensitive) | Cryptographic erasure or overwrite | NIST 800-88 Purge | Certificate |
| Physical media (HDD) | Degauss + physical destruction | NIST 800-88 Destroy | Certificate + photos |
| Physical media (SSD) | Cryptographic erase + physical destruction | NIST 800-88 Destroy | Certificate |
| Paper documents | Cross-cut shredding | DIN 66399 P-4+ | Shredding log |
| Cloud data | Platform deletion + key destruction | Platform-specific | Platform confirmation |

### Destruction Documentation

- [ ] Destruction request initiated by data owner
- [ ] Destruction approved per policy (classification-appropriate)
- [ ] Destruction performed by authorized personnel or vendor
- [ ] Destruction evidence collected (certificates, logs, photos)
- [ ] Destruction evidence retained per audit requirements
- [ ] Asset register updated (media decommissioned)

## Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| Data stores with retention policy applied | 100% | Quarterly |
| Automated retention enforcement coverage | >90% | Quarterly |
| Overdue data (beyond retention, not deleted) | 0 | Quarterly |
| Legal holds properly maintained | 100% | Quarterly |
| Destruction certificates complete | 100% | Per event |
| Retention policy review currency | Within 12 months | Annual |

## Cross-References

- [Data Classification Framework](../../frameworks/data-classification-framework.md) -- classification drives retention
- [Privacy Impact Checklist](privacy-impact-checklist.md) -- GDPR retention requirements
- [Backup Security Checklist](backup-security-checklist.md) -- backup retention alignment
- [Encryption Audit Checklist](encryption-audit-checklist.md) -- cryptographic erasure
