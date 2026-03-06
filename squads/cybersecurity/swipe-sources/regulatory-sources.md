# Regulatory and Compliance Sources

## Purpose

This resource catalogs the key regulatory frameworks, compliance standards, and authoritative sources that govern cybersecurity requirements across industries. Security teams must understand which regulations apply to their organization, where to find authoritative guidance, and how to track changes. This guide provides that foundation with practical notes on implementation and audit expectations.

## Major Regulatory Frameworks

### GDPR (General Data Protection Regulation)
- **Jurisdiction**: European Union / European Economic Area, applies to any organization processing EU resident data
- **Effective**: May 25, 2018
- **Authority**: European Data Protection Board (EDPB), national supervisory authorities
- **Key Security Requirements**:
  - Article 25: Data protection by design and by default
  - Article 32: Appropriate technical and organizational security measures (encryption, pseudonymization, resilience, recoverability, regular testing)
  - Article 33: Breach notification to supervisory authority within 72 hours
  - Article 34: Notification to affected individuals without undue delay for high-risk breaches
  - Article 35: Data Protection Impact Assessments (DPIA) for high-risk processing
- **Penalties**: Up to 4% of annual global turnover or 20 million EUR, whichever is higher
- **Official Source**: https://eur-lex.europa.eu/eli/reg/2016/679/oj
- **Practical Guidance**: EDPB guidelines at https://edpb.europa.eu/our-work-tools/our-documents_en

### HIPAA (Health Insurance Portability and Accountability Act)
- **Jurisdiction**: United States — covered entities and business associates handling Protected Health Information (PHI)
- **Key Rules**:
  - **Security Rule** (45 CFR Part 164 Subpart C): Administrative, physical, and technical safeguards for ePHI
  - **Privacy Rule** (45 CFR Part 164 Subpart E): Use and disclosure limitations
  - **Breach Notification Rule** (45 CFR Part 164 Subpart D): Notification within 60 days for breaches affecting 500+ individuals
- **Penalties**: $100-$50,000 per violation, up to $1.5M per violation category per year; criminal penalties possible
- **Official Source**: https://www.hhs.gov/hipaa/
- **Implementation Guidance**: NIST SP 800-66 (mapping HIPAA to NIST controls)

### PCI-DSS (Payment Card Industry Data Security Standard)
- **Version**: v4.0.1 (current)
- **Scope**: Any entity that stores, processes, or transmits cardholder data
- **Key Requirements** (12 requirement categories):
  1. Network security controls
  2. Secure configurations
  3. Protect stored account data
  4. Encrypt transmission over open networks
  5. Protect against malicious software
  6. Develop secure systems and software
  7. Restrict access by business need-to-know
  8. Identify users and authenticate access
  9. Restrict physical access
  10. Log and monitor all access
  11. Test security regularly
  12. Maintain an information security policy
- **Validation**: Self-Assessment Questionnaire (SAQ) or on-site assessment by QSA depending on merchant/service provider level
- **Official Source**: https://www.pcisecuritystandards.org/
- **Key Change in v4.0**: Many requirements moved from prescriptive to objective-based, with a "customized approach" option

### SOX (Sarbanes-Oxley Act)
- **Jurisdiction**: United States — publicly traded companies
- **Security Relevance**: Section 404 requires internal controls over financial reporting, which includes IT general controls (access management, change management, operations)
- **Key IT Controls**: Access to financial systems, segregation of duties, change management for financial applications, backup and recovery of financial data
- **Official Source**: https://www.sec.gov/
- **Framework Alignment**: Typically mapped to COSO and COBIT frameworks

### NIS2 (Network and Information Security Directive 2)
- **Jurisdiction**: European Union
- **Effective**: October 2024 (member state transposition deadline)
- **Scope**: Essential and important entities across 18 sectors
- **Key Requirements**: Risk management measures, incident reporting (24-hour early warning, 72-hour notification, one-month report), supply chain security, encryption, access control, business continuity
- **Penalties**: Up to 10 million EUR or 2% of global turnover for essential entities
- **Official Source**: https://eur-lex.europa.eu/eli/dir/2022/2555

