# Connectivity Matrix — Cybersecurity Squad

> Mapa de interconexao entre todos os componentes do squad.
> Referencia cruzada para navegacao e auditoria de integridade.

## 1. Core Routing Chain

```
config.yaml (routing brain)
    │
    ├── Define para cada task:
    │   ├── agents (quem executa)
    │   ├── frameworks (como executa)
    │   ├── checklists (quality gates)
    │   ├── templates (formato de output)
    │   └── registry (onde registra resultado)
    │
    └── Define governance:
        ├── escalation_rules
        ├── delegation_rules
        ├── cadence
        ├── score_thresholds
        ├── go_no_go
        ├── rework_loop
        ├── review_loops
        └── teams
```

## 2. Document-to-Document Connectivity

| From | To | Relationship | Type |
|------|----|-------------|------|
| `config.yaml` | `tasks/**/*.md` | Routes tasks to agents/frameworks/checklists/templates | routing |
| `config.yaml` | `agents/*.md` | Defines team membership and task assignments | routing |
| `config.yaml` | `frameworks/*.md` | Maps frameworks to tasks | routing |
| `config.yaml` | `checklists/**/*.md` | Maps quality gates to tasks | routing |
| `config.yaml` | `templates/**/*.md` | Maps output formats to tasks | routing |
| `config.yaml` | `data/registries/*.md` | Maps registries to tasks | routing |
| `config.yaml` | `data/metrics/*.md` | Defines KPIs and cadence | governance |
| `config.yaml` | `docs/quality-gate-system.md` | Score thresholds and gate logic | governance |
| `ARCHITECTURE.md` | `config.yaml` | Explains routing model | reference |
| `ARCHITECTURE.md` | `agents/*.md` | Defines HRM cascade and team structure | governance |
| `ARCHITECTURE.md` | `docs/*.md` | References governance documents | reference |
| `agents/*.md` | `tasks/**/*.md` | Agents execute tasks (listed in "Tasks que Executa") | execution |
| `agents/*.md` | `frameworks/*.md` | Agents use frameworks (listed in "Cross-References") | methodology |
| `agents/*.md` | `checklists/**/*.md` | Agents follow checklists (listed in "Cross-References") | quality |
| `agents/*.md` | `templates/**/*.md` | Agents produce outputs in templates | output |
| `agents/*.md` | `docs/quality-gate-system.md` | Quality bar references | quality |
| `agents/*.md` | `docs/hrm-governance-model.md` | Team membership references | governance |
| `tasks/**/*.md` | `config.yaml` | Task routing section mirrors config.yaml | routing |
| `tasks/**/*.md` | `docs/rework-loop-protocol.md` | Escalation rules reference | governance |
| `tasks/**/*.md` | `docs/delegation-protocol.md` | Out-of-scope handling reference | governance |
| `tasks/**/*.md` | `data/registries/*.md` | Tasks register results | memory |
| `workflows/*.md` | `tasks/**/*.md` | Workflows orchestrate task sequences | orchestration |
| `workflows/*.md` | `agents/*.md` | Workflows assign agents to stages | execution |
| `workflows/*.md` | `docs/quality-gate-system.md` | Per-stage gate logic | quality |
| `workflows/*.md` | `docs/rework-loop-protocol.md` | Rework between stages | quality |
| `docs/quality-gate-system.md` | `config.yaml` | Score thresholds source | governance |
| `docs/quality-gate-system.md` | `checklists/**/*.md` | Gate evaluation uses checklists | quality |
| `docs/quality-gate-system.md` | `docs/rework-loop-protocol.md` | Failure triggers rework | governance |
| `docs/hrm-governance-model.md` | `agents/*.md` | Team structure source | governance |
| `docs/hrm-governance-model.md` | `ARCHITECTURE.md` | Mirrors section 11 | reference |
| `docs/delegation-protocol.md` | `config.yaml` | Delegation rules source | governance |
| `docs/delegation-protocol.md` | `agents/cyber-chief.md` | Chief is delegator | governance |
| `docs/cadence-operations.md` | `config.yaml` | Cadence definition source | governance |
| `docs/cadence-operations.md` | `data/metrics/*.md` | Cadence updates metrics | memory |
| `docs/cadence-operations.md` | `data/registries/*.md` | Cadence updates registries | memory |
| `docs/cadence-operations.md` | `data/scorecards/*.md` | Cadence updates scorecards | memory |
| `docs/cross-squad-integration-guide.md` | `workflows/cross-squad-handoff-workflow.md` | Handoff process | integration |
| `data/registries/*.md` | `data/metrics/*.md` | Registry data feeds metrics | analysis |
| `data/metrics/*.md` | `data/scorecards/*.md` | Metrics feed scorecards | analysis |
| `data/backlog/improvement-backlog.md` | `data/registries/lessons-learned-registry.md` | Lessons become backlog items | learning |
| `data/scorecards/squad-scorecard.md` | `data/metrics/*.md` | Scorecard aggregates metrics | analysis |

