# SEC Cybersecurity Disclosure Rules (2023)

## Overview

| Field | Details |
|-------|---------|
| Rule | SEC Final Rule: Cybersecurity Risk Management, Strategy, Governance, and Incident Disclosure |
| Adopted | July 26, 2023 |
| Effective | September 5, 2023 (governance); December 18, 2023 (incident reporting) |
| Applies To | All SEC-registered companies (public companies in the US) |
| Key Filing | Form 8-K (incident disclosure); Form 10-K (annual governance disclosure) |
| Enforcement | SEC Division of Enforcement |

---

## Core Requirements

### 1. Material Incident Disclosure (Form 8-K, Item 1.05)

**4 Business Day Notification Requirement:**
- Public companies must disclose material cybersecurity incidents within **4 business days** of determining the incident is material
- Clock starts at materiality determination, not incident discovery
- Disclosure must be filed on Form 8-K (or Form 6-K for foreign private issuers)

**Materiality Standard:**
An incident is material if there is a substantial likelihood that a reasonable investor would consider the information important in making an investment decision. Consider:
- Financial impact (direct costs, lost revenue, litigation exposure)
- Operational impact (business disruption, customer impact)
- Reputational impact (customer trust, market position)
- Legal and regulatory consequences
- Scope and nature of data compromised

**Required Disclosure Content:**
- [ ] Material aspects of the nature, scope, and timing of the incident
- [ ] Material impact or reasonably likely material impact on the company, including financial condition and results of operations
- Companies are NOT required to disclose specific technical details that would impede response or expose vulnerabilities

**Delayed Disclosure:**
- US Attorney General may grant delay if disclosure poses substantial risk to national security or public safety
- Delay request must come through law enforcement channel
- Maximum delay: generally 30 days, with possible extension to 60 days, and rare 120-day extension

### 2. Annual Governance Disclosure (Form 10-K, Regulation S-K Item 106)

**Risk Management and Strategy (Item 106(b)):**
Companies must describe:
- [ ] Processes for assessing, identifying, and managing material cybersecurity risks
- [ ] Whether and how cybersecurity risks are integrated into overall risk management
- [ ] Whether the company engages assessors, consultants, auditors, or other third parties
- [ ] Whether the company has processes to oversee and identify risks from third-party service providers
- [ ] Whether risks from cybersecurity threats have materially affected or are reasonably likely to affect business strategy, results, or financial condition

**Governance (Item 106(c)):**
Companies must describe:
- [ ] Board of directors' oversight of cybersecurity risks (which committee, how informed, frequency)
- [ ] Management's role in assessing and managing cybersecurity risks
- [ ] Relevant expertise of management responsible for cybersecurity
- [ ] How management is informed about and monitors prevention, detection, mitigation, and remediation of cybersecurity incidents
- [ ] Whether management reports cybersecurity information to the board and how frequently

## Implications for Security Teams

### Materiality Determination Process
Security teams must establish a clear process for materiality assessment:

**Step 1: Incident Detection and Initial Assessment**
- Security team detects and performs initial incident classification
- Reference: `docs/incident-classification-guide.md`

**Step 2: Materiality Assessment Team Activation**
Assemble cross-functional team including:
- CISO / security leadership
- General counsel / legal
- CFO / finance (quantitative impact assessment)
- Business unit leaders (operational impact assessment)
- Investor relations
- External counsel (securities law expertise)

**Step 3: Materiality Factors Assessment**

| Factor | Questions | Assessment |
|--------|-----------|------------|
| Financial | What are direct costs? Lost revenue? Litigation exposure? Insurance coverage? | $___ |
| Operational | What business processes are disrupted? For how long? Customer impact? | ___ |
| Data | What data was compromised? How many individuals? Regulatory notification? | ___ |
| Reputational | Will this affect customer trust? Market position? Brand value? | ___ |
| Legal | What regulatory fines are possible? Class action risk? | ___ |
| Strategic | Does this affect competitive position? Future business plans? | ___ |

**Step 4: Determination and Documentation**
- Document the materiality determination with rationale
- If material: initiate 4-business-day 8-K filing process
- If not material: document reasoning; reassess if new information emerges
- If uncertain: err on the side of disclosure; consult securities counsel

### Incident Response Integration
- [ ] Add materiality assessment step to incident response workflow
- [ ] Define clear escalation path from SOC to legal/finance for materiality evaluation
- [ ] Pre-identify the materiality assessment team members and alternates
- [ ] Practice materiality determination in tabletop exercises
- [ ] Ensure incident timeline documentation supports SEC disclosure requirements
- [ ] Coordinate with IR and legal to separate technical response from disclosure timing

### Annual Reporting Preparation
Security teams must prepare content for 10-K annual filing:
- [ ] Document cybersecurity risk management program description
- [ ] Describe risk assessment processes and methodologies used
- [ ] List third-party security assessments, audits, and engagements
- [ ] Document board and committee cybersecurity oversight activities
- [ ] Describe management cybersecurity governance structure
- [ ] Detail CISO qualifications and reporting relationships
- [ ] Summarize risk management integration with enterprise risk

### Board Communication
The SEC rules elevate cybersecurity to a board-level governance requirement:
- [ ] Establish regular board cybersecurity briefing cadence (at minimum quarterly)
- [ ] Create board-appropriate metrics and reporting (see `workflows/security-metrics-reporting.md`)
- [ ] Document all board cybersecurity discussions in meeting minutes
- [ ] Ensure at least one board member has cybersecurity expertise or literacy
- [ ] Prepare pre-approved 8-K disclosure templates for rapid filing

## Compliance Considerations

### What NOT to Disclose
The rules explicitly do not require:
- Specific technical information about security architecture or systems
- Vulnerability details that could be exploited
- Incident response playbooks or detection capabilities
- Information that would compromise ongoing investigation
- National security classified information

### Aggregation
- Multiple individually immaterial incidents may be material in aggregate
- Track and assess cumulative impact of cybersecurity incidents
- Quarterly review of aggregate incident impact

### Amendments
- If information not available at time of initial 8-K, may file amendment
- Must update if initial assessment of materiality changes
- Ongoing obligation to assess evolving impact

## Key Dates and Compliance Calendar
- **Each quarter**: Review aggregate incidents for materiality
- **Annually** (10-K filing): Update governance and risk management disclosures
- **Per incident**: 4 business days from materiality determination for 8-K
- **Ongoing**: Maintain documentation supporting all disclosures

## Cross-References

- `workflows/data-breach-response.md` — Breach response including SEC notification
- `workflows/incident-response-workflow.md` — IR integration with materiality assessment
- `docs/incident-classification-guide.md` — Incident severity and materiality
- `workflows/security-metrics-reporting.md` — Board reporting metrics
- `tasks/governance/compliance-gap-analysis.md` — SEC rule compliance assessment
- `archive/regulatory-milestones/gdpr-implementation-2018.md` — GDPR notification comparison
