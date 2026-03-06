# Comprehensive Security Testing Methodology

## Purpose

Define a standardized methodology for conducting security assessments across all engagement types: vulnerability assessments, penetration tests, web application tests, cloud security reviews, and red team operations. This methodology ensures consistent quality, thoroughness, and defensible results across all security testing activities.

## Scope

All security testing engagements conducted by internal teams or contracted to external parties. This methodology applies regardless of target technology or assessment scope.

---

## Engagement Types and Depth

| Type | Objective | Depth | Duration | Deliverable |
|------|-----------|-------|----------|-------------|
| Vulnerability Assessment | Identify known vulnerabilities | Automated scanning + manual validation | 1-3 days | Vulnerability report with prioritization |
| Penetration Test | Validate exploitability and chain attacks | Manual testing + exploitation | 1-3 weeks | Pentest report with attack narratives |
| Web Application Test | Deep application security assessment | OWASP methodology, manual + automated | 1-2 weeks | AppSec report with code-level findings |
| Cloud Security Review | Cloud configuration and architecture | CIS Benchmarks + cloud-specific testing | 1-2 weeks | Cloud security posture report |
| Red Team Engagement | Test organizational detection and response | Adversary emulation, stealth operations | 2-6 weeks | Red team report with detection analysis |
| Purple Team Exercise | Collaborative detection validation | Joint red/blue, technique-by-technique | 1-2 weeks | Detection gap analysis with remediation |

## Phase 1: Pre-Engagement

### 1.1 Scoping
- [ ] Define target systems, networks, and applications (see `tasks/intake/asset-scoping.md`)
- [ ] Determine testing type and depth
- [ ] Identify testing window and schedule constraints
- [ ] Define rules of engagement (see `templates/briefs/pentest-roe-template.md`)
- [ ] Identify out-of-scope systems and restrictions
- [ ] Confirm emergency contact procedures

### 1.2 Authorization
- [ ] Obtain written authorization from system owners
- [ ] Confirm scope with legal counsel
- [ ] Sign rules of engagement document
- [ ] Verify testing authorization covers cloud environments (cloud provider policies)
- [ ] Document authorization chain for legal defensibility

### 1.3 Environment Preparation
- [ ] Set up testing infrastructure (VPN, attack VM, tooling)
- [ ] Verify connectivity to target environment
- [ ] Configure logging of all testing activities
- [ ] Establish communication channel with client/system owner
- [ ] Confirm rollback procedures for any changes
- [ ] Verify backup status of critical targets

## Phase 2: Reconnaissance and Discovery

### 2.1 Passive Reconnaissance
Gather information without directly touching target systems:
- [ ] DNS enumeration (subdomains, mail servers, name servers)
- [ ] WHOIS and registration data
- [ ] Certificate transparency log analysis
- [ ] OSINT: search engines, social media, code repositories
- [ ] Shodan/Censys for exposed services
- [ ] Google dorking for sensitive files and directories
- [ ] LinkedIn for organizational structure and technology clues
- [ ] Breach databases for exposed credentials (ethical, authorized use only)

### 2.2 Active Discovery
Direct interaction with target systems:
- [ ] Network scanning: host discovery, port scanning, service detection
- [ ] Service version identification and fingerprinting
- [ ] Web application discovery: crawling, directory enumeration
- [ ] API endpoint enumeration
- [ ] SSL/TLS configuration assessment
- [ ] Technology stack identification (web frameworks, CMS, libraries)
- [ ] Default credential checking on discovered services

### 2.3 Attack Surface Documentation
- [ ] Map all discovered entry points (network services, web apps, APIs)
- [ ] Document technology stack per target
- [ ] Identify potential high-value targets
- [ ] Map trust relationships between systems
- [ ] Document findings in attack surface map

Reference: `tasks/discovery/attack-surface-mapping.md`

## Phase 3: Vulnerability Identification

### 3.1 Automated Scanning
- [ ] Network vulnerability scanning (Nessus, Qualys, OpenVAS)
- [ ] Web application scanning (Burp Suite, OWASP ZAP, Nuclei)
- [ ] SSL/TLS scanning (testssl.sh, sslyze)
- [ ] CMS-specific scanning (WPScan, Droopescan)
- [ ] Cloud configuration scanning (ScoutSuite, Prowler, CloudSploit)
- [ ] Infrastructure-as-code scanning (Checkov, tfsec)

### 3.2 Manual Vulnerability Analysis
Automated scanners miss logic flaws and chained attacks:
- [ ] Authentication mechanism analysis (brute force protections, MFA bypass)
- [ ] Authorization testing (IDOR, privilege escalation, role-based access)
- [ ] Input validation testing (injection: SQL, command, LDAP, XPath)
- [ ] Business logic testing (workflow bypass, race conditions)
- [ ] Session management analysis (fixation, prediction, expiration)
- [ ] Cryptographic implementation review (weak algorithms, key management)
- [ ] API-specific testing (rate limiting, mass assignment, BOLA)
- [ ] File upload and handling (unrestricted upload, path traversal)

