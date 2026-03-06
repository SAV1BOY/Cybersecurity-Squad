# New Security Analyst Onboarding Guide

## Purpose

Provide a structured onboarding program for new security analysts joining the team. This guide covers the first 90 days: tool access, training requirements, operational procedures, and performance expectations. A well-onboarded analyst reaches operational effectiveness in weeks, not months.

## Audience
New SOC analysts (L1/L2), threat analysts, and vulnerability management analysts.

---

## Day 1: Orientation and Access

### 1.1 Administrative Setup
- [ ] Obtain building access badge and secure area access
- [ ] Set up workstation in SOC or assigned workspace
- [ ] Configure MFA on all accounts (hardware token preferred)
- [ ] Review and sign acceptable use policy and NDA
- [ ] Complete mandatory security awareness training
- [ ] Meet direct manager for 1:1 introduction and expectations setting

### 1.2 System Access Requests
Submit access requests for (expect 1-3 day provisioning):

| System | Purpose | Access Level |
|--------|---------|-------------|
| SIEM (Splunk/Elastic/Sentinel) | Alert triage and investigation | Analyst (read + limited search) |
| EDR (CrowdStrike/SentinelOne/Defender) | Endpoint investigation | Analyst (read + isolate) |
| Ticketing System (ServiceNow/Jira) | Incident tracking | Analyst (create + update) |
| Threat Intelligence Platform | IOC lookup and enrichment | Read access |
| Vulnerability Scanner (Qualys/Nessus/Rapid7) | Vulnerability review | Read access |
| Wiki/Knowledge Base | SOC procedures and playbooks | Read + contribute |
| Communication Channels | Slack/Teams security channels | Member |
| VPN | Remote access | Standard analyst |
| Email | Team communication | Standard |

### 1.3 Team Introductions
- [ ] Meet SOC team lead and shift supervisors
- [ ] Meet fellow analysts on your shift rotation
- [ ] Meet incident response team lead
- [ ] Meet threat intelligence team point of contact
- [ ] Meet vulnerability management team point of contact
- [ ] Understand escalation chain and after-hours contacts

## Week 1: Foundation Training

### 2.1 Environment Orientation
- [ ] Review network architecture diagram (high-level)
- [ ] Understand critical systems and crown jewels
- [ ] Review asset inventory and classification (see `data/registries/asset-registry.md`)
- [ ] Understand organization's industry, regulatory requirements, and threat profile
- [ ] Review recent incident history (last 6 months from `data/registries/incident-registry.md`)

### 2.2 SIEM Training
- [ ] Complete SIEM platform basic training (vendor-provided or internal)
- [ ] Learn search query language (SPL, KQL, Lucene)
- [ ] Practice common searches: failed logins, malware alerts, network anomalies
- [ ] Understand alert pipeline: how alerts are generated, routed, and prioritized
- [ ] Review saved searches and dashboards used by the team
- [ ] Practice with training scenarios (non-production data)

### 2.3 Playbook Review
Read and understand all L1 analyst playbooks:
- [ ] Phishing email investigation playbook
- [ ] Malware detection alert triage playbook
- [ ] Suspicious authentication alert playbook
- [ ] DLP alert investigation playbook
- [ ] Network anomaly investigation playbook
- [ ] Escalation procedures and criteria

### 2.4 Key References
Required reading during first week:
- [ ] `docs/incident-classification-guide.md` — How to classify incidents
- [ ] `frameworks/vuln-triage-playbook.md` — Vulnerability prioritization
- [ ] `workflows/incident-response-workflow.md` — IR process overview
- [ ] `tasks/threat-intel/daily-threat-briefing.md` — Daily TI briefing format
- [ ] Team SOP (Standard Operating Procedures) document

## Weeks 2-4: Supervised Operations

### 3.1 Shadowing Phase (Week 2)
- [ ] Shadow experienced analyst for full shift rotations
- [ ] Observe alert triage decision-making process
- [ ] Watch investigation workflow from alert to closure
- [ ] Observe escalation to L2/L3 and how handoffs work
- [ ] Ask questions -- there are no stupid questions in a SOC

