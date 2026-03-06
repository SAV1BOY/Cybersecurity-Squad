# Threat Model Canvas

## Purpose

Provide a visual, structured canvas for threat modeling that maps assets, threats, controls, data flows, and trust boundaries into a single coherent view. This canvas enables collaborative threat modeling sessions where security engineers, developers, and architects can identify and prioritize threats systematically.

## When to Use
- Security architecture reviews for new systems
- Major changes to existing systems
- Periodic review of critical applications
- Developer security training exercises
- Pre-deployment security gate

---

## Canvas Structure

The threat model canvas consists of six interconnected sections that together provide a complete picture of the system's security posture.

```
+------------------------------------------------------------------+
|                    THREAT MODEL CANVAS                             |
|  System: _______________  Date: ___________  Version: ___         |
+------------------------------------------------------------------+
|                                                                    |
|  1. SYSTEM OVERVIEW          |  2. ASSETS & DATA                  |
|  [Architecture diagram]      |  [What are we protecting?]         |
|  [Components & services]     |  [Data classification]             |
|  [Technology stack]          |  [Value & sensitivity]             |
|                              |                                     |
+------------------------------------------------------------------+
|                                                                    |
|  3. TRUST BOUNDARIES         |  4. THREAT ACTORS                  |
|  [Where trust changes]       |  [Who would attack?]               |
|  [Authentication points]     |  [Capability & motivation]         |
|  [Network segments]          |  [Relevant ATT&CK groups]         |
|                              |                                     |
+------------------------------------------------------------------+
|                                                                    |
|  5. THREATS & ATTACK          |  6. CONTROLS &                    |
|     SCENARIOS                 |     MITIGATIONS                   |
|  [STRIDE per element]         |  [Existing controls]              |
|  [Attack trees]               |  [Control gaps]                   |
|  [Kill chain paths]           |  [Recommended controls]           |
|                               |  [Residual risk]                  |
+------------------------------------------------------------------+
```

## Section 1: System Overview

### 1.1 Architecture Diagram
Draw or reference the system architecture showing:
- [ ] All system components (web servers, APIs, databases, caches, message queues)
- [ ] External dependencies (third-party APIs, SaaS services, CDNs)
- [ ] Infrastructure (cloud services, containers, serverless functions)
- [ ] User access points (web UI, mobile app, API clients, admin console)

### 1.2 Technology Stack
Document the full stack:
```
Frontend:     [Framework, language, hosting]
Backend:      [Framework, language, runtime]
Database:     [Type, version, hosting]
Cache:        [Type, version]
Message Queue:[Type, version]
CDN/WAF:      [Provider, configuration]
Auth:         [Provider, protocol (OIDC, SAML)]
Hosting:      [Cloud provider, services, region]
```

### 1.3 Data Flow Diagram (DFD)
Map how data moves through the system:
- Identify all data flows between components
- Label each flow with: protocol, authentication, encryption status
- Mark data transformation points
- Identify data storage locations

## Section 2: Assets and Data

### 2.1 Asset Inventory

| Asset | Type | Classification | Owner | Value |
|-------|------|---------------|-------|-------|
| Customer PII | Data | Confidential | Product team | High - regulatory |
| Authentication credentials | Data | Restricted | Security team | Critical |
| Application source code | IP | Confidential | Engineering | High - competitive |
| API keys and secrets | Credentials | Restricted | DevOps | Critical |
| System configuration | Config | Internal | Infrastructure | Medium |
| Audit logs | Data | Confidential | Security team | High - compliance |

### 2.2 Data Classification at Each Point
For each storage and transit point, document:
- What data is present (specific fields, not just "customer data")
- Classification level
- Encryption status (at rest and in transit)
- Retention period
- Access controls

## Section 3: Trust Boundaries

### 3.1 Identifying Trust Boundaries
Trust boundaries exist wherever the level of trust changes:
- [ ] Internet to DMZ (untrusted to semi-trusted)
- [ ] DMZ to internal network (semi-trusted to trusted)
- [ ] Application to database (application trust to data trust)
- [ ] User to admin (standard privileges to elevated)
- [ ] Organization to third-party (internal to external trust)
- [ ] Container to container (microservice boundaries)
- [ ] Cloud account to cloud account (account isolation)

### 3.2 Boundary Documentation

| Boundary | From (Trust Level) | To (Trust Level) | Authentication | Authorization | Encryption |
|----------|-------------------|-------------------|---------------|---------------|------------|
| Internet -> WAF | Untrusted | Semi-trusted | None | IP filtering | TLS 1.3 |
| WAF -> App Server | Semi-trusted | Trusted | mTLS | Allow-list | TLS 1.2+ |
| App -> Database | Trusted | Highly trusted | Credentials | Role-based | TLS + AES-256 |
| App -> External API | Trusted | External | API key | Scope-limited | TLS 1.2+ |

