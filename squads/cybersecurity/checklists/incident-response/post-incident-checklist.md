# Post-Incident Review Checklist

## Purpose / When to Use

Execute this checklist within 5 business days of incident closure. The post-incident phase transforms an incident from a crisis into an organizational learning event. This is where detection gaps are identified, processes are improved, and the team levels up. Skipping or half-executing this phase guarantees you will fight the same battle again.

## Prerequisites

- [ ] Incident fully resolved: eradication verified, recovery complete, monitoring stable
- [ ] All incident responders and key stakeholders available for review meeting
- [ ] Incident ticket and war room logs preserved with full timeline
- [ ] Evidence and forensic artifacts archived per retention policy
- [ ] Blameless review culture established -- focus on process, not people

---

## Phase 1 -- Timeline Construction

- [ ] Build comprehensive incident timeline from first observable activity to closure:
  ```
  Format per entry:
  [YYYY-MM-DD HH:MM UTC] | Source | Event Description | Actor (attacker/defender)
  ```
- [ ] Include attacker actions:
  - Initial access (delivery, exploitation, credential use)
  - Execution and installation of tools/malware
  - Persistence establishment
  - Discovery and reconnaissance
  - Lateral movement
  - Privilege escalation
  - Collection and staging
  - Exfiltration or impact
- [ ] Include defender actions:
  - First detection event (automated or human)
  - Triage start and completion
  - Each containment action with timestamp
  - Eradication actions
  - Recovery milestones
  - Key decisions and who made them
- [ ] Calculate critical metrics:
  - **Dwell time**: time from initial compromise to detection
  - **Time to detect (TTD)**: time from detectable activity to actual detection
  - **Time to contain (TTC)**: time from detection to effective containment
  - **Time to eradicate (TTE)**: time from containment to complete eradication
  - **Time to recover (TTR)**: time from eradication to full service restoration
  - **Total incident duration**: initial compromise to closure
- [ ] Identify timeline gaps where visibility was limited and note the reason
- [ ] Produce visual timeline (Gantt chart or swimlane diagram) for executive briefing

## Phase 2 -- Lessons Learned Meeting

- [ ] Schedule 90-minute blameless review with all incident participants
- [ ] Structure discussion around five questions:
  1. **What happened?** -- Walk through the timeline; ensure shared understanding
  2. **What went well?** -- Identify effective responses, tools, and decisions to reinforce
  3. **What did not go well?** -- Identify failures, delays, confusion, and gaps without blame
  4. **What was lucky?** -- Identify outcomes that depended on chance rather than process
  5. **What will we do differently?** -- Concrete, actionable improvements with owners
- [ ] Document all discussion points with specific examples from the incident
- [ ] Capture action items with:
  - Description of improvement
  - Responsible owner
  - Target completion date
  - Priority (critical / high / medium)
  - Tracking mechanism (Jira ticket, project board)
- [ ] Record dissenting opinions -- if team members disagree on root cause or improvements, capture both perspectives

## Phase 3 -- Detection Gap Analysis

- [ ] Map the attack to MITRE ATT&CK techniques (use Navigator layer from threat intel phase)
- [ ] For each technique used by the attacker, assess detection coverage:
  | ATT&CK Technique | Detected? | Detection Source | Time to Detect | Gap? |
  |---|---|---|---|---|
  | T1566.001 Phishing | No | - | - | Yes - no attachment detonation |
  | T1059.001 PowerShell | Yes | EDR | 4 hours | Partial - logged but not alerted |
- [ ] Identify techniques with no detection coverage (complete blind spots)
- [ ] Identify techniques with detection but excessive time-to-alert
- [ ] Identify techniques where detection existed but alert was missed or deprioritized
- [ ] Prioritize detection improvements:
  - **Critical**: techniques used for initial access and persistence (prevent recurrence)
  - **High**: techniques used for lateral movement and privilege escalation
  - **Medium**: techniques used for discovery and collection
- [ ] Create detection engineering tickets for each identified gap
- [ ] Estimate detection development effort and assign to sprint/quarter

## Phase 4 -- Process Improvement Identification

- [ ] Evaluate incident response process effectiveness:
  - [ ] Was the incident response plan followed? If not, why?
  - [ ] Were escalation procedures adequate and timely?
  - [ ] Were communication channels effective (internal and external)?
  - [ ] Were roles and responsibilities clear during the response?
  - [ ] Were sufficient tools and access available to responders?
  - [ ] Were any decisions delayed by approval processes?
  - [ ] Was documentation kept current during the response?
- [ ] Evaluate technical capabilities:
  - [ ] Did logging provide sufficient visibility? Where were gaps?
  - [ ] Did EDR perform as expected? Any agent gaps or coverage failures?
  - [ ] Did network monitoring capture the necessary traffic?
  - [ ] Were forensic tools adequate for evidence collection?
  - [ ] Did containment tools work as expected?
- [ ] Evaluate organizational readiness:
  - [ ] Were playbooks available and useful for this incident type?
  - [ ] Was the team sufficiently trained for this scenario?
  - [ ] Were third-party resources (IR retainer, legal) engaged effectively?
  - [ ] Did business continuity plans function during service disruption?
- [ ] Categorize improvements:
  - **People**: training needs, staffing gaps, on-call coverage
  - **Process**: playbook updates, escalation changes, communication improvements
  - **Technology**: tool gaps, configuration changes, new capabilities needed

## Phase 5 -- Report Generation

- [ ] Produce technical incident report containing:
  - Executive summary (1 page, non-technical language)
  - Incident classification and severity justification
  - Complete timeline with evidence references
  - Root cause analysis
  - Impact assessment (systems, data, users, business operations)
  - Containment, eradication, and recovery actions taken
  - IOC summary (appendix)
  - MITRE ATT&CK mapping
  - Detection gap analysis summary
  - Recommended improvements with priority and ownership
- [ ] Produce executive summary for leadership:
  - What happened (one paragraph)
  - Business impact (quantified where possible: downtime hours, affected users, data at risk)
  - What we did about it
  - What we are doing to prevent recurrence
  - Resource requests (if any)
- [ ] Produce compliance-specific documentation if required:
  - Breach notification records (GDPR 72-hour, HIPAA, state laws)
  - PCI DSS incident documentation
  - Regulatory filing support documents
  - Cyber insurance claim documentation
- [ ] Archive all reports with incident case file
- [ ] Distribute reports per TLP marking and need-to-know

## Phase 6 -- Improvement Tracking and Closure

- [ ] Enter all action items into tracking system with assigned owners and deadlines
- [ ] Schedule 30-day check-in to verify critical action items are progressing
- [ ] Schedule 90-day check-in to verify all action items are complete
- [ ] Update incident response playbooks based on lessons learned
- [ ] Update detection rules and monitoring configurations
- [ ] Conduct targeted training or tabletop exercise based on incident scenario
- [ ] Update risk register to reflect new threat intelligence from incident
- [ ] Close incident ticket with final status and link to report
- [ ] Add anonymized case to internal knowledge base for future responder training

---

## Cross-References

- Initial triage: `checklists/incident-response/initial-triage-checklist.md`
- Recovery: `checklists/incident-response/recovery-checklist.md`
- Lessons learned (Carey framework): `checklists/carey/carey-lessons-learned.md`
- Detection engineering: `checklists/detection-engineering-quality.md`
- Tabletop exercises: `checklists/tabletop-exercise-quality.md`
- Threat intel integration: `checklists/malware/threat-intel-integration-checklist.md`
- NIST SP 800-61r2: Section 3.4 -- Post-Incident Activity
- SANS Incident Handler's Handbook: Lessons Learned Phase
