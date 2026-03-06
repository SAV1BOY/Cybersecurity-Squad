# Insider Threat Investigation Workflow

## Purpose

Provide a structured, legally sound framework for investigating potential insider threats, from initial indicator detection through evidence collection, legal coordination, and resolution. Insider threats include malicious insiders (espionage, sabotage, fraud, data theft) and negligent insiders (accidental data exposure, policy violations). This workflow balances security objectives with employee privacy rights and legal requirements.

## Scope

All employees, contractors, and third-party personnel with authorized access to organizational systems and data. Covers both technical investigation procedures and coordination with legal, HR, and law enforcement.

---

## Phase 1: Indicator Detection and Triage (Days 1-3)

### 1.1 Behavioral Indicators
Potential insider threat indicators that may trigger investigation:
- Accessing data outside normal job responsibilities or working hours
- Bulk downloading or copying sensitive files
- Attempting to bypass security controls or escalate privileges
- Expressing intent to leave combined with unusual data access
- Financial distress, disgruntlement, or workplace conflicts (HR-reported)
- Communicating with known competitors about proprietary information
- Using unauthorized storage devices or cloud services
- Accessing systems after termination or role change notification

### 1.2 Technical Indicators
- DLP alerts for sensitive data exfiltration attempts
- Unusual USB device connections or large file transfers
- Email forwarding rules to personal accounts
- Printing volumes significantly above baseline
- VPN connections from unexpected locations
- Privileged access at unusual times
- Database queries returning abnormal result set sizes
- Use of steganography, encryption, or anonymization tools

### 1.3 Triage Assessment
Before escalating to full investigation:
- [ ] Verify the indicator is not a false positive or legitimate business activity
- [ ] Check with the employee's manager for authorized access patterns
- [ ] Review access logs for the preceding 30 days for pattern context
- [ ] Assess potential harm: data sensitivity, volume, exfiltration evidence
- [ ] Determine urgency: active exfiltration requires immediate action

### 1.4 Triage Decision Matrix

| Severity | Criteria | Action |
|----------|----------|--------|
| Critical | Active data exfiltration of classified/trade secret data | Immediate containment, legal/HR notification |
| High | Confirmed unauthorized access to sensitive data, evidence of staging | Formal investigation, legal engagement |
| Medium | Policy violations, suspicious patterns without confirmed harm | Preliminary investigation, enhanced monitoring |
| Low | Minor policy violations, likely negligent behavior | Manager counseling, security awareness referral |

## Phase 2: Legal and HR Coordination (Day 1-2, Concurrent)

### 2.1 Legal Engagement
- [ ] Notify legal counsel before expanding investigation
- [ ] Determine applicable privacy laws and employee monitoring regulations
- [ ] Confirm monitoring authorization under company policies and employee agreements
- [ ] Assess whether law enforcement engagement is required or advisable
- [ ] Establish attorney-client privilege over investigation communications

### 2.2 HR Engagement
- [ ] Notify HR of investigation (need-to-know basis only)
- [ ] Review employee's personnel file for context (PIP, resignation notice, etc.)
- [ ] Confirm employee signed acceptable use policy and monitoring consent
- [ ] Plan for potential interview, suspension, or termination scenarios
- [ ] Designate HR point of contact for investigation coordination

### 2.3 Investigation Team Formation
Limit knowledge to essential personnel:
- Investigation lead (security)
- Legal counsel
- HR representative
- Digital forensics analyst
- System/data owner (for access verification only, not full investigation details)

## Phase 3: Evidence Collection (Days 2-10)

### 3.1 Digital Evidence (Under Legal Guidance)
- [ ] Preserve email account contents (legal hold)
- [ ] Collect endpoint forensic image (if warranted, see `tasks/forensics/disk-image-analysis.md`)
- [ ] Capture browser history, download history, and application logs
- [ ] Collect DLP logs and alerts for the investigation period
- [ ] Retrieve badge access logs (physical access patterns)
- [ ] Collect print server logs
- [ ] Preserve cloud storage activity logs (OneDrive, Google Drive, Dropbox)
- [ ] Collect VPN and remote access logs
- [ ] Retrieve database query logs for accessed data stores

