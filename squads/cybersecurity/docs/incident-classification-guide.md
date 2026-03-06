# Incident Classification and Severity Rating Guide

## Purpose

Provide a standardized taxonomy for classifying security incidents and rating their severity. Consistent classification ensures appropriate resource allocation, escalation, SLA compliance, regulatory notification decisions, and meaningful metrics. When everyone uses the same language, response is faster and communication is clearer.

## Scope

All cybersecurity events and incidents detected by the security operations center, reported by employees, or identified through any other channel.

---

## Event vs. Incident Definitions

| Term | Definition | Example |
|------|-----------|---------|
| **Event** | Any observable occurrence in a system or network | Login attempt, firewall rule match, AV scan completion |
| **Security Event** | An event with potential security implications | Failed login, IDS alert, unusual outbound traffic |
| **Security Incident** | A security event that violates security policy or indicates compromise | Confirmed malware execution, unauthorized data access, account compromise |

Not every security event is an incident. Triage determines whether an event warrants incident classification.

## Incident Categories

### Category Taxonomy

| Category | Code | Description | Examples |
|----------|------|-------------|---------|
| Malware | MAL | Malicious software execution or infection | Ransomware, trojan, worm, cryptominer, RAT |
| Phishing | PHI | Social engineering via email, SMS, or voice | Credential phishing, BEC, spear phishing, vishing |
| Unauthorized Access | UAC | Illegitimate access to systems or data | Compromised account, brute force success, privilege escalation |
| Data Breach | DBR | Confirmed unauthorized data exposure or exfiltration | Data theft, accidental exposure, insider data leak |
| Denial of Service | DOS | Availability disruption attack | DDoS, application-layer DoS, resource exhaustion |
| Insider Threat | INT | Malicious or negligent insider activity | Data theft by employee, policy violation, sabotage |
| Vulnerability Exploitation | VEX | Exploitation of known or zero-day vulnerability | Web app exploit, OS exploit, service exploitation |
| Supply Chain | SCC | Compromise via third-party vendor or software | Vendor breach, compromised update, library compromise |
| Physical Security | PHY | Physical security breach with cyber impact | Unauthorized facility access, stolen device, USB drop |
| Policy Violation | POL | Security policy violation without malicious intent | Shadow IT, unapproved cloud service, data mishandling |

### Sub-Categories
Each category can be further refined. For example:
- MAL-RANSOM: Ransomware
- MAL-CRYPT: Cryptominer
- PHI-BEC: Business Email Compromise
- PHI-CRED: Credential Harvesting
- UAC-BRUTE: Brute Force
- UAC-PRIV: Privilege Escalation

## Severity Rating Framework

### Severity Levels

| Severity | Level | Description | Response SLA | Escalation |
|----------|-------|-------------|-------------|------------|
| **SEV-1: Critical** | 1 | Active, widespread compromise threatening core business operations or involving large-scale data breach | Immediate (15 min) | CISO, CTO, Legal, Executive Leadership |
| **SEV-2: High** | 2 | Confirmed compromise of systems or data with significant but contained impact | 1 hour | Security Manager, IT Director, affected BU |
| **SEV-3: Medium** | 3 | Confirmed security incident with limited scope and controlled impact | 4 hours | Security Lead, System Owners |
| **SEV-4: Low** | 4 | Minor security event or policy violation with minimal impact | 24 hours | Analyst handles, manager informed |
| **SEV-5: Informational** | 5 | Suspicious activity that warrants documentation but no immediate response | 72 hours | Document and monitor |

### Severity Determination Matrix

Assess each factor and use the highest resulting severity:

**Impact Factors:**

| Factor | SEV-1 | SEV-2 | SEV-3 | SEV-4 |
|--------|-------|-------|-------|-------|
| Data exposure | Regulated data (PII/PHI/PCI) at scale; trade secrets | Regulated data, limited scope; internal confidential | Internal data, limited scope | Public data only |
| System impact | Core business systems down; multiple critical systems | Single critical system or multiple non-critical | Non-critical system; limited functionality loss | Minimal operational impact |
| User impact | All users or customers affected | Department or significant user group | Small team or few users | Individual user |
| Financial impact | > $1M estimated or material (SEC) | $100K - $1M | $10K - $100K | < $10K |
| Regulatory | Mandatory breach notification triggered | Potential notification; investigation needed | Internal reporting only | No regulatory impact |
| Reputational | National media likely; customer trust at risk | Industry or local media possible | Internal awareness | Negligible |

