# Operational Risk Log — Cybersecurity Squad

> Riscos operacionais que afetam o proprio squad (nao riscos de clientes).
> Gerenciado pelo cyber-chief. Revisado trimestralmente.

## Risk Register

| ID | Risk | Likelihood | Impact | Score | Mitigation | Owner | Status | Review Date |
|----|------|-----------|--------|-------|------------|-------|--------|-------------|
| OPR-001 | Agent bottleneck — cyber-chief centraliza demais e cria gargalo | Media | Alto | 12 | Delegar decisoes de baixo risco a domain leads | cyber-chief | open | — |
| OPR-002 | Knowledge silos — conhecimento critico em um unico agente | Media | Alto | 12 | Cross-training via purple team exercises e pair operations | cyber-chief | open | — |
| OPR-003 | Quality gate fatigue — gates ignorados por excesso de checklist items | Baixa | Alto | 8 | Revisar e simplificar checklists trimestralmente | cyber-chief | open | — |
| OPR-004 | Cross-squad handoff friction — outros squads nao seguem protocolo | Media | Medio | 9 | Treinamento e onboarding de squads parceiros | marcus-carey | open | — |
| OPR-005 | Stale registries — registries nao atualizados apos task completion | Media | Medio | 9 | Cadence semanal de review + automation scripts | cyber-chief | open | — |
| OPR-006 | OPSEC violation — segredo ou dado real commitado acidentalmente | Baixa | Critico | 10 | Pre-commit hooks, review process, swipe.config rules | cyber-chief | open | — |

### Score = Likelihood (1-5) x Impact (1-5)
- **1-6**: Low risk — monitor
- **7-12**: Medium risk — mitigate
- **13-19**: High risk — immediate action
- **20-25**: Critical risk — stop and resolve

## Cross-References
- Risk register (client-facing): `data/registries/risk-register.md`
- Assumptions: `data/assumptions/operating-assumptions.md`
- Improvement backlog: `data/backlog/improvement-backlog.md`
- Cadence: `docs/cadence-operations.md` (reviewed quarterly)
