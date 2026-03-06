# Initial Triage Checklist -- First 30 Minutes

## Purpose / When to Use

Execute this checklist the moment a potential security incident is reported or detected. The first 30 minutes determine whether an event escalates into a full incident, who needs to be involved, and whether critical evidence is preserved or lost. Speed and accuracy in triage directly correlate to containment effectiveness and total business impact.

## Prerequisites

- [ ] On-call responder has access to: SIEM, EDR console, ticketing system, communication platform
- [ ] Incident response contact list current (technical leads, management chain, legal, PR, third-party IR)
- [ ] Incident classification matrix available (severity definitions, escalation thresholds)
- [ ] Evidence preservation toolkit accessible (forensic imaging tools, secure storage)
- [ ] Pre-approved containment actions documented (what can be done without management approval)

---

## Phase 1 -- Detection Validation (Minutes 0-10)

- [ ] Open incident ticket immediately; record detection timestamp, source, and initial description
- [ ] Identify detection source category:
  - Automated: SIEM alert, EDR detection, IDS/IPS, DLP, email gateway
  - Human: user report, help desk ticket, SOC analyst observation
  - External: vendor notification, law enforcement, threat intel feed, media report
- [ ] Gather initial data from the detection source:
  ```
  Alert-based: alert name, severity, affected asset(s), triggered rule/signature
  User report: what was observed, when, on which system, any actions taken
  External: reporter identity, what they observed, how they obtained the information
  ```
- [ ] Verify the alert is not a known false positive (check tuning notes, recent changes, maintenance windows)
- [ ] Confirm affected assets exist and are in scope (not test systems, decommissioned, or out-of-scope third-party)
- [ ] Perform initial enrichment on key observables:
  - IP addresses: GeoIP, reputation, ASN ownership
  - Domains: WHOIS, passive DNS, reputation score
  - File hashes: VirusTotal, EDR prevalence in environment
  - User accounts: role, privilege level, recent activity
- [ ] Make preliminary determination: **True Positive**, **Likely True Positive**, **Likely False Positive**, or **Undetermined**
- [ ] If false positive confirmed: document rationale, update tuning rules, close ticket

## Phase 2 -- Severity Assessment (Minutes 10-15)

- [ ] Classify incident type:
  - Malware infection (ransomware, RAT, worm, cryptominer)
  - Account compromise (phishing, credential stuffing, brute force)
  - Data exfiltration / data breach
  - Insider threat
  - Denial of service
  - Web application attack
  - Supply chain compromise
  - Physical security breach
- [ ] Assess severity using organizational matrix:
  - **Critical (P1)**: Active data exfiltration, ransomware spreading, critical infrastructure compromised, confirmed nation-state activity
  - **High (P2)**: Confirmed compromise of sensitive system, credential theft with privileged access, active C2 communication
  - **Medium (P3)**: Isolated malware infection contained to single endpoint, phishing with credential capture but no confirmed misuse
  - **Low (P4)**: Adware, policy violation, reconnaissance activity with no confirmed compromise
- [ ] Determine blast radius: number of systems, users, data sets potentially affected
- [ ] Assess data sensitivity: is PII, PHI, financial data, IP, or classified information at risk?
- [ ] Check for regulatory notification requirements based on data types and jurisdictions
- [ ] Document severity justification in incident ticket

## Phase 3 -- Stakeholder Notification (Minutes 15-20)

- [ ] Notify based on severity level:
  - **P1 Critical**: CISO, CTO, Legal, PR, all IR team members, external IR retainer (if applicable)
  - **P2 High**: Security management, IR team lead, affected system owners
  - **P3 Medium**: IR team lead, affected system owner
  - **P4 Low**: SOC team lead
- [ ] Use pre-established communication channels (not the potentially compromised network):
  - Out-of-band communication: Signal, phone bridge, or pre-established war room
  - Never discuss incident details via corporate email if email compromise is possible
- [ ] Provide initial notification with:
  - Incident ID and classification
  - Affected systems and estimated scope
  - Current severity and justification
  - Immediate actions taken or recommended
  - Next scheduled update time
- [ ] For P1/P2: establish regular update cadence (every 30-60 minutes during active response)
- [ ] Confirm notification receipt from all critical stakeholders

## Phase 4 -- Containment Decision Tree (Minutes 20-25)

- [ ] Evaluate containment urgency based on active threat assessment:
  - Is the attacker currently active on the network? (Check C2 beaconing, active sessions)
  - Is data actively being exfiltrated?
  - Is malware actively spreading to additional systems?
  - Is destructive activity imminent (ransomware staging, wiper deployment)?
- [ ] Select containment strategy:
  - **Immediate full isolation**: active ransomware, worm propagation, destructive malware
  - **Selective isolation**: isolate affected endpoints while maintaining network services
  - **Monitor and contain**: attacker appears dormant, risk of tipping off outweighs immediate isolation
  - **Block and monitor**: block specific C2/IOCs at perimeter, monitor for attacker reaction
- [ ] Execute pre-approved containment actions (do not wait for additional approval):
  - EDR network isolation of confirmed compromised endpoints
  - Firewall blocks on confirmed malicious IPs/domains
  - Account disablement for confirmed compromised accounts
- [ ] For actions requiring approval: present options with risk assessment to incident commander
- [ ] Document containment actions with timestamps and responsible party
- [ ] Proceed to full containment checklist: `containment-checklist.md`

## Phase 5 -- Evidence Preservation (Minutes 25-30)

- [ ] Identify volatile evidence at risk of loss:
  - Running processes and network connections (lost on reboot)
  - Memory contents (lost on power off)
  - Temporary files and browser artifacts (lost on cleanup)
  - Log data approaching rotation/retention limits
- [ ] Initiate volatile data collection on key systems before containment alters state:
  ```bash
  # Capture order (most volatile first)
  # 1. Network connections
  netstat -anob > \\forensics\case_id\netstat_%COMPUTERNAME%.txt
  # 2. Running processes
  tasklist /v > \\forensics\case_id\tasklist_%COMPUTERNAME%.txt
  wmic process list full > \\forensics\case_id\processes_%COMPUTERNAME%.txt
  # 3. Memory acquisition (if time permits)
  winpmem_mini_x64.exe \\forensics\case_id\memory_%COMPUTERNAME%.raw
  ```
- [ ] Increase SIEM log retention for affected systems and related network segments
- [ ] Preserve relevant firewall, proxy, DNS, and authentication logs
- [ ] Begin chain-of-custody log for all evidence collected
- [ ] Identify systems that need full forensic imaging (schedule with forensics team)
- [ ] Document evidence collection gaps and risks

## Triage Complete -- Handoff

- [ ] Incident ticket updated with all triage findings, severity justification, and containment status
- [ ] Assign incident to appropriate response team based on incident type and severity
- [ ] Confirm next response phase: containment (`containment-checklist.md`), investigation, or monitoring
- [ ] Schedule next status update
- [ ] Transfer triage findings to assigned responders with context briefing

---

## Cross-References

- Containment actions: `checklists/incident-response/containment-checklist.md`
- Eradication: `checklists/incident-response/eradication-checklist.md`
- Evidence handling: `checklists/evidence-chain-quality.md`
- Malware response: `checklists/malware/malware-response-checklist.md`
- SOC alert triage: `checklists/santos/santos-alert-triage.md`
- NIST SP 800-61r2: Computer Security Incident Handling Guide
- SANS Incident Handler's Handbook
