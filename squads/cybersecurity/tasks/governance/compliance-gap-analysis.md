# Compliance Gap Analysis and Remediation Planning

## Purpose

Systematically compare the organization's current security controls against applicable regulatory and framework requirements to identify gaps, prioritize remediation, and maintain audit readiness. This task transforms compliance from a periodic scramble into a continuous, managed process.

## Task Owner
Compliance analyst / GRC lead, with support from security engineers, IT operations, and legal.

## Frequency
Full gap analysis annually per framework; continuous tracking of remediation and control status.

---

## Phase 1: Framework and Regulation Identification (Week 1)

### 1.1 Applicable Frameworks Inventory
Determine which frameworks apply based on industry, geography, and contracts:

| Framework | Applicability Trigger | Status |
|-----------|----------------------|--------|
| NIST CSF 2.0 | Voluntary best practice / federal contracts | ___ |
| SOC 2 Type II | Customer contractual requirement | ___ |
| ISO 27001 | International customers, certification requirement | ___ |
| PCI DSS 4.0 | Processing, storing, or transmitting cardholder data | ___ |
| HIPAA | Processing protected health information | ___ |
| GDPR | Processing EU resident personal data | ___ |
| SOX (IT controls) | Publicly traded company (US) | ___ |
| CCPA/CPRA | California consumer personal information | ___ |
| DORA | Financial services operating in EU | ___ |
| CIS Controls v8 | Voluntary best practice / cyber insurance | ___ |
| NIST 800-171 | CUI handling for DoD contracts | ___ |

### 1.2 Control Mapping
- [ ] Map controls across frameworks to create unified control inventory
- [ ] Identify overlapping controls (implement once, satisfy many)
- [ ] Use common control framework (CCF) approach to reduce duplication
- [ ] Document control-to-framework mapping in spreadsheet or GRC tool

## Phase 2: Current State Assessment (Weeks 2-4)

### 2.1 Control Evidence Collection
For each control in the unified inventory:
- [ ] **Implemented**: Control exists and operates effectively (evidence available)
- [ ] **Partially Implemented**: Control exists but has gaps in scope or effectiveness
- [ ] **Planned**: Control is in roadmap but not yet implemented
- [ ] **Not Implemented**: No control exists
- [ ] **Not Applicable**: Control does not apply (document justification)

### 2.2 Evidence Types

| Evidence Type | Examples | Collection Method |
|---------------|---------|-------------------|
| Policy | Security policies, standards, procedures | Document review |
| Configuration | System configurations, hardening baselines | Automated scans, screenshots |
| Technical | Scan results, test reports, log samples | Tool exports |
| Process | Workflow documentation, approval records | Interviews, process review |
| Training | Completion records, training materials | LMS reports |
| Monitoring | Dashboard screenshots, alert configurations | SIEM/tool exports |

### 2.3 Control Testing
For implemented controls, verify operational effectiveness:
- [ ] Sample-based testing: select representative systems for control validation
- [ ] Automated testing where possible (configuration compliance scans)
- [ ] Interview control operators for process-based controls
- [ ] Review logs and reports for monitoring-based controls
- [ ] Document test results with evidence

## Phase 3: Gap Identification and Analysis (Week 5)

### 3.1 Gap Documentation
For each identified gap:
```
Gap ID: GAP-2026-001
Framework Control: NIST CSF PR.AC-07 / ISO 27001 A.9.2.3
Control Description: Privileged access management
Current State: Local admin passwords are not unique per endpoint
Gap Description: No LAPS or equivalent deployed; shared local admin password
Risk: Lateral movement via credential reuse (High)
Affected Systems: All Windows endpoints (~2000)
```

### 3.2 Gap Prioritization
Prioritize gaps using a risk-based approach:

| Priority | Criteria | Remediation Timeline |
|----------|----------|---------------------|
| P1 - Critical | Regulatory violation with active enforcement risk; exploitable gap | 30 days |
| P2 - High | Significant compliance gap with audit finding risk | 90 days |
| P3 - Medium | Partial implementation needing enhancement | 180 days |
| P4 - Low | Best practice gap, not regulatory requirement | Next annual cycle |

### 3.3 Cross-Framework Impact
For each gap, assess impact across all applicable frameworks:
- [ ] Does this gap create non-compliance in multiple frameworks?
- [ ] Is this gap likely to be identified in upcoming audits?
- [ ] Does remediation satisfy requirements across multiple frameworks?
- [ ] Prioritize gaps with highest cross-framework remediation value

## Phase 4: Remediation Planning (Week 6)

### 4.1 Remediation Roadmap
For each gap, create a remediation plan:
- [ ] Specific remediation action(s) required
- [ ] Resource requirements (personnel, budget, tools)
- [ ] Implementation owner and accountable executive
- [ ] Milestone dates and completion criteria
- [ ] Evidence required to demonstrate closure
- [ ] Dependencies on other projects or teams

### 4.2 Quick Wins
Identify and fast-track low-effort, high-impact remediations:
- Policy documentation gaps (write or update the document)
- Configuration changes (enable existing but disabled features)
- Process documentation (formalize existing informal processes)
- Training gaps (schedule existing training for missing personnel)

### 4.3 Budget and Resource Requests
For gaps requiring investment:
- [ ] Build business case with compliance risk quantification
- [ ] Include potential fine/penalty exposure for regulatory gaps
- [ ] Reference audit finding risk and potential business impact
- [ ] Present options with varying cost/compliance coverage tradeoffs
- [ ] Submit to budget approval process with CISO sponsorship

## Phase 5: Tracking and Continuous Compliance (Ongoing)

### 5.1 Remediation Tracking
- [ ] Track remediation progress weekly in GRC tool or tracking spreadsheet
- [ ] Report status to CISO monthly with red/yellow/green indicators
- [ ] Escalate blocked or delayed remediations
- [ ] Validate completed remediations with evidence collection

### 5.2 Continuous Monitoring
- [ ] Implement automated compliance monitoring where possible
- [ ] Schedule quarterly control effectiveness reviews
- [ ] Maintain evidence repository for audit readiness
- [ ] Update gap analysis when new regulations or framework versions are released
- [ ] Integrate compliance checks into DevSecOps pipeline (see `workflows/devsecops-pipeline-setup.md`)

### 5.3 Audit Preparation
- [ ] Organize evidence by control area 30 days before audit
- [ ] Conduct pre-audit self-assessment
- [ ] Brief relevant personnel on audit expectations and interview preparation
- [ ] Designate audit liaison for auditor communications

## Deliverables
- Unified control inventory with framework mapping
- Gap analysis report with risk-prioritized findings
- Remediation roadmap with owners, timelines, and resource requirements
- Compliance status dashboard for executive reporting
- Evidence repository organized by control area

## Cross-References

- `tasks/governance/security-policy-review.md` — Policy gap remediation
- `tasks/governance/risk-assessment-execution.md` — Risk context for prioritization
- `frameworks/nist-csf.md` — NIST CSF control requirements
- `frameworks/cis-controls-v8.md` — CIS Controls requirements
- `frameworks/nist-800-53-controls.md` — NIST 800-53 control details
- `archive/regulatory-milestones/gdpr-implementation-2018.md` — GDPR requirements
- `archive/regulatory-milestones/dora-eu-2025.md` — DORA requirements

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | compliance-audit-quality |
| Templates | reports/security-posture-report-template |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: cyber-chief + marcus-carey