## Security Frameworks and Standards

### NIST Cybersecurity Framework (CSF) 2.0
- **URL**: https://www.nist.gov/cyberframework
- **Version**: 2.0 (February 2024)
- **Structure**: Six functions — Govern, Identify, Protect, Detect, Respond, Recover
- **Use Case**: Voluntary framework widely adopted as baseline for security programs, often required by contract or regulation by reference
- **Key Change in 2.0**: Added "Govern" function, expanded supply chain risk management, improved guidance for small/medium organizations

### ISO/IEC 27001:2022
- **URL**: https://www.iso.org/standard/27001
- **Structure**: Information security management system (ISMS) requirements with Annex A controls
- **Use Case**: Certifiable standard, often required by enterprise customers and partners
- **Certification**: Requires accredited third-party audit
- **Companion Standards**: ISO 27002 (control guidance), ISO 27005 (risk management), ISO 27017 (cloud), ISO 27018 (PII in cloud)

### CIS Controls v8
- **URL**: https://www.cisecurity.org/controls
- **Structure**: 18 prioritized security controls with Implementation Groups (IG1, IG2, IG3)
- **Use Case**: Practical, prioritized starting point for organizations building a security program. IG1 represents essential cyber hygiene.
- **Strength**: Prescriptive and actionable — tells you what to do, not just what to achieve

### NIST SP 800-53 Rev 5
- **URL**: https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final
- **Structure**: Comprehensive catalog of security and privacy controls organized into 20 families
- **Use Case**: Required for US federal systems (FISMA), widely referenced by private sector
- **Companion**: SP 800-53B (control baselines), SP 800-53A (assessment procedures)

## Industry-Specific Standards

| Industry | Standard/Regulation | Authority | Key Resource |
|----------|-------------------|-----------|-------------|
| Financial Services | FFIEC IT Examination Handbook | FFIEC | https://ithandbook.ffiec.gov/ |
| Financial Services | DORA (EU) | EU | Digital Operational Resilience Act |
| Healthcare | HITRUST CSF | HITRUST | https://hitrustalliance.net/ |
| Energy / Utilities | NERC CIP | NERC | https://www.nerc.com/pa/Stand/Pages/CIPStandards.aspx |
| Automotive | ISO/SAE 21434 | ISO/SAE | Cybersecurity engineering for road vehicles |
| Government (US) | FedRAMP | GSA | https://www.fedramp.gov/ |
| Government (US) | CMMC | DoD | https://dodcio.defense.gov/CMMC/ |
| Telecommunications | GSMA security guidelines | GSMA | https://www.gsma.com/security/ |

## Tracking Regulatory Changes

### Monitoring Strategy
1. **Subscribe to official update feeds**: Most regulatory bodies offer email alerts or RSS feeds
2. **Legal counsel briefings**: Monthly check-in with legal on upcoming regulatory changes
3. **Industry association membership**: ISACs and industry groups often provide regulatory impact analysis
4. **Commercial compliance platforms**: Tools like OneTrust, Compliance.ai, or RegScale provide automated tracking

### Change Impact Assessment Template
```
REGULATORY CHANGE NOTICE

Regulation: [Name and reference]
Change Type: [New requirement / Amendment / Interpretation / Enforcement action]
Effective Date: [Date]
Source: [URL to official publication]

SUMMARY OF CHANGE:
[What changed in plain language]

IMPACT ASSESSMENT:
- Current compliance status: [Compliant / Partially Compliant / Gap]
- Gap description: [Specific gaps created by the change]
- Affected systems/processes: [List]
- Remediation effort estimate: [Hours/cost]
- Remediation deadline: [Date, with buffer before enforcement]

ACTION ITEMS:
1. [Specific action with owner and deadline]
```

## Cross-References

- See `voice/tone-profiles/compliance-auditor.md` for audit communication tone
- See `voice/language-guides/security-policy-language.md` for writing policies that satisfy regulatory requirements
- See `voice/calibration/severity-calibration.md` for aligning severity to compliance impact
- See `swipe-sources/vulnerability-databases.md` for vulnerability sources referenced by regulatory frameworks
