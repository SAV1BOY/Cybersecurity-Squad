# Data Breach Response Workflow

## Purpose

Provide a structured, legally defensible workflow for responding to confirmed or suspected data breaches involving personally identifiable information (PII), protected health information (PHI), financial data, or other regulated data categories. This workflow integrates technical incident response with legal, communications, and regulatory obligations.

## Scope

Any incident where unauthorized access, acquisition, or disclosure of protected data is confirmed or reasonably suspected. Covers both internal breaches and third-party vendor breaches affecting organizational data.

## Prerequisites

- Incident response workflow active (see `workflows/incident-response-workflow.md`)
- Legal counsel (internal and external breach counsel) identified and on retainer
- Cyber insurance carrier and policy details documented
- Notification templates pre-drafted and reviewed by legal

---

## Phase 1: Detection and Initial Assessment (Hours 0-4)

### 1.1 Breach Indicators
A data breach investigation is triggered by any of the following:
- EDR/DLP alert indicating unauthorized data access or exfiltration
- Threat actor communication claiming data theft (ransomware double extortion)
- Third-party notification of organizational data found on dark web
- Anomalous database queries or bulk data export detected
- Employee report of unauthorized data access
- Vendor notification of breach affecting shared data

### 1.2 Immediate Actions
- [ ] Activate incident response team (see `workflows/incident-response-workflow.md`)
- [ ] Engage external breach counsel IMMEDIATELY (attorney-client privilege)
- [ ] Notify cyber insurance carrier (most policies require prompt notification)
- [ ] Preserve all relevant logs and evidence under legal hold
- [ ] Do NOT make public statements until legal counsel advises
- [ ] Begin breach assessment log (timestamped, factual entries only)

### 1.3 Initial Scoping Questions
Document answers to these questions as facts become available:
1. What data types are potentially affected? (PII, PHI, PCI, credentials, IP)
2. How many records/individuals are potentially affected?
3. What is the geographic scope of affected individuals?
4. How was the data accessed/exfiltrated? (attack vector)
5. Is the breach ongoing or contained?
6. Is there evidence of data being publicly disclosed or sold?

## Phase 2: Technical Investigation (Hours 4-72)

### 2.1 Evidence Collection
Conducted under direction of breach counsel to preserve privilege:
- [ ] Full forensic images of affected systems
- [ ] Network traffic captures during breach window
- [ ] Database audit logs showing query patterns
- [ ] DLP logs for data movement indicators
- [ ] Cloud access logs (CloudTrail, Azure Activity Log, GCP Audit Log)
- [ ] Email logs if phishing was the initial vector
- [ ] VPN and remote access logs

### 2.2 Data Impact Analysis
- [ ] Identify specific databases, file shares, or systems accessed
- [ ] Determine what data fields were exposed (name, SSN, DOB, financial, medical)
- [ ] Quantify number of unique individuals affected
- [ ] Determine geographic distribution of affected individuals
- [ ] Assess whether data was encrypted at rest (was encryption key also compromised?)
- [ ] Determine if accessed data was actually exfiltrated vs. merely accessed

### 2.3 Attribution and Threat Assessment
- [ ] Identify threat actor if possible (nation-state, criminal, insider)
- [ ] Assess likelihood of data misuse based on threat actor profile
- [ ] Check if data has appeared on dark web markets or paste sites
- [ ] Evaluate ongoing risk to affected individuals

## Phase 3: Legal and Regulatory Assessment (Hours 24-72)

### 3.1 Notification Obligation Analysis
Breach counsel determines obligations based on:

| Regulation | Trigger | Timeline | Authority |
|-----------|---------|----------|-----------|
| GDPR (EU) | Risk to rights/freedoms of data subjects | 72 hours to DPA | National DPA |
| HIPAA (US) | Unsecured PHI accessed/acquired | 60 days to HHS; without unreasonable delay to individuals | HHS OCR |
| State breach laws (US) | PII of state residents | Varies: 30-90 days | State AG |
| SEC rules | Material cybersecurity incident | 4 business days (8-K filing) | SEC |
| PCI DSS | Cardholder data compromise | Immediately to acquirer/card brands | Card brands |
| PIPEDA (Canada) | Real risk of significant harm | As soon as feasible | OPC |

### 3.2 Law Enforcement Engagement
- [ ] File report with FBI IC3 (cyber crimes)
- [ ] Engage CISA for technical assistance if applicable
- [ ] Coordinate with law enforcement on notification timing (may request delay)
- [ ] Document all law enforcement interactions

## Phase 4: Containment and Remediation (Concurrent with Phases 2-3)

### 4.1 Technical Containment
- [ ] Isolate compromised systems
- [ ] Revoke compromised credentials and API keys
- [ ] Block attacker infrastructure (IPs, domains, C2 channels)
- [ ] Patch exploited vulnerabilities
- [ ] Implement additional monitoring on affected data stores

### 4.2 Data-Specific Remediation
- [ ] If credentials exposed: force password resets for affected accounts
- [ ] If PCI data exposed: coordinate with payment processor for card reissue
- [ ] If API keys/secrets exposed: rotate all affected keys immediately
- [ ] If source code exposed: assess for embedded secrets and rotate

## Phase 5: Notification Execution (Per Legal Guidance)

### 5.1 Individual Notification
- [ ] Draft notification letter (reviewed by breach counsel)
- [ ] Include: what happened, what data was involved, what we are doing, what individuals can do
- [ ] Provide credit monitoring / identity protection services (typically 12-24 months)
- [ ] Establish dedicated call center for affected individuals
- [ ] Provide clear contact information for questions

### 5.2 Regulatory Notification
- [ ] Submit notifications to all required regulatory authorities
- [ ] Include: nature of breach, categories of data, approximate number affected, measures taken
- [ ] Document all submissions with timestamps and confirmation receipts

### 5.3 Public Communication
- [ ] Prepare holding statement for media inquiries
- [ ] Draft public notice (website, press release) per legal guidance
- [ ] Brief customer-facing teams (support, sales, account management)
- [ ] Prepare executive talking points for board, investors, partners
- [ ] Monitor social media for narrative and misinformation

## Phase 6: Post-Breach Actions (Weeks 2-12)

### 6.1 Root Cause Analysis
- [ ] Complete forensic investigation report
- [ ] Identify root cause and contributing factors
- [ ] Document attack timeline from initial access to data exfiltration
- [ ] Assess control failures and gaps

### 6.2 Remediation Program
- [ ] Prioritize and implement security improvements based on root cause
- [ ] Enhance detection capabilities for similar attacks
- [ ] Update incident response procedures based on lessons learned
- [ ] Conduct post-incident tabletop exercise

### 6.3 Ongoing Obligations
- [ ] Respond to regulatory inquiries and investigations
- [ ] Manage litigation hold and discovery obligations
- [ ] Track credit monitoring enrollment and utilization
- [ ] Prepare for potential regulatory hearings or consent orders
- [ ] Update breach response procedures based on lessons learned

## Cross-References

- `workflows/incident-response-workflow.md` — Technical IR procedures
- `workflows/ransomware-preparedness.md` — If ransomware with data exfiltration
- `archive/notable-breaches/equifax-2017.md` — Breach response lessons
- `archive/notable-breaches/capital-one-2019.md` — Cloud breach case study
- `archive/regulatory-milestones/gdpr-implementation-2018.md` — GDPR notification requirements
- `archive/regulatory-milestones/sec-cyber-rules-2023.md` — SEC disclosure requirements
- `docs/incident-classification-guide.md` — Severity classification

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
