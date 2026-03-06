# Technical Depth Calibration Guide

## Purpose

This guide defines how deep to go technically based on the audience and communication context. The same vulnerability might require a one-sentence board summary, a one-paragraph risk assessment, a one-page remediation guide, or a ten-page exploit walkthrough. Matching depth to audience is a core competency of effective security communication.

## Depth Levels

### Level 1: Executive Summary (Board/C-Suite)

**Target Audience**: Board of directors, CEO, CFO, non-technical executives
**Technical Knowledge Assumed**: None
**Depth**: Business impact and risk posture only

**Rules**:
- Zero technical jargon. If a term requires explanation, replace it with a plain language equivalent.
- No CVE numbers, CVSS scores, IP addresses, or tool names
- Every statement connects to business outcomes: revenue, reputation, compliance, operations
- Use analogies from physical security or business operations when helpful
- Maximum one page per topic

**Example — Same Finding at Level 1**:
"A flaw in our customer-facing website could allow an attacker to access our customer database without needing to log in. This database contains names, emails, and payment information for approximately 2.3 million customers. If exploited, we estimate $3-5M in breach response costs, potential regulatory fines, and customer notification expenses. Our security team has identified a fix that can be implemented within one week at minimal cost."

### Level 2: Management Briefing (CISO/IT Leadership/Security Management)

**Target Audience**: CISO, VP of Engineering, IT Directors, Security Managers
**Technical Knowledge Assumed**: General IT and security concepts, familiarity with common frameworks
**Depth**: Risk context with enough technical grounding to inform resource allocation decisions

**Rules**:
- Framework references acceptable (NIST, OWASP Top 10, MITRE ATT&CK at category level)
- CVSS score acceptable as a single data point, not the sole basis for urgency
- Vulnerability class names acceptable (SQL injection, RCE, privilege escalation)
- Include remediation cost, timeline, and resource requirements
- Include compensating controls and their effectiveness
- One to three pages per topic

**Example — Same Finding at Level 2**:
"SQL injection vulnerability (CVSS 9.8, Critical) in the customer portal's order lookup API. The flaw is unauthenticated and internet-facing, providing direct access to the customer database (2.3M records including PCI-scoped data). No WAF rule currently blocks this attack pattern. Remediation requires parameterized query implementation in the orders module — estimated 40 developer hours. Interim mitigation: WAF virtual patch deployable within 4 hours. Recommend immediate WAF mitigation with code fix in the next sprint."

### Level 3: Security Operations (SOC/Security Engineers)

**Target Audience**: SOC analysts, security engineers, detection teams, IT administrators
**Technical Knowledge Assumed**: Solid security fundamentals, familiarity with tools and attack techniques
**Depth**: Actionable technical detail sufficient to detect, respond, or remediate

**Rules**:
- Specific CVE identifiers, CWE classifications, ATT&CK technique IDs
- Detection signatures, SIEM queries, and IOCs
- Remediation steps with specific configuration changes or patches
- Affected versions, endpoints, and services
- Include verification steps to confirm remediation
- Three to five pages per topic

**Example — Same Finding at Level 3**:
"CVE-2024-XXXX: SQL injection in `/api/v2/orders?id=` parameter. CWE-89. Affected: CustomerPortal v3.2.1-3.4.0, running on app-web-01 through app-web-04 (10.1.2.10-13). The `id` parameter is concatenated directly into the SQL query without parameterization or input validation. Exploitation grants read access to the `customers` database (MySQL 8.0, db-prod-01). Detection: Monitor WAF logs for SQLi signatures on `/api/v2/orders`. SIEM query: `source=waf uri="/api/v2/orders" attack_type="sqli"`. Remediation: Apply patch CP-2024-0312 or implement parameterized queries per developer guide section 4.7. Verify fix by running `sqlmap -u 'https://portal.company.com/api/v2/orders?id=1' --batch` and confirming no injection points detected."

### Level 4: Exploit Development / Deep Technical (Red Team/Researchers)

**Target Audience**: Penetration testers, red team operators, vulnerability researchers
**Technical Knowledge Assumed**: Expert-level understanding of attack techniques, protocols, and system internals
**Depth**: Full technical detail including exploit mechanics, bypass techniques, and edge cases

**Rules**:
- Full exploit chains with step-by-step reproduction
- Memory layouts, protocol specifications, assembly/bytecode where relevant
- Tool configurations, custom scripts, and proof-of-concept code
- Bypass techniques for common defenses (WAF evasion, EDR bypass, ASLR/DEP circumvention)
- Attack tree diagrams showing alternative paths
- Detailed cleanup and operational security notes
- No length limit — completeness over brevity

**Example — Same Finding at Level 4**:
"The `id` parameter in `/api/v2/orders` is vulnerable to boolean-based blind, error-based, and UNION-based SQL injection. The application uses prepared statements globally but the orders module uses legacy string concatenation (confirmed via source review of `OrdersController.java:142`). The MySQL user `app_portal` has SELECT on all tables in the `customers` schema and FILE privilege (enabling `LOAD_FILE()` and `INTO OUTFILE`). WAF bypass achieved using inline comments: `/api/v2/orders?id=1'/*!UNION*//*!SELECT*/table_name,2,3/*!FROM*/information_schema.tables--`. Rate limiting applies after 100 requests/minute from a single IP; distribute across multiple source IPs or slow to 90 req/min. Full database extraction of 2.3M records takes approximately 45 minutes via UNION-based extraction with 50 concurrent threads. [Full sqlmap command, custom tamper script, and evidence artifacts follow...]"

## Depth Selection Decision Matrix

| Context | Level | Rationale |
|---------|-------|-----------|
| Board meeting presentation | 1 | Decision-makers need impact, not mechanics |
| CISO weekly briefing | 2 | Resource allocation decisions |
| Monthly vulnerability report to IT managers | 2-3 | Mix of prioritization and action items |
| SOC alert triage playbook | 3 | Operators need specific detection and response steps |
| Pentest report - executive summary section | 1-2 | Dual audience document |
| Pentest report - technical findings section | 3-4 | Reproducibility is the standard |
| Red team operation debrief | 4 | Full technical detail for defensive improvement |
| Security awareness training | 1 | Maximum accessibility |
| Incident post-mortem | 2-3 | Understanding what happened without losing non-technical stakeholders |

## Common Depth Miscalibrations

### Too Deep for the Audience
- Showing exploit code to the board — they cannot evaluate it and it wastes their time
- Including CVSS vector strings in executive summaries — meaningless to non-practitioners
- Referencing ATT&CK technique IDs in awareness training — intimidating and unnecessary

### Too Shallow for the Audience
- Telling a SOC analyst "there is a vulnerability in the web app" without IOCs or detection guidance
- Giving a developer "fix the SQL injection" without specifying which endpoint, parameter, or remediation pattern
- Providing a red team with a vulnerability name but no exploitation details or environmental context

### Mixed Depth (Most Common Error)
- Reports that oscillate between Level 1 and Level 4 within the same section
- Presentations that start accessible and suddenly dive into packet captures
- Emails that mix business impact with raw SIEM queries

**Solution**: Write for one audience per section. Use document structure (executive summary, technical details, appendix) to serve multiple audiences in a single document.

## Cross-References

- See `voice/tone-profiles/executive-advisory.md` for Level 1 tone and structure
- See `voice/tone-profiles/technical-operator.md` for Level 3-4 tone and structure
- See `voice/language-guides/risk-communication-language.md` for translating technical findings to business language
- See `voice/language-guides/pentest-report-language.md` for multi-audience report structure
