# Data Classification Framework

## Purpose

Establish a uniform data classification system that drives handling requirements, access controls, encryption standards, retention policies, and destruction procedures. Classification is the foundation of data protection -- without it, controls cannot be appropriately scoped.

## Classification Levels

| Level | Label | Description | Examples |
|-------|-------|-------------|----------|
| 4 | **Restricted** | Highest sensitivity. Unauthorized disclosure causes severe harm, regulatory penalties, or existential risk | PII/PHI, payment card data, trade secrets, M&A data, cryptographic keys, incident forensic data |
| 3 | **Confidential** | Sensitive business data. Disclosure causes significant financial or reputational harm | Financial reports (pre-release), customer lists, security assessments, architecture diagrams, source code |
| 2 | **Internal** | Not intended for public release. Disclosure causes minor impact | Internal policies, org charts, meeting notes, project plans, internal communications |
| 1 | **Public** | Approved for external release. No impact from disclosure | Marketing materials, published documentation, public website content, open-source code |

## Labeling Requirements

### Document Labeling

| Classification | Header/Footer | Filename Convention | Metadata Tag |
|---------------|---------------|--------------------:|-------------|
| Restricted | "RESTRICTED" in red, every page | `[R]-filename` | `classification:restricted` |
| Confidential | "CONFIDENTIAL" in orange, every page | `[C]-filename` | `classification:confidential` |
| Internal | "INTERNAL" in blue, first page | `[I]-filename` | `classification:internal` |
| Public | None required | No prefix | `classification:public` |

### Digital Asset Labeling
- Apply DLP classification tags (Microsoft Information Protection, Google DLP, or equivalent)
- Database columns containing classified data must be tagged in the data catalog
- Cloud storage buckets/containers must have classification tags
- API responses containing classified data must include classification headers

## Handling Requirements

### Access Controls

| Classification | Authentication | Authorization | Review Frequency |
|---------------|---------------|---------------|-----------------|
| Restricted | MFA required | Named individuals, need-to-know, manager + data owner approval | Quarterly |
| Confidential | MFA required | Role-based, manager approval | Semi-annual |
| Internal | Standard auth | Role-based, automatic for employees | Annual |
| Public | None required | Open access | N/A |

### Encryption Requirements

| Classification | At Rest | In Transit | Key Management |
|---------------|---------|------------|----------------|
| Restricted | AES-256, customer-managed keys | TLS 1.3 preferred, 1.2 minimum | HSM-backed, dual custody |
| Confidential | AES-256, provider or customer keys | TLS 1.2+ | Key vault with access logging |
| Internal | Platform default encryption | TLS 1.2+ | Platform-managed acceptable |
| Public | Optional | TLS recommended | N/A |

### Storage and Transmission

| Classification | Cloud Storage | Email | Removable Media | Printing |
|---------------|--------------|-------|-----------------|----------|
| Restricted | Approved, encrypted buckets only | Encrypted (S/MIME or portal) | Prohibited unless encrypted + approved | Controlled, secure printing only |
| Confidential | Approved cloud with encryption | Encrypted preferred | Encrypted, manager approval | Authorized printers only |
| Internal | Approved cloud services | Standard corporate email | Permitted with encryption | Standard printers |
| Public | Any approved platform | Standard email | Permitted | Unrestricted |

## Retention and Destruction

### Retention Periods

| Classification | Default Retention | Regulatory Override | Legal Hold |
|---------------|-------------------|--------------------:|-----------|
| Restricted | 3 years post-use | Per applicable regulation (GDPR, HIPAA, PCI) | Supersedes default |
| Confidential | 5 years | Per applicable regulation | Supersedes default |
| Internal | 3 years | Per applicable regulation | Supersedes default |
| Public | Indefinite | N/A | Supersedes default |

### Destruction Standards

| Classification | Digital Destruction | Physical Destruction | Verification |
|---------------|--------------------|--------------------|-------------|
| Restricted | NIST 800-88 Purge (cryptographic erase or overwrite) | Cross-cut shred (DIN 66399 P-5+) | Certificate of destruction required |
| Confidential | NIST 800-88 Clear or Purge | Cross-cut shred (DIN 66399 P-4+) | Destruction log entry |
| Internal | Standard deletion + recycle bin purge | Standard shred | Log entry |
| Public | Standard deletion | Standard disposal | None |

## Classification Process

1. **Data owner identifies data** -- person or team creating/acquiring data
2. **Apply classification level** -- based on sensitivity criteria above
3. **Label appropriately** -- per labeling requirements
4. **Implement controls** -- per handling requirements for that level
5. **Review periodically** -- reclassify if sensitivity changes
6. **Destroy per policy** -- when retention period expires and no legal hold

## Roles and Responsibilities

| Role | Responsibilities |
|------|-----------------|
| Data Owner (business unit) | Classify data, approve access, review classifications |
| Data Custodian (IT/security) | Implement technical controls, manage encryption, enforce policies |
| Data User | Handle data per classification, report misclassification |
| Data Protection Officer | Oversee program, audit compliance, manage regulatory requirements |
| Security Team | Monitor DLP alerts, investigate violations, maintain tooling |

## Cross-References

- [DLP Implementation Checklist](../checklists/data-protection/dlp-implementation-checklist.md) -- deploying classification-aware DLP
- [Encryption Audit Checklist](../checklists/data-protection/encryption-audit-checklist.md) -- verifying encryption controls
- [Data Retention Checklist](../checklists/data-protection/data-retention-checklist.md) -- retention compliance
- [Privacy Impact Checklist](../checklists/data-protection/privacy-impact-checklist.md) -- DPIA for classified data
