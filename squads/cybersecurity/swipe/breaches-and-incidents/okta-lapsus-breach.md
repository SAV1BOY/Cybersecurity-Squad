# Okta / LAPSUS$ Breach (2022) — Case Study

## Incident Summary
- **Date**: January 2022 (disclosed March 2022)
- **Attacker**: LAPSUS$ group (teenage threat actors)
- **Vector**: Compromised third-party support contractor (Sitel/Sykes)
- **Impact**: ~366 Okta customers potentially affected
- **Disclosure**: Screenshots leaked by LAPSUS$ on Telegram before Okta disclosed

## Attack Chain

### 1. Initial Access
- Targeted Sitel (third-party support contractor for Okta)
- Social engineering and credential purchase on dark web
- Gained RDP access to a Sitel support engineer's workstation

### 2. Privilege Abuse
- Sitel engineer had access to Okta's customer support tools (SuperUser)
- Could view customer tenants, reset MFA, generate temporary passwords
- Access was intended for legitimate support operations

### 3. Data Access
- Accessed internal Okta admin tools
- Viewed customer tenant configurations
- Potentially could initiate password resets for customer accounts
- Screenshots captured as evidence by attacker

### 4. Disclosure
- LAPSUS$ posted screenshots on Telegram (March 22, 2022)
- Okta initially downplayed — "the service has not been breached"
- Internal investigation had been ongoing since January
- Delayed customer notification created trust crisis

## Critical Failures

### Supply Chain Trust
- Third-party contractor with excessive access to customer data
- No just-in-time access provisioning for support tools
- Contractor security posture not adequately verified
- No real-time monitoring of support tool usage patterns

### Incident Response & Communication
- 2-month delay between detection and customer notification
- Initial public statement minimized impact
- Customers learned about breach from attacker, not from Okta
- Contradictory statements eroded trust

### Access Controls
- SuperUser tool access was persistent, not session-based
- No behavioral analytics on support engineer actions
- Lack of customer-side notification for admin actions taken
- Insufficient logging of contractor activities

## LAPSUS$ Tactics (Noteworthy)
- **SIM swapping** for MFA bypass
- **Social engineering** of help desks and IT support
- **Recruiting insiders** via Telegram for access
- **Public shaming** via Telegram to pressure victims
- **Young operators**: Several members were teenagers
- Demonstrated that sophisticated tools aren't needed — social engineering suffices

## Lessons for Defense

### Third-Party Risk Management
- Enforce zero standing privileges for contractors
- Just-in-time access with approval workflows
- Real-time monitoring of all support tool usage
- Regular security assessments of critical vendors
- Contractual requirements for security controls and incident notification

### Identity Security
- MFA resistant to SIM swapping (FIDO2/WebAuthn, not SMS)
- Behavioral analytics on privileged account usage
- Customer notification for any administrative action on their tenant
- Session-based access with mandatory re-authentication

### Incident Communication
- Pre-built communication templates for breach scenarios
- Legal-approved notification timelines (don't exceed 72h for material events)
- Transparency builds trust — minimize uncertainty, not impact
- Proactive customer notification before public disclosure

## MITRE ATT&CK Techniques
- T1078 — Valid Accounts (contractor credentials)
- T1199 — Trusted Relationship
- T1021.001 — Remote Desktop Protocol
- T1098 — Account Manipulation

## Cross-References
- `frameworks/cloud-identity-attack-defense.md`
- `archive/attack-evolution/evolution-of-identity-attacks.md`
- `checklists/cloud/third-party-risk-checklist.md`