### 3.2 Network Evidence
- [ ] Review proxy logs for cloud storage uploads, webmail usage
- [ ] Analyze DNS queries for anomalous destinations
- [ ] Check for tunneling or covert channel indicators
- [ ] Review data transfer volumes to/from the employee's workstation
- [ ] Check for unauthorized network shares or services

### 3.3 Evidence Handling
- [ ] Maintain strict chain of custody documentation
- [ ] Hash all evidence at collection time (SHA-256)
- [ ] Store evidence in secured, access-controlled repository
- [ ] Log all evidence access with timestamps and personnel
- [ ] Prepare evidence in format admissible for legal proceedings

## Phase 4: Analysis and Assessment (Days 5-15)

### 4.1 Timeline Reconstruction
- [ ] Build comprehensive timeline of subject's digital activities
- [ ] Correlate physical access, network activity, and endpoint events
- [ ] Identify the scope of data accessed, copied, or exfiltrated
- [ ] Determine if other individuals are involved (collusion)
- [ ] Assess whether exfiltrated data has appeared externally

### 4.2 Impact Assessment
- [ ] Quantify the volume and sensitivity of compromised data
- [ ] Assess competitive harm if data reaches competitors
- [ ] Evaluate regulatory notification obligations if PII/PHI involved
- [ ] Estimate financial impact (IP value, remediation costs, legal exposure)
- [ ] Determine if ongoing risk exists (continued access, accomplices)

## Phase 5: Response and Resolution (Days 10-20)

### 5.1 Containment Actions
Based on investigation findings and legal guidance:
- [ ] Disable or restrict access (proportional to risk level)
- [ ] Revoke VPN, remote access, and privileged credentials
- [ ] Implement enhanced monitoring if access is maintained during investigation
- [ ] Block personal email and cloud storage from corporate network
- [ ] Place legal hold on all relevant data stores

### 5.2 Employee Interview (If Applicable)
Conducted by HR and legal, with security input on technical questions:
- [ ] Prepare interview plan with specific questions tied to evidence
- [ ] Document the interview thoroughly
- [ ] Provide opportunity for employee to explain legitimate reasons
- [ ] Do not reveal full scope of evidence collected during initial interview
- [ ] Follow legal counsel guidance on Miranda-equivalent obligations

### 5.3 Resolution Options

| Outcome | Criteria | Actions |
|---------|----------|---------|
| Cleared | Investigation finds legitimate explanation | Close case, document findings, return to normal monitoring |
| Policy Violation | Negligent behavior, no malicious intent | Formal warning, additional training, enhanced monitoring |
| Termination | Confirmed intentional policy violation | Terminate employment, preserve evidence, block all access |
| Criminal Referral | Evidence of theft, espionage, or fraud | Engage law enforcement, support prosecution |
| Civil Action | IP theft or contract violation | Support litigation with preserved evidence |

### 5.4 Post-Resolution
- [ ] Conduct immediate access revocation upon termination
- [ ] Monitor for continued attempts to access systems post-separation
- [ ] Notify relevant parties of data compromise if applicable
- [ ] Update detection rules based on techniques observed
- [ ] Document lessons learned for process improvement
- [ ] Brief leadership on findings and recommendations

## Cross-References

- `workflows/incident-response-workflow.md` — IR integration for insider-caused incidents
- `workflows/data-breach-response.md` — If insider threat results in data breach
- `tasks/forensics/disk-image-analysis.md` — Endpoint forensic procedures
- `tasks/forensics/memory-forensics.md` — Live memory analysis if warranted
- `docs/incident-classification-guide.md` — Severity classification
- `data/registries/incident-registry.md` — Incident documentation
