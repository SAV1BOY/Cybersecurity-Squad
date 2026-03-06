# Severity Calibration Guide

## Purpose

This guide ensures consistent severity ratings across all assessment types — vulnerability scans, penetration tests, code reviews, architecture reviews, threat models, and audit findings. Inconsistent severity ratings erode trust, misallocate remediation resources, and create friction between security teams and stakeholders. Calibrated severity is the foundation of a credible security program.

## The Calibration Problem

Two analysts reviewing the same finding should arrive at the same severity rating. In practice, this fails because:

- Analysts anchor on CVSS base scores without considering environmental context
- Personal risk tolerance influences ratings (conservative vs. optimistic bias)
- Pressure from stakeholders inflates or deflates ratings
- Different assessment types use different rating scales

This guide establishes a single, context-aware severity framework the squad uses across all work products.

## Severity Rating Framework

### Critical

**Definition**: Immediate, exploitable threat to the confidentiality, integrity, or availability of high-value assets with minimal barriers to exploitation.

**All of the following must be true**:
- Exploitation is feasible by an external or low-privilege attacker
- The attack can be executed without significant prerequisites (no chained exploits, no social engineering required)
- The impact affects high-value assets: production systems, sensitive data stores, authentication infrastructure, safety-critical systems
- Active exploitation exists in the wild OR a reliable public exploit is available

**Examples**:
- Unauthenticated RCE on an internet-facing application server (CVE with public PoC)
- SQL injection on a production database containing PII with no WAF protection
- Default credentials on an internet-facing administrative interface
- Active compromise detected — threat actor present in the environment

**NOT Critical** (common miscalibrations):
- High CVSS score on an internal-only system with no sensitive data
- Theoretical vulnerability with no known exploit and high attack complexity
- Vulnerability in a decommissioned system scheduled for removal

### High

**Definition**: Significant exploitable weakness that could lead to substantial impact, with some barriers to exploitation or reduced blast radius.

**Characteristics (most should apply)**:
- Exploitation requires authentication, user interaction, or non-default configuration
- Impact is significant but constrained by compensating controls or network segmentation
- Affects production systems or sensitive data but with some mitigation in place
- No active exploitation, but exploit development is likely given the vulnerability class

**Examples**:
- Authenticated RCE in an internal application used by privileged users
- Stored XSS in a customer-facing application with session token access
- Privilege escalation from standard user to domain admin via misconfigured GPO
- Missing critical security patches on production servers (no known exploit yet, but actively targeted vulnerability class)

### Medium

**Definition**: Exploitable weakness with moderate impact or significant barriers to exploitation. Represents a defense-in-depth gap.

**Characteristics**:
- Exploitation requires chaining with another vulnerability or significant preconditions
- Impact is limited to non-critical data or non-production systems
- Compensating controls substantially reduce the effective risk
- Represents a deviation from security best practices rather than an active threat

**Examples**:
- Reflected XSS requiring user interaction with limited session access
- Information disclosure of internal hostnames, software versions, or stack traces
- Missing security headers on an internal application
- Weak encryption (e.g., TLS 1.0 still enabled alongside TLS 1.2/1.3)

### Low

**Definition**: Minor weakness with limited exploitability and minimal direct impact. Remediation improves security hygiene but is not risk-critical.

**Examples**:
- Verbose error messages disclosing framework version
- Directory listing enabled on a web server with no sensitive content
- Missing HTTP security headers on an informational static site
- Use of deprecated (but not broken) cryptographic algorithms in non-sensitive contexts

### Informational

**Definition**: Observation that does not represent a direct security vulnerability but may be relevant for hardening, compliance, or future security improvements.

**Examples**:
- Deviation from organizational naming conventions
- Opportunity to implement additional logging
- Configuration that is currently secure but may become vulnerable if other controls change

## Edge Cases and Calibration Decisions

### The "Critical CVSS, Low Context" Problem
**Scenario**: A vulnerability with CVSS 9.8 exists on a system that is air-gapped, contains no sensitive data, and is scheduled for decommission in 30 days.
**Calibration**: Rate as Medium or Low with explicit documentation of the contextual factors. Note: "CVSS base score 9.8 adjusted to Medium based on: air-gapped network (no remote exploitation path), no sensitive data, decommission scheduled [date]."

### The "Low CVSS, High Context" Problem
**Scenario**: A CVSS 3.1 information disclosure vulnerability reveals the internal API structure of a payment processing system, enabling targeted attacks.
**Calibration**: Rate as Medium or High with documentation. Note: "CVSS base score 3.1 adjusted to High based on: disclosed information directly enables exploitation of payment processing API, which handles [volume] transactions per day."

### Chain Vulnerabilities
**Scenario**: Three individually medium-severity findings can be chained to achieve domain admin.
**Calibration**: Rate the chain as a separate finding at the severity of the ultimate impact (Critical/High), while keeping individual findings at their standalone ratings. Document the chain relationship explicitly.

### Vulnerability in Compensating Control
**Scenario**: A medium-severity vulnerability exists in the WAF that protects against a critical vulnerability in the application.
**Calibration**: Elevate the WAF finding to High because its exploitation removes the compensating control for a critical risk. Document the dependency.

## Avoiding Calibration Bias

### Inflation Pressure
- Asset owners asking you to rate things higher to get remediation budget — resist. Severity reflects risk, not politics.
- Counter by helping frame the business case separately from the severity rating.

### Deflation Pressure
- Stakeholders pushing back on high/critical ratings because remediation is expensive — the cost of remediation does not change the severity of the risk.
- Document pushback and, if severity is overridden, require formal risk acceptance.

### Peer Calibration
- Conduct quarterly calibration exercises: present anonymized findings to the team and compare independent severity ratings.
- Track calibration drift over time. If one analyst consistently rates higher or lower than peers, investigate the root cause.

## Cross-References

- See `voice/language-guides/vulnerability-severity-language.md` for how to describe findings at each severity level
- See `voice/calibration/confidence-calibration.md` for expressing confidence in findings
- See `voice/calibration/urgency-calibration.md` for mapping severity to remediation timelines
- See `voice/tone-profiles/compliance-auditor.md` for audit-specific severity alignment