## 3. Team-to-Task Matrix

| Team | Lead | Tasks (config.yaml routing) |
|------|------|-----------------------------|
| Discovery | cartographer | asset-discovery, attack-surface-mapping, identity-and-privilege-mapping, data-flow-mapping |
| Red Team | peter-kim | recon-and-enumeration, vuln-validation, safe-exploitation-simulation, lateral-movement-hypothesis, privilege-escalation-testing, credential-attack-testing, social-engineering-campaign, report-findings |
| Blue Team | chris-sanders | detection-coverage-mapping, detection-rule-development, threat-hunting-sprint, soc-operations-improvement, purple-team-exercise, tabletop-exercise-facilitation |
| AppSec | jim-manico | secure-code-review, api-security-review, sdlc-security-gates-setup, secrets-management-hardening, dependency-security-audit, security-champion-onboarding, threat-model-workshop |
| CloudSec | omar-santos | iam-least-privilege-project, storage-exposure-audit, cloud-logging-setup, network-segmentation-review, cloud-guardrails-setup, multi-cloud-security-review |
| IR | chris-sanders | triage-and-severity, containment-actions, eradication-and-recovery, evidence-collection, postmortem-and-actions, incident-communication |
| Governance | cyber-chief | intake tasks, review tasks, analysis tasks, operations tasks, security-policy-review, risk-assessment-execution, compliance-gap-analysis, security-awareness-campaign, vendor-security-review |
| Threat Intel | rogue | daily-threat-briefing, ioc-enrichment, threat-actor-profiling, vulnerability-intelligence, campaign-tracking |
| Forensics | chris-sanders | disk-image-analysis, memory-forensics, network-forensics, mobile-forensics, cloud-forensics |

## 4. Quality Gate Matrix

| Domain | Mandatory Gates | Domain-Specific Gates |
|--------|----------------|----------------------|
| ALL outputs | scope-and-roe-quality, evidence-chain-quality, security-report-quality | — |
| Red Team | (mandatory) | pentest-execution-quality, redteam-safe-testing-rules |
| AppSec | (mandatory) | code-review-security-quality, manico-ssdlc-gates |
| Blue Team | (mandatory) | detection-engineering-quality, blueteam-detection-coverage |
| IR | (mandatory) | incident-triage-quality, forensics-collection-quality |
| CloudSec | (mandatory) | cloud-security-assessment-quality, cloud-iam-least-privilege |

## 5. Feedback Loops

| Loop | Trigger | Flow | Output |
|------|---------|------|--------|
| Red → Blue (Purple) | Red Team finding | Finding → Detection gap → New rule → Validate → Coverage++ | Updated detection-rules-registry |
| Finding → Fix → Verify | Vuln identified | Finding → Remediation plan → Dev fix → Retest → Close | Updated findings-registry + remediation-registry |
| Incident → Improvement | Incident detected | Response → Postmortem → Actions → Detection improvement | Updated incident-registry + lessons-learned |
| Rework | Gate failure | Output rejected → Feedback → Agent revises → Resubmit → Re-gate | Updated decisions-log |
| Kaizen | Monthly cadence | Metrics review → Scorecard → Backlog grooming → Improvements | Updated improvement-backlog |