### 3.2 Guided Triage (Week 3)
- [ ] Begin triaging alerts with experienced analyst observing
- [ ] Handle low-severity alerts independently
- [ ] Review your triage decisions with supervisor daily
- [ ] Document questions and unclear procedures for discussion
- [ ] Complete at least 20 alert triage cycles with feedback

### 3.3 Independent Triage with Review (Week 4)
- [ ] Handle L1 alert triage independently
- [ ] Supervisor reviews closed tickets for quality (100% review initially)
- [ ] Escalate anything uncertain -- better to escalate unnecessarily than miss something
- [ ] Begin contributing to shift handoff documentation
- [ ] Complete first shift as primary analyst (with backup available)

## Month 2: Skill Development

### 4.1 Technical Skill Building
- [ ] Complete network fundamentals training (TCP/IP, DNS, HTTP, TLS)
- [ ] Learn packet analysis basics with Wireshark (reference: `tasks/forensics/network-forensics.md`)
- [ ] Practice malware triage (static analysis basics: strings, file properties)
- [ ] Learn basic log analysis for Windows Event Logs and Linux syslog
- [ ] Understand Active Directory basics: authentication, group policy, Kerberos

### 4.2 Certification Path (Choose Based on Role)
Begin studying for first certification:
- **CompTIA Security+**: Foundation certification (if not already held)
- **CompTIA CySA+**: SOC analyst certification
- **BTL1 (Blue Team Level 1)**: Practical blue team certification
- **SC-200 (Microsoft)**: If Microsoft Defender/Sentinel environment

### 4.3 Threat Intelligence Awareness
- [ ] Begin reading daily threat briefing (see `tasks/threat-intel/daily-threat-briefing.md`)
- [ ] Understand MITRE ATT&CK framework at overview level
- [ ] Learn to use threat intelligence platform for IOC lookup
- [ ] Understand TLP markings and information sharing classifications

## Month 3: Operational Integration

### 5.1 Full Operational Capability
- [ ] Handle L1 alert triage independently with spot-check review
- [ ] Participate in incident response as supporting analyst
- [ ] Contribute to detection rule tuning (propose false positive suppressions)
- [ ] Present one finding or lesson learned to the team
- [ ] Complete first on-call rotation (with experienced backup)

### 5.2 Performance Benchmarks (90-Day Targets)

| Metric | Target | Measured By |
|--------|--------|-------------|
| Alert triage per shift | Handle 80%+ of assigned alerts | Ticket metrics |
| False positive identification accuracy | > 90% | Supervisor review |
| Escalation appropriateness | > 95% correct escalation decisions | L2 feedback |
| Playbook adherence | 100% of triage follows documented playbook | Ticket review |
| Ticket documentation quality | Complete, clear, actionable | Supervisor review |
| On-time shift handoff | 100% | Shift log |

### 5.3 90-Day Review
- [ ] Self-assessment against onboarding milestones
- [ ] Manager review of progress and areas for improvement
- [ ] Set goals for months 4-6
- [ ] Identify specialization interest areas (threat hunting, forensics, detection engineering)
- [ ] Discuss training and certification support

## Ongoing Development

### Resources
- Weekly team knowledge sharing sessions
- Monthly tabletop exercises
- Quarterly red team/purple team exercises (observation for first year)
- Annual security conference attendance (budget permitting)
- Internal CTF events and training labs

### Career Progression Path
```
L1 Analyst (0-18 months) -> L2 Analyst (18-36 months) -> L3/Specialist:
  -> Incident Responder
  -> Threat Hunter
  -> Detection Engineer
  -> Forensic Analyst
  -> Threat Intelligence Analyst
  -> Security Engineer
```

## Cross-References

- `docs/onboarding-security-engineer.md` — Engineer onboarding path
- `docs/incident-classification-guide.md` — Incident classification
- `workflows/incident-response-workflow.md` — IR workflow
- `frameworks/detection-coverage-matrix.md` — Detection coverage
- `tasks/threat-intel/daily-threat-briefing.md` — Daily TI briefing
