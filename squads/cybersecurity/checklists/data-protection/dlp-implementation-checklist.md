# DLP Implementation Checklist

## Purpose

Checklist for deploying Data Loss Prevention across endpoint, network, and cloud channels. Covers data classification prerequisites, policy creation, tuning, and operational management.

## Prerequisites

### Data Classification Foundation

- [ ] Data classification framework defined and approved
- [ ] Classification levels established (public, internal, confidential, restricted)
- [ ] Data owners identified for critical data categories
- [ ] Data inventory completed for high-sensitivity data stores
- [ ] Data flow mapping completed (where does sensitive data move?)
- [ ] Regulatory requirements identified (PCI, HIPAA, GDPR, etc.)
- [ ] Data handling policies documented and communicated
- [ ] Executive sponsorship secured for DLP program

### Scope Definition

| Data Type | Regulatory Driver | Priority | Detection Method |
|-----------|------------------|----------|-----------------|
| Payment card data (PAN) | PCI DSS | Critical | Pattern matching (Luhn validation) |
| Social Security / national ID | HIPAA, privacy laws | Critical | Pattern matching + context |
| Protected health information | HIPAA | Critical | Keyword + pattern + context |
| Personal data (GDPR) | GDPR | High | Keyword + classifier |
| Financial records | SOX, internal | High | Document classification |
| Source code | Internal IP | High | File type + keyword |
| Customer data | Contract, privacy | High | Database fingerprint |
| Trade secrets | Internal IP | Critical | Exact match + classification |
| Credentials/secrets | Security | Critical | Pattern matching (API keys, passwords) |

## Endpoint DLP

### Endpoint DLP Deployment

- [ ] DLP agent deployed on all managed endpoints (workstations, laptops)
- [ ] Agent tamper protection enabled
- [ ] Agent performance impact assessed and acceptable
- [ ] Agent compatible with existing endpoint security tools (EDR, AV)
- [ ] Agent auto-update configured
- [ ] Agent health monitoring deployed
- [ ] Coverage tracked (deployed/total managed endpoints)

### Endpoint DLP Policies

| Channel | Action | Policy Mode | Verified |
|---------|--------|-------------|----------|
| USB/removable media | Block or encrypt | Enforce (after tuning) | [ ] |
| Clipboard (copy/paste) | Monitor | Monitor (audit) | [ ] |
| Print (physical) | Block for restricted data | Enforce | [ ] |
| Print to PDF/file | Monitor | Monitor | [ ] |
| Screen capture | Monitor for restricted | Monitor | [ ] |
| Application file access | Monitor | Monitor | [ ] |
| Upload to personal cloud | Block | Enforce | [ ] |
| Upload to unapproved SaaS | Block | Enforce | [ ] |

### Endpoint DLP Tuning

- [ ] USB policy allows approved encrypted devices (if needed)
- [ ] Exceptions process defined for legitimate use cases
- [ ] Print exceptions for specific printers/roles documented
- [ ] Cloud storage allowlist configured (approved services only)
- [ ] Application allowlist for sensitive data access defined
- [ ] User notification on policy trigger configured (educate, not just block)

## Network DLP

### Network DLP Deployment

- [ ] Network DLP sensors deployed at internet egress points
- [ ] Network DLP integrated with email gateway
- [ ] Network DLP integrated with web proxy
- [ ] Network DLP sensors can inspect encrypted traffic (TLS inspection)
- [ ] Network DLP high availability configured
- [ ] Network DLP fail-open/fail-closed behavior configured and documented

### Network DLP Policies

| Channel | Policy | Mode | Verified |
|---------|--------|------|----------|
| Email (external) | Detect PII, PCI, PHI in body/attachments | Block + notify | [ ] |
| Email (internal) | Monitor for classification violations | Monitor | [ ] |
| Web upload | Detect sensitive file uploads | Block for restricted | [ ] |
| FTP/SFTP | Detect sensitive file transfers | Block or alert | [ ] |
| Web forms | Detect PII in form submissions | Monitor + alert | [ ] |

### TLS Inspection Considerations

- [ ] TLS inspection deployed for DLP visibility into encrypted traffic
- [ ] TLS inspection certificate distributed to managed endpoints
- [ ] TLS inspection bypass list configured (banking, healthcare, personal)
- [ ] TLS inspection bypass list reviewed quarterly
- [ ] Privacy impact assessment completed for TLS inspection
- [ ] Employee notice provided about TLS inspection
- [ ] TLS inspection does not break certificate pinned applications
- [ ] TLS inspection performance impact assessed

## Cloud DLP