### 3.3 OWASP Top 10 Coverage (Web Applications)
Ensure testing covers:
- [ ] A01: Broken Access Control
- [ ] A02: Cryptographic Failures
- [ ] A03: Injection
- [ ] A04: Insecure Design
- [ ] A05: Security Misconfiguration
- [ ] A06: Vulnerable and Outdated Components
- [ ] A07: Identification and Authentication Failures
- [ ] A08: Software and Data Integrity Failures
- [ ] A09: Security Logging and Monitoring Failures
- [ ] A10: Server-Side Request Forgery (SSRF)

## Phase 4: Exploitation and Validation

### 4.1 Safe Exploitation
For penetration tests and red team engagements:
- [ ] Validate vulnerabilities through controlled exploitation
- [ ] Document exploitation chain (attack narrative)
- [ ] Demonstrate impact without causing damage
- [ ] Capture evidence: screenshots, command output, data samples (redacted)
- [ ] Attempt privilege escalation where in scope
- [ ] Attempt lateral movement where in scope
- [ ] Test data exfiltration paths (without exfiltrating real sensitive data)

### 4.2 Exploitation Guidelines
- NEVER delete or modify production data
- NEVER cause denial of service to production systems
- Use non-destructive exploitation techniques
- Stop and report immediately if critical system instability is observed
- Sanitize any evidence containing real sensitive data
- Operate within agreed rules of engagement at all times

### 4.3 Post-Exploitation (If In Scope)
- [ ] Credential harvesting and reuse assessment
- [ ] Persistence mechanism testing
- [ ] Internal network pivoting
- [ ] Domain privilege escalation
- [ ] Data access assessment (what could an attacker reach?)
- [ ] Detection assessment (were testing activities detected?)

## Phase 5: Reporting

### 5.1 Report Structure

```
1. Executive Summary (1-2 pages)
   - Engagement overview
   - Critical risk summary
   - Key recommendations (top 3-5)

2. Scope and Methodology
   - Systems tested
   - Testing approach and tools
   - Dates and timeframes
   - Limitations and caveats

3. Findings Summary
   - Finding count by severity
   - Risk heat map
   - Comparison to previous assessment (if applicable)

4. Detailed Findings
   For each finding:
   - Title and severity (Critical/High/Medium/Low/Info)
   - CVSS score
   - Description
   - Evidence (screenshots, redacted output)
   - Impact assessment
   - Remediation recommendation (specific, actionable)
   - References (CVE, CWE, OWASP)

5. Attack Narratives (Pentest/Red Team)
   - Step-by-step attack chain descriptions
   - Visual attack path diagrams
   - Detection analysis (what was detected, what was missed)

6. Strategic Recommendations
   - Systemic issues and root causes
   - Program-level improvements
   - Prioritized remediation roadmap

7. Appendices
   - Complete vulnerability list
   - Tool configuration and command logs
   - Scan output summaries
```

### 5.2 Finding Severity Rating

| Severity | CVSS Range | Criteria |
|----------|-----------|----------|
| Critical | 9.0-10.0 | Immediate exploitation risk; unauthenticated RCE; full system compromise; sensitive data exposure at scale |
| High | 7.0-8.9 | Significant exploitation risk; authenticated RCE; privilege escalation; meaningful data exposure |
| Medium | 4.0-6.9 | Moderate risk; requires specific conditions; limited data exposure; defense-in-depth weakness |
| Low | 0.1-3.9 | Minor risk; informational; best practice deviation; limited real-world exploitability |
| Informational | N/A | Observation; no direct security impact; potential future risk; hardening recommendation |

## Phase 6: Remediation Support and Retest

### 6.1 Remediation Guidance
- [ ] Provide specific, implementable fix recommendations (not just "patch")
- [ ] Offer to answer questions from remediation teams
- [ ] Prioritize fixes by risk (not just severity -- consider exploitability and exposure)
- [ ] Suggest compensating controls for findings that cannot be immediately fixed

### 6.2 Retest
- [ ] Schedule retest after remediation window (typically 30-60 days)
- [ ] Verify critical and high findings are resolved
- [ ] Test that fixes do not introduce new vulnerabilities
- [ ] Update report with retest results
- [ ] Reference: `frameworks/retest-method.md`

## Cross-References

- `tasks/intake/asset-scoping.md` — Pre-engagement scoping
- `templates/briefs/pentest-roe-template.md` — Rules of engagement
- `templates/reports/executive-summary-template.md` — Report templates
- `frameworks/finding-structure-standard.md` — Finding documentation standard
- `frameworks/risk-scoring-model.md` — Risk scoring
- `frameworks/retest-method.md` — Retest methodology
- `checklists/pentest-execution-quality.md` — Quality assurance
