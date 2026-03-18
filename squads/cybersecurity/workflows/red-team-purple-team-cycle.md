# Red Team / Purple Team Continuous Assessment Cycle

## Purpose

Establish a continuous cycle of adversary simulation (red team) and collaborative detection validation (purple team) to systematically identify defensive gaps, validate detection capabilities, and drive measurable security improvement. This workflow ensures that offensive assessments translate directly into defensive uplift.

## Scope

Covers internal red team operations, purple team exercises, and the feedback loop between offensive findings and defensive improvements. Aligns with MITRE ATT&CK framework for coverage tracking.

---

## The Continuous Cycle

```
    [PLAN] --> [RED TEAM EXECUTE] --> [PURPLE TEAM VALIDATE]
       ^                                       |
       |                                       v
    [MEASURE] <-- [DEFEND IMPROVE] <-- [DEBRIEF & ANALYZE]
```

Each cycle targets specific MITRE ATT&CK tactics or threat actor TTPs. Cycles run quarterly with mini-sprints monthly.

## Phase 1: Planning (Week 1-2)

### 1.1 Threat-Informed Targeting
- [ ] Review current threat intelligence for relevant threat actors
- [ ] Map threat actor TTPs to MITRE ATT&CK techniques
- [ ] Identify ATT&CK techniques with no detection coverage (see `frameworks/detection-coverage-matrix.md`)
- [ ] Prioritize techniques based on: threat relevance, detection gap, business risk
- [ ] Select 5-10 techniques per cycle for testing

### 1.2 Engagement Scoping
- [ ] Define objectives: detection validation, control bypass, end-to-end kill chain
- [ ] Establish rules of engagement and safety boundaries
- [ ] Identify target systems and data (crown jewels for realistic scenarios)
- [ ] Define success criteria for both red team (objectives achieved) and blue team (detection)
- [ ] Set communication protocols and emergency stop procedures

### 1.3 Scenario Development
Design realistic attack scenarios based on selected techniques:
- [ ] Initial access vector (phishing, external exploit, supply chain, insider)
- [ ] Persistence mechanisms to be tested
- [ ] Lateral movement paths to target objectives
- [ ] Data staging and exfiltration methods
- [ ] Impact simulation (ransomware deployment simulation, data theft)
- [ ] Document expected detection opportunities at each kill chain stage

## Phase 2: Red Team Execution (Weeks 3-5)

### 2.1 Execution Principles
- Operate with adversary mindset: stealth, patience, persistence
- Use real adversary tooling and techniques (not just automated scanners)
- Document every action with timestamps for later purple team correlation
- Maintain operational security (separate infrastructure, clean attribution)
- Follow safety protocols: no production impact, no customer data access

### 2.2 Kill Chain Execution Log
For each technique executed, document:
```
Technique ID: T1059.001 (PowerShell)
Timestamp: 2026-03-06 14:32:00 UTC
Target System: WS-FINANCE-042
Command/Action: [exact command or action taken]
Artifacts Generated: [process, file, network, registry artifacts]
Expected Detection: [SIEM rule, EDR alert, NDR signature]
Actual Detection: [to be filled during purple team phase]
Result: Success/Detected/Blocked
```

### 2.3 Objective Tracking

| Objective | Technique Chain | Status | Detection Evaded |
|-----------|----------------|--------|-----------------|
| Domain Admin | T1566 > T1059 > T1003 > T1078 | _____ | _____ |
| Data Exfiltration | T1074 > T1560 > T1041 | _____ | _____ |
| Persistence | T1547 > T1053 > T1136 | _____ | _____ |
| Lateral Movement | T1021 > T1570 > T1210 | _____ | _____ |

## Phase 3: Purple Team Validation (Week 6)

### 3.1 Collaborative Review
Red team and blue team sit together to review each attack step:
- [ ] Red team reveals exact actions and timestamps
- [ ] Blue team searches SIEM, EDR, and NDR for corresponding alerts
- [ ] For each technique, classify detection result:
  - **Detected and Alerted**: Alert fired, analyst notified
  - **Logged but No Alert**: Evidence exists in logs but no detection rule triggered
  - **Partially Detected**: Related activity detected but not the specific technique
  - **Not Detected**: No evidence captured anywhere
  - **Blocked**: Preventive control stopped the technique