**Threat Factors:**

| Factor | Increases Severity | Decreases Severity |
|--------|-------------------|-------------------|
| Active adversary | Ongoing attack with attacker still present: +1 SEV | Attack concluded, no active threat |
| Lateral movement | Evidence of spread to additional systems: +1 SEV | Contained to single system |
| Persistence | Attacker has established persistence: +1 SEV | No persistence mechanisms found |
| Data exfiltration | Evidence of data leaving the network: +1 SEV | No exfiltration evidence |
| Known threat actor | APT or sophisticated criminal group: +1 SEV | Opportunistic/automated attack |

## Classification Workflow

### Step-by-Step Classification Process

```
1. DETECT: Security event identified
   |
2. TRIAGE: Is this a security incident? (Yes/No)
   |-- No: Close as false positive or non-security event
   |-- Yes: Continue
   |
3. CATEGORIZE: Assign incident category (MAL, PHI, UAC, etc.)
   |
4. ASSESS SEVERITY: Evaluate impact and threat factors
   |-- SEV-1/2: Immediate escalation per SLA
   |-- SEV-3/4/5: Standard handling per SLA
   |
5. DOCUMENT: Record classification in incident ticket
   |
6. REASSESS: Update classification as new information emerges
```

### Classification Changes
Severity can change as investigation progresses:
- **Upgrade**: New evidence reveals greater impact (e.g., single host compromise found to be lateral movement across domain)
- **Downgrade**: Investigation determines scope is smaller than initially assessed (e.g., suspected data breach found to be authorized access)
- All changes must be documented with rationale and timestamp
- Re-escalation required if severity increases

## Escalation Matrix

### SEV-1: Critical

| Timing | Action | Responsible |
|--------|--------|-------------|
| 0-15 min | SOC lead notified; incident bridge opened | On-call analyst |
| 15-30 min | CISO notified; IR team activated | SOC lead |
| 30-60 min | Legal counsel engaged; executive briefing | CISO |
| 1-4 hours | Board notification if material | CISO + General Counsel |
| 4-24 hours | Regulatory notification assessment | Legal + Compliance |

### SEV-2: High

| Timing | Action | Responsible |
|--------|--------|-------------|
| 0-1 hour | Security manager notified; investigation initiated | Analyst + L2 |
| 1-4 hours | CISO briefed; affected business units notified | Security manager |
| 4-24 hours | Status update to leadership | Security manager |

### SEV-3 and Below
Handled within standard SOC operations with periodic status updates to security management.

## Regulatory Notification Triggers

### Automatic Notification Assessment Required
These classifications trigger mandatory regulatory notification assessment:
- [ ] DBR (Data Breach) of any severity involving regulated data
- [ ] SEV-1 incidents regardless of category
- [ ] Any incident involving PII of > 500 individuals
- [ ] Any incident involving financial data (PCI scope)
- [ ] Any incident involving PHI (HIPAA scope)
- [ ] Any incident that may be material (SEC rules)

Reference: `workflows/data-breach-response.md` for full notification workflow.

## Incident Metrics

Track classification data for reporting:
- Incidents by category (monthly trend)
- Incidents by severity (monthly trend)
- Mean time to classify (target: < 30 minutes)
- Classification accuracy (reviewed quarterly)
- Severity upgrade/downgrade frequency
- Regulatory notifications triggered

## Cross-References

- `workflows/incident-response-workflow.md` — IR process by severity
- `workflows/data-breach-response.md` — Breach-specific response
- `archive/regulatory-milestones/sec-cyber-rules-2023.md` — SEC materiality
- `archive/regulatory-milestones/gdpr-implementation-2018.md` — GDPR notification
- `data/registries/incident-registry.md` — Incident documentation
- `workflows/security-metrics-reporting.md` — Incident metrics reporting
