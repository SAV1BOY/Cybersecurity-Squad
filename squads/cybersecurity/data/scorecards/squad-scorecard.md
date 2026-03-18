# Squad Scorecard — Cybersecurity Squad

> Registro consolidado de maturidade, KPIs e evolucao do squad.
> Atualizado mensalmente pelo cyber-chief.

## Maturity Score por Dominio

| Dominio | Score (1-5) | Target | Trend | Ultima Atualizacao |
|---------|-------------|--------|-------|--------------------|
| Discovery | 3.2 | 3.5 | Up | 2026-03 |
| Red Team (Offense) | 3.4 | 3.5 | Up | 2026-03 |
| Blue Team (Defense) | 3.0 | 3.5 | Up | 2026-03 |
| AppSec | 2.8 | 3.5 | Up | 2026-03 |
| CloudSec | 2.6 | 3.5 | Up | 2026-03 |
| Incident Response | 3.1 | 3.5 | Stable | 2026-03 |
| Governance | 3.3 | 3.5 | Up | 2026-03 |
| **Squad Geral** | **2.8** | **3.5** | **Up** | **2026-03** |

## KPIs — Actuals vs Targets

| KPI | Target | Actual | Status | Periodo |
|-----|--------|--------|--------|---------|
| MTTD (Mean Time to Detect) | < 4h | 6.2h | Below Target | 2026-03 |
| MTTC (Mean Time to Contain) | < 2h | 1.8h | On Target | 2026-03 |
| MTTR (Mean Time to Remediate) | < 30d | 42d | Below Target | 2026-03 |
| Vuln SLA Compliance | > 90% | 82% | Below Target | 2026-03 |
| Detection Coverage (ATT&CK) | > 75% | 62% | Below Target | 2026-03 |
| False Positive Rate | < 10% | 8.3% | On Target | 2026-03 |
| Patch Coverage | > 95% | 88% | Below Target | 2026-03 |
| Security Training Completion | 100% | 94% | Below Target | 2026-03 |
| Phishing Click Rate | < 5% | 8.3% | Below Target | 2026-03 |
| Compliance Rate | > 95% | 91% | Below Target | 2026-03 |
| Risk Posture Score | < 15 | 18 | Below Target | 2026-03 |
| Security Maturity Score | > 3.5 | 2.8 | Below Target | 2026-03 |

## Quality Gate Pass Rates

| Gate Type | Pass Rate | Rework Rate | Escalation Rate |
|-----------|-----------|-------------|-----------------|
| Red Team gates | 88% | 10% | 2% |
| Blue Team gates | 82% | 14% | 4% |
| AppSec gates | 85% | 12% | 3% |
| CloudSec gates | 80% | 16% | 4% |
| IR gates | 90% | 8% | 2% |
| Cross-squad handoff gates | 78% | 18% | 4% |

## Cross-Squad SLA Compliance

| Squad Parceiro | Requests Recebidos | Atendidos no SLA | % Compliance |
|----------------|--------------------|--------------------|--------------|
| pre-programming | 12 | 10 | 83% |
| data | 8 | 7 | 88% |
| c-level | 6 | 6 | 100% |
| deepresearch | 4 | 3 | 75% |
| traffic-masters | 3 | 2 | 67% |

## Improvement Trend

| Mes | Score Geral | Principais Melhorias | Principais Riscos |
|-----|------------|----------------------|--------------------|
| 2026-01 | 2.4 | Initial squad setup, agent definitions | No quality gates, no cross-refs |
| 2026-02 | 2.6 | Frameworks and checklists populated | Workflows generic, no routing |
| 2026-03 | 2.8 | Full MMOS audit remediation, quality gates, HRM cascade | MTTD above target, detection coverage gap |

## Priority Actions (from Improvement Backlog)

1. **Reduce MTTD to < 4h** — Improve detection rule coverage and SOC automation
2. **Increase Detection Coverage to > 75%** — Map remaining ATT&CK techniques
3. **Improve Vuln SLA Compliance to > 90%** — Streamline remediation workflow
4. **Reduce Phishing Click Rate to < 5%** — Intensify awareness campaigns
5. **Increase CloudSec maturity to 3.0+** — Complete IAM and logging projects

## Cross-References
- KPI definitions: `data/metrics/security-kpis.md`
- Improvement backlog: `data/backlog/improvement-backlog.md`
- Cadence: `docs/cadence-operations.md` (updated monthly)
- Config: `config.yaml > cadence > monthly`
- Quality gate system: `docs/quality-gate-system.md`
- HRM governance: `docs/hrm-governance-model.md`