## 6. Cross-Squad Integration Points (All 12 MMOS Squads)

| Direction | Partner Squad | What Flows | Handoff Document |
|-----------|--------------|-----------|-----------------|
| OUT → | pre-programming | Threat model results, security architecture review, SDLC gates | docs/cross-squad-integration-guide.md |
| ← IN | pre-programming | Architecture docs, system design specs for security review | workflows/cross-squad-handoff-workflow.md |
| OUT → | data | Data protection controls, access audit findings, privacy impact assessment | docs/cross-squad-integration-guide.md |
| ← IN | data | Data pipeline configs, data classification requests | workflows/cross-squad-handoff-workflow.md |
| OUT → | design | Security UX recommendations, privacy pattern library | docs/cross-squad-integration-guide.md |
| ← IN | design | UI designs for security/privacy review | workflows/cross-squad-handoff-workflow.md |
| OUT → | brand | Phishing simulation brand guidelines, incident comms templates | docs/cross-squad-integration-guide.md |
| ← IN | brand | Brand assets for IP protection review | workflows/cross-squad-handoff-workflow.md |
| OUT → | copy | Security awareness content, incident notification drafts | docs/cross-squad-integration-guide.md |
| ← IN | copy | Security content drafts for technical review | workflows/cross-squad-handoff-workflow.md |
| OUT → | c-level | Security posture report, quarterly review, critical incident briefings | docs/cross-squad-integration-guide.md |
| ← IN | c-level | Strategic priorities, risk appetite definition | workflows/cross-squad-handoff-workflow.md |
| OUT → | advisory-board | Security program maturity report, risk register summary | docs/cross-squad-integration-guide.md |
| ← IN | advisory-board | Governance directives for policy alignment | workflows/cross-squad-handoff-workflow.md |
| OUT → | storytelling | Sanitized case studies, lessons learned narratives | docs/cross-squad-integration-guide.md |
| ← IN | storytelling | Narrative content for sensitivity review | workflows/cross-squad-handoff-workflow.md |
| OUT → | movement | Security culture program, security champion network | docs/cross-squad-integration-guide.md |
| ← IN | movement | Community platform plans for security review | workflows/cross-squad-handoff-workflow.md |
| OUT → | traffic-masters | Fraud detection alerts, bot traffic analysis | docs/cross-squad-integration-guide.md |
| ← IN | traffic-masters | Ad platform configs, tracking pixel deployments | workflows/cross-squad-handoff-workflow.md |
| OUT → | deepresearch | Threat landscape analysis requests, vulnerability research requests | docs/cross-squad-integration-guide.md |
| ← IN | deepresearch | Research on emerging threats | workflows/cross-squad-handoff-workflow.md |

## 7. Memory Architecture

```
Execution Layer          Memory Layer               Analysis Layer
─────────────           ────────────               ──────────────
Tasks produce    →     data/registries/*.md    →   data/metrics/*.md
outputs                (findings, incidents,        (KPIs, trends,
                        decisions, assets,           compliance scores)
                        detection rules,                    │
                        remediation,                        ▼
                        lessons learned)           data/scorecards/
                                                   squad-scorecard.md
                              │                            │
                              ▼                            ▼
                       data/backlog/              docs/cadence-operations.md
                       improvement-backlog.md     (triggers review cycles)
```

## Cross-References
- Architecture: `ARCHITECTURE.md`
- Config routing: `config.yaml`
- Quality gates: `docs/quality-gate-system.md`
- HRM model: `docs/hrm-governance-model.md`
- Delegation: `docs/delegation-protocol.md`
- Rework: `docs/rework-loop-protocol.md`
- Cadence: `docs/cadence-operations.md`
- Cross-squad: `docs/cross-squad-integration-guide.md`

---

*Connectivity Matrix v2.0.0 — MMOS Audit v3*