### 3.2 Detection Gap Analysis
For each undetected technique:
- [ ] Determine if telemetry exists (logs available but no rule)
- [ ] Determine if telemetry is missing (logging gap)
- [ ] Assess feasibility of creating detection rule
- [ ] Estimate false positive rate of potential rule
- [ ] Prioritize detection engineering work

### 3.3 Live Detection Engineering
During purple team sessions, collaboratively build detections:
- [ ] Write detection rule for highest-priority undetected technique
- [ ] Red team re-executes technique to validate detection
- [ ] Tune rule to minimize false positives
- [ ] Document rule in detection rules registry (see `data/registries/detection-rules-registry.md`)
- [ ] Repeat for each gap identified

## Phase 4: Debrief and Analysis (Week 7)

### 4.1 Findings Report
- [ ] Executive summary: objectives, results, key risks identified
- [ ] Technique-by-technique results with detection status
- [ ] Attack narrative: how an adversary could achieve critical objectives
- [ ] Detection coverage heat map (ATT&CK Navigator visualization)
- [ ] Prioritized remediation recommendations

### 4.2 Metrics Calculation

| Metric | Formula | This Cycle | Previous |
|--------|---------|------------|----------|
| Detection Rate | Detected / Total Techniques Tested | ___% | ___% |
| Alert Rate | Alerted / Total Techniques Tested | ___% | ___% |
| Block Rate | Blocked / Total Techniques Tested | ___% | ___% |
| Mean Time to Detect | Avg time from execution to alert | ___ min | ___ min |
| Coverage Score | Techniques with detection / Total ATT&CK techniques | ___% | ___% |

### 4.3 Stakeholder Briefing
- [ ] Brief CISO on key findings and risk posture
- [ ] Present to SOC team for awareness and training
- [ ] Share sanitized findings with engineering for remediation
- [ ] Update risk register with identified control gaps

## Phase 5: Defensive Improvement (Weeks 8-12)

### 5.1 Detection Engineering Sprint
- [ ] Implement detection rules for all identified gaps (see `workflows/detection-engineering-workflow.md`)
- [ ] Deploy additional logging where telemetry gaps were identified
- [ ] Tune existing rules that generated false negatives
- [ ] Update SIEM correlation rules for multi-step attack patterns
- [ ] Add new threat hunting hypotheses based on red team TTPs

### 5.2 Control Hardening
- [ ] Patch or mitigate vulnerabilities exploited during engagement
- [ ] Harden configurations that enabled technique success
- [ ] Deploy additional preventive controls where feasible
- [ ] Update security baselines and compliance checks

### 5.3 Validation
- [ ] Re-test previously undetected techniques (atomic red team tests)
- [ ] Confirm new detections fire correctly
- [ ] Verify no regression in existing detection capabilities
- [ ] Update ATT&CK coverage matrix

## Phase 6: Cycle Planning (Feed into Next Cycle)

- [ ] Select next cycle's target techniques based on remaining gaps
- [ ] Incorporate new threat intelligence into scenario planning
- [ ] Rotate red team operators to bring fresh perspectives
- [ ] Adjust scope based on organizational changes and new assets
- [ ] Schedule next cycle kickoff

## Annual Objectives

- Complete 4 major red/purple team cycles per year
- Achieve > 80% detection rate across tested ATT&CK techniques
- Reduce mean time to detect from cycle to cycle
- Expand ATT&CK coverage by 15% per year
- Produce 20+ new detection rules per cycle

## Cross-References

- `frameworks/detection-coverage-matrix.md` — ATT&CK detection tracking
- `frameworks/red-team-maturity-model.md` — Red team capability maturity
- `workflows/detection-engineering-workflow.md` — Detection rule development
- `workflows/threat-hunting-sprint-workflow.md` — Threat hunting integration
- `tasks/red-team/recon-and-enumeration.md` — Red team task details
- `scripts/detection-rule-templates.md` — Sigma, YARA, Snort templates

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