### 3.3 Critical Questions at Each Boundary
- What happens if this boundary is bypassed?
- Is authentication enforced programmatically (not just by network)?
- Can an attacker at this boundary access data they should not?
- Is there monitoring at this boundary?

## Section 4: Threat Actors

### 4.1 Relevant Threat Actors

| Actor Type | Motivation | Capability | Targeting | Relevance |
|-----------|-----------|-----------|-----------|-----------|
| External attacker (opportunistic) | Financial | Low-Medium | Automated scanning, known CVEs | High |
| External attacker (targeted) | Financial/Espionage | Medium-High | Targeted phishing, custom tooling | Medium |
| Nation-state APT | Espionage/Disruption | Very High | Zero-days, supply chain | [Assess] |
| Malicious insider | Financial/Revenge | Medium (legitimate access) | Data theft, sabotage | Medium |
| Negligent insider | None (accidental) | Low | Misconfig, phishing clicks | High |
| Compromised third party | N/A (supply chain) | Variable | Via trusted integration | Medium |

### 4.2 Attack Motivation Mapping
Map what each actor would target in this system:
- Opportunistic: exposed vulnerabilities, default credentials, public data
- Targeted: customer data, financial data, intellectual property
- Insider: accessible data, administrative functions, audit trail tampering

## Section 5: Threats and Attack Scenarios

### 5.1 STRIDE Per Element
For each component identified in the architecture, apply STRIDE:

| Component | S | T | R | I | D | E |
|-----------|---|---|---|---|---|---|
| Web Frontend | Session hijacking | DOM-based XSS | No client-side logging | Reflected XSS data leak | Client-side DoS | N/A (no privileges) |
| API Gateway | Token forgery | Parameter tampering | Insufficient logging | Error message leakage | Rate limit bypass | Auth bypass |
| Database | SQL injection auth bypass | Data modification | Audit log tampering | Data exfiltration | Resource exhaustion | Privilege escalation |
| Auth Service | Credential stuffing | MFA bypass | Login attempt hiding | Credential leakage | Account lockout abuse | Token privilege escalation |

### 5.2 Top Attack Scenarios
Develop 3-5 detailed attack scenarios:

```
Scenario 1: Credential Stuffing to Data Theft
  Entry: Automated credential stuffing against login API
  Escalation: Valid credential found, access customer account
  Impact: PII exposure, account takeover
  Controls Tested: Rate limiting, account lockout, MFA, anomaly detection

Scenario 2: SSRF to Cloud Metadata
  Entry: SSRF via user-supplied URL parameter
  Escalation: Access cloud metadata service, obtain IAM credentials
  Impact: Cloud account compromise, data exfiltration from S3
  Controls Tested: Input validation, IMDSv2, IAM least privilege
```

## Section 6: Controls and Mitigations

### 6.1 Control Mapping

| Threat | Existing Control | Effectiveness | Gap | Recommended |
|--------|-----------------|--------------|-----|-------------|
| Credential stuffing | Rate limiting (10/min) | Medium | No account lockout, no MFA | Implement MFA + account lockout |
| SQL injection | Parameterized queries | High | No WAF rules | Add WAF SQL injection rules |
| SSRF | None | None | Full gap | Input validation + IMDSv2 |
| XSS | CSP header | Medium | Incomplete CSP policy | Strict CSP + output encoding |
| Data exfiltration | No DLP | None | Full gap | Implement DLP on egress |

### 6.2 Residual Risk Assessment
After controls are applied, assess remaining risk:
- [ ] What attacks can still succeed despite controls?
- [ ] What is the likelihood and impact of residual risk?
- [ ] Is residual risk within organizational risk appetite?
- [ ] Document risk acceptance decisions

### 6.3 Action Items
Prioritized list of security improvements:
1. [Critical] Implement MFA for all user authentication
2. [Critical] Deploy IMDSv2 on all cloud instances
3. [High] Add WAF rules for OWASP Top 10
4. [High] Implement egress DLP controls
5. [Medium] Enhance CSP policy to strict mode

## Cross-References

- `tasks/discovery/threat-modeling.md` — Detailed threat modeling task
- `workflows/security-architecture-review.md` — Architecture review integration
- `lib/components/attack-tree-builder.md` — Attack tree construction
- `lib/components/risk-heat-map.md` — Risk visualization
- `frameworks/nist-csf.md` — CSF alignment
