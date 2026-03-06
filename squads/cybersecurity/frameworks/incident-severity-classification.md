# Incident Severity Classification Framework

## Purpose

Standardize incident severity classification to drive consistent escalation, communication, and response timelines. Each severity level defines clear criteria, SLAs, roles, and communication requirements.

## Severity Definitions

### SEV-1: Critical

**Definition:** Active, widespread impact to critical business functions or confirmed data breach affecting sensitive data.

**Criteria (any one qualifies):**
- Active data exfiltration of restricted/confidential data
- Ransomware actively encrypting production systems
- Complete loss of critical business application (revenue-generating)
- Active exploitation by threat actor with persistent access
- Regulatory reporting obligation triggered (e.g., breach notification)
- Safety-critical system compromise (OT/ICS, medical, physical security)

**Examples:**
- Ransomware spreading across production environment
- Confirmed exfiltration of customer PII database
- Domain controller compromise with evidence of lateral movement
- Payment processing system unavailable due to security incident
- Supply chain compromise affecting production deployments

**SLAs:**

| Activity | Timeline |
|----------|----------|
| Initial acknowledgment | 15 minutes |
| Incident commander assigned | 30 minutes |
| War room established | 30 minutes |
| First status update to executives | 1 hour |
| Containment actions initiated | 1 hour |
| Status update cadence | Every 2 hours |
| Post-incident review | Within 5 business days |

### SEV-2: High

**Definition:** Significant security event with potential for major impact, limited active exploitation, or compromise of important (non-critical) systems.

**Criteria (any one qualifies):**
- Compromise of non-critical production system
- Successful phishing with credential theft (no confirmed lateral movement)
- Vulnerability actively exploited but contained to single system
- Insider threat with evidence of unauthorized data access
- Cloud account compromise (limited scope)
- Malware infection on multiple endpoints (contained to segment)

**Examples:**
- BEC attack resulting in unauthorized wire transfer attempt
- Single server compromised via unpatched vulnerability
- Privileged credential exposed in public repository
- Cloud storage bucket with internal data found publicly accessible
- Successful spear-phishing of executive with MFA bypass

**SLAs:**

| Activity | Timeline |
|----------|----------|
| Initial acknowledgment | 30 minutes |
| Incident lead assigned | 1 hour |
| Investigation initiated | 1 hour |
| First status update to management | 2 hours |
| Containment actions initiated | 4 hours |
| Status update cadence | Every 4 hours (business hours) |
| Post-incident review | Within 10 business days |

### SEV-3: Medium

**Definition:** Security event requiring investigation with limited immediate impact. Potential for escalation if not addressed.

**Criteria (any one qualifies):**
- Malware detected and auto-quarantined on single endpoint
- Suspicious authentication activity (no confirmed compromise)
- Vulnerability scan reveals critical vulnerability on exposed system
- Policy violation with security implications
- Failed intrusion attempt with reconnaissance indicators
- Third-party breach notification (potential data exposure)

**Examples:**
- Phishing email clicked but no credential submission confirmed
- Brute force attack against VPN with no successful authentication
- Unauthorized software installation on corporate endpoint
- Employee accessing files outside normal pattern (DLP alert)
- Vendor notifies of breach that may include shared data

**SLAs:**

| Activity | Timeline |
|----------|----------|
| Initial acknowledgment | 2 hours |
| Analyst assigned | 4 hours (business hours) |
| Investigation initiated | 8 hours (business hours) |
| First status update | 24 hours |
| Resolution target | 72 hours |
| Status update cadence | Daily |
| Post-incident review | If escalated or lessons identified |

### SEV-4: Low

**Definition:** Minor security event, informational alert, or policy violation with negligible immediate risk.

**Criteria:**
- Automated scan detects low-severity vulnerability
- Single failed login attempt from unusual location
- Minor policy compliance deviation
- Informational threat intelligence alert (no direct impact)
- Routine malware blocked at perimeter
- Security tool misconfiguration (no exposure)

**Examples:**
- Spam filter blocks phishing email before delivery
- Single unauthorized access attempt to non-sensitive resource
- Expired TLS certificate on internal-only service
- User reports suspicious email (confirmed benign)
- Security awareness test click tracked

**SLAs:**

| Activity | Timeline |
|----------|----------|
| Initial acknowledgment | Next business day |
| Triage and classification | 2 business days |
| Resolution target | 7 business days |
| Status update cadence | Weekly (if open) |
| Post-incident review | Not required |

## Escalation Criteria

### Upward Escalation Triggers

| From | To | Trigger |
|------|----|---------|
| SEV-4 | SEV-3 | Pattern of related events, scope expansion |
| SEV-3 | SEV-2 | Confirmed compromise, data exposure, spreading |
| SEV-2 | SEV-1 | Critical system impact, data breach confirmed, active adversary |

### Downward De-escalation Criteria

| From | To | Criteria |
|------|----|---------|
| SEV-1 | SEV-2 | Threat contained, no active exploitation, critical systems restored |
| SEV-2 | SEV-3 | Scope confirmed limited, no data exposure, remediation underway |
| SEV-3 | SEV-4 | Investigation complete, no evidence of compromise, routine cleanup |

## Communication Requirements

| Severity | Internal Notification | Executive Notification | External Notification | Legal Notification |
|----------|-----------------------|-----------------------|-----------------------|-------------------|
| SEV-1 | Immediate (all hands) | Within 1 hour (CISO, CTO, CEO) | As required by regulation/contract | Immediately |
| SEV-2 | Within 2 hours (security + IT) | Within 4 hours (CISO, CTO) | If contractually required | Within 24 hours |
| SEV-3 | Within 8 hours (security team) | Weekly summary | None typically | If data exposure suspected |
| SEV-4 | Daily triage review | Monthly summary | None | None |

### Communication Templates

**SEV-1 Initial Notification:**
```
SECURITY INCIDENT - SEV-1
Time Detected: [timestamp UTC]
Incident Commander: [name]
Summary: [1-2 sentence description]
Impact: [systems/data affected]
Current Actions: [containment steps underway]
Next Update: [timestamp]
War Room: [link/bridge number]
```

**SEV-2 Status Update:**
```
SECURITY INCIDENT UPDATE - SEV-2
Incident ID: [ID]
Time: [timestamp UTC]
Status: [Investigating/Containing/Remediating/Resolved]
Summary: [current understanding]
Actions Taken: [list]
Next Steps: [planned actions]
Next Update: [timestamp]
```

## Roles per Severity

| Role | SEV-1 | SEV-2 | SEV-3 | SEV-4 |
|------|-------|-------|-------|-------|
| Incident Commander | Required (senior) | Required | N/A | N/A |
| Lead Investigator | Required | Required | Assigned analyst | Assigned analyst |
| Communications Lead | Required | As needed | N/A | N/A |
| Legal Counsel | Required | On standby | N/A | N/A |
| Executive Sponsor | Required (CISO+) | CISO informed | N/A | N/A |
| External IR (retainer) | Engaged | On standby | N/A | N/A |

## Cross-References

- [Incident Response Workflow](../workflows/incident-response-workflow.md) -- response procedures
- [Incident Type Taxonomy](../lib/taxonomies/incident-type-taxonomy.md) -- classification types
- [BEC Runbook](../swipe/runbooks/business-email-compromise-runbook.md) -- BEC response
- [Ransomware Defense Framework](ransomware-defense-framework.md) -- ransomware-specific guidance