### Cloud Platform DLP

- [ ] Microsoft Purview DLP configured (if M365 environment)
- [ ] Google Cloud DLP configured (if Google Workspace)
- [ ] AWS Macie enabled for S3 scanning (if AWS)
- [ ] Azure Information Protection labels applied to sensitive documents
- [ ] Cloud DLP policies aligned with on-premises DLP policies
- [ ] Cloud DLP covers email, SharePoint/OneDrive, Teams, Drive

### CASB Integration

- [ ] Cloud Access Security Broker deployed
- [ ] CASB monitors sanctioned cloud application usage
- [ ] CASB detects data upload to unsanctioned cloud services (shadow IT)
- [ ] CASB inline mode for real-time blocking (vs. API mode for audit)
- [ ] CASB DLP policies match endpoint and network DLP
- [ ] CASB covers major SaaS (Salesforce, Box, Slack, etc.)

### Cloud Storage Scanning

- [ ] Existing cloud storage scanned for sensitive data (retrospective)
- [ ] New file uploads scanned in real-time
- [ ] Shared links reviewed for over-sharing (public links with sensitive data)
- [ ] External sharing policies enforced
- [ ] Classification labels propagated across cloud storage
- [ ] Remediation workflow for discovered sensitive data (quarantine, notify owner)

## Policy Tuning

### Tuning Process

| Phase | Duration | Activity | Target FP Rate |
|-------|----------|----------|----------------|
| Monitor only | 4-6 weeks | Deploy policies in audit mode, collect data | N/A |
| Baseline analysis | 2 weeks | Analyze alerts, identify false positives | N/A |
| Initial tuning | 2-4 weeks | Adjust patterns, add exceptions, refine context | <30% FP |
| Selective enforcement | 4 weeks | Enforce high-confidence policies, monitor others | <15% FP |
| Full enforcement | Ongoing | Enforce all policies, continuous tuning | <10% FP |

### Tuning Techniques

- [ ] Add contextual conditions (sender role, destination, file type)
- [ ] Use exact data matching (EDM) for structured data (DB fingerprinting)
- [ ] Implement document fingerprinting for form/template matching
- [ ] Configure minimum match count thresholds (e.g., 5+ SSNs, not 1)
- [ ] Implement proximity rules (keyword near pattern)
- [ ] Create targeted exceptions with approval and logging
- [ ] Build classification-based rules (not just pattern matching)
- [ ] Test new rules in monitor mode before enforcement

### False Positive Management

- [ ] FP reporting mechanism available to end users
- [ ] FP reports reviewed within 48 hours
- [ ] Confirmed FPs result in policy tuning
- [ ] FP rate tracked per policy (target: <10%)
- [ ] Policies with high FP rate prioritized for tuning
- [ ] Exception requests require manager approval
- [ ] Exceptions are time-bounded and reviewed quarterly

## Incident Management

### DLP Alert Workflow

```
1. DLP alert triggered
2. Auto-enrichment: user, data type, destination, volume
3. Triage by security analyst (true positive / false positive)
4. If TP: Assess severity and intent (accidental vs. malicious)
5. If accidental: Educate user, ensure data retrieved/deleted
6. If potentially malicious: Escalate to insider threat investigation
7. Document finding and resolution
8. Update policy if needed (tuning)
```

### Severity Classification

| Severity | Criteria | Response SLA |
|----------|---------|-------------|
| Critical | Restricted data exfiltrated externally | 1 hour |
| High | Confidential data sent to unauthorized party | 4 hours |
| Medium | Internal data sent externally (accidental) | 24 hours |
| Low | Policy violation, no data exposure confirmed | 72 hours |

## Metrics and Reporting

| Metric | Target | Frequency |
|--------|--------|-----------|
| DLP coverage (endpoints) | >95% | Monthly |
| DLP coverage (email) | 100% | Monthly |
| DLP coverage (cloud storage) | >90% | Monthly |
| False positive rate | <10% | Monthly |
| True positive response time | Per severity SLA | Monthly |
| Policy exception count | Decreasing trend | Monthly |
| Data exposure incidents prevented | Track | Quarterly |
| User awareness (self-reporting rate) | Increasing | Quarterly |

## Cross-References

- [Data Classification Framework](../../frameworks/data-classification-framework.md) -- classification foundation
- [Insider Threat Runbook](../../swipe/runbooks/insider-threat-runbook.md) -- DLP in insider threat
- [Encryption Audit Checklist](encryption-audit-checklist.md) -- encryption as complementary control
- [Privacy Impact Checklist](privacy-impact-checklist.md) -- DLP and privacy
