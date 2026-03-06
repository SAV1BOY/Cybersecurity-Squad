# Third-Party Risk Assessment Workflow

## Purpose

Establish a structured process for evaluating, onboarding, and continuously monitoring the security posture of third-party vendors, suppliers, and service providers. Supply chain compromises (SolarWinds, Kaseya, MOVEit) demonstrate that organizational security is only as strong as its weakest vendor.

## Scope

All third parties with access to organizational data, systems, networks, or physical facilities. Includes SaaS providers, managed service providers (MSPs), contractors, and API integrations.

---

## Phase 1: Vendor Classification and Tiering (Pre-Assessment)

### 1.1 Criticality Tiering
Classify vendors into risk tiers based on data access and business impact:

| Tier | Criteria | Assessment Depth | Review Frequency |
|------|----------|-----------------|------------------|
| Tier 1 - Critical | Access to sensitive data, network connectivity, business-critical service | Full assessment + pentest | Annual + continuous |
| Tier 2 - Significant | Limited sensitive data, cloud-only integration | Standard questionnaire + evidence review | Annual |
| Tier 3 - Standard | No sensitive data, replaceable service | Abbreviated questionnaire | Biennial |
| Tier 4 - Minimal | No data access, no integration | Self-attestation | On onboarding only |

### 1.2 Data Classification Mapping
- [ ] Identify what data the vendor will access, process, or store
- [ ] Map data types to regulatory requirements (PII, PHI, PCI, financial)
- [ ] Document data flow: ingress, processing, storage, egress, deletion
- [ ] Determine data residency requirements

## Phase 2: Security Questionnaire and Documentation Review

### 2.1 Questionnaire Distribution
Use standardized questionnaires based on industry frameworks:
- SIG (Standardized Information Gathering) questionnaire for Tier 1-2
- SIG Lite for Tier 3
- Custom abbreviated form for Tier 4

### 2.2 Key Assessment Domains
- [ ] **Governance**: Security program maturity, CISO reporting structure, board oversight
- [ ] **Access Control**: MFA enforcement, privilege management, access reviews
- [ ] **Data Protection**: Encryption at rest and in transit, key management, DLP
- [ ] **Incident Response**: IR plan, notification timelines, breach history
- [ ] **Business Continuity**: DR capabilities, RTO/RPO, geographic redundancy
- [ ] **Compliance**: SOC 2 Type II, ISO 27001, PCI DSS, HIPAA (as applicable)
- [ ] **Supply Chain**: Vendor's own third-party risk program (fourth-party risk)
- [ ] **Personnel Security**: Background checks, security training, offboarding

### 2.3 Evidence Collection
For Tier 1 and Tier 2 vendors, require:
- [ ] SOC 2 Type II report (current year, review for exceptions)
- [ ] Penetration test executive summary (within 12 months)
- [ ] Insurance certificate (cyber liability coverage)
- [ ] Business continuity / DR test results
- [ ] Security architecture diagram
- [ ] Data processing agreement (DPA) or equivalent

## Phase 3: Technical Assessment (Tier 1 Only)

### 3.1 External Attack Surface Review
- [ ] Passive reconnaissance of vendor's internet-facing infrastructure
- [ ] SSL/TLS configuration assessment
- [ ] DNS security (DNSSEC, SPF, DKIM, DMARC)
- [ ] Review SecurityScorecard, BitSight, or RiskRecon ratings
- [ ] Check for exposed credentials in breach databases

### 3.2 Integration Security Review
- [ ] API authentication and authorization mechanisms
- [ ] Data encryption in transit between organizations
- [ ] Network connectivity requirements (VPN, direct connect, internet)
- [ ] Service account privilege scoping
- [ ] Log availability for security monitoring

### 3.3 Penetration Testing
For Tier 1 vendors integrating directly into the network:
- [ ] Request right to conduct scoping-limited pentest of integration points
- [ ] Or require vendor to share recent pentest findings and remediation status
- [ ] Validate critical/high findings have been remediated

## Phase 4: Risk Scoring and Decision

### 4.1 Risk Calculation
Score each domain on a 1-5 scale and weight by criticality:

```
Vendor Risk Score = SUM(Domain Score x Weight) / Total Weight

Risk Rating:
  1.0 - 2.0: Low Risk      -> Approve
  2.1 - 3.0: Medium Risk   -> Approve with conditions
  3.1 - 4.0: High Risk     -> Approve with compensating controls + executive sign-off
  4.1 - 5.0: Critical Risk -> Reject or require remediation before onboarding
```

### 4.2 Compensating Controls
For vendors that cannot meet requirements:
- [ ] Network isolation (dedicated VLAN, firewall restrictions)
- [ ] Enhanced monitoring (dedicated SIEM alerts for vendor activity)
- [ ] Data minimization (reduce data shared to minimum necessary)
- [ ] Contractual protections (breach notification SLA, liability, audit rights)
- [ ] Escrow arrangements for critical vendor dependencies

## Phase 5: Contractual Requirements

### 5.1 Mandatory Security Clauses
- Right to audit (at least annually for Tier 1)
- Breach notification within 24-72 hours
- Data return/destruction upon contract termination
- Compliance with applicable regulations
- Security incident cooperation and evidence preservation
- Subcontractor/subprocessor approval requirements

## Phase 6: Continuous Monitoring (Post-Onboarding)

### 6.1 Automated Monitoring
- [ ] Subscribe to vendor's security rating via BitSight/SecurityScorecard
- [ ] Monitor for vendor mentions in threat intelligence feeds
- [ ] Track vendor's CVE exposure for products in use
- [ ] Alert on significant rating score drops (> 10 points)

### 6.2 Periodic Reassessment
- [ ] Annual questionnaire refresh for Tier 1-2
- [ ] Review updated SOC 2 reports and pentest results
- [ ] Validate that previously identified risks were remediated
- [ ] Re-tier vendor if scope of engagement changes

### 6.3 Incident Coordination
- [ ] Maintain vendor security contact list (updated quarterly)
- [ ] Define joint incident response procedures
- [ ] Test communication channels annually
- [ ] Include critical vendors in tabletop exercises

## Cross-References

- `tasks/governance/vendor-security-review.md` — Individual vendor review task
- `workflows/data-breach-response.md` — If vendor breach affects organization
- `archive/notable-breaches/kaseya-2021.md` — MSP supply chain attack
- `frameworks/nist-csf.md` — Supply chain risk management (GV.SC)
- `docs/tool-evaluation-criteria.md` — Tool vendor assessment criteria
