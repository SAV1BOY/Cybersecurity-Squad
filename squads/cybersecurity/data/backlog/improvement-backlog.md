# Improvement Backlog — Cybersecurity Squad

> Lista priorizada de melhorias identificadas via postmortems, quality gate failures, metrics reviews e auditorias.
> Gerenciado pelo cyber-chief. Revisado mensalmente (ver docs/cadence-operations.md).

## Backlog

| ID | Prioridade | Origem | Descricao | Dominio | Owner | Status | Data Criacao | Data Resolucao |
|----|------------|--------|-----------|---------|-------|--------|--------------|----------------|
| IMP-001 | Alta | Audit v2 2026-03 | Adicionar cross-references em todos os task files | Governance | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-002 | Alta | Audit v2 2026-03 | Workflow files usam nomes genericos em vez de agent IDs reais | Workflows | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-003 | Media | Audit v2 2026-03 | Task files sem subtask breakdown com dependencias | Tasks | cyber-chief | open | 2026-03-18 | — |
| IMP-004 | Media | Audit v2 2026-03 | Scripts nao integrados com workflows | Scripts | cyber-chief | open | 2026-03-18 | — |
| IMP-005 | Baixa | Audit v2 2026-03 | Projects templates sem workflow mapping | Projects | cyber-chief | open | 2026-03-18 | — |
| IMP-006 | Critica | Audit v3 2026-03 | 15 tasks (governance, forensics, threat-intel) sem routing no config.yaml | Config | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-007 | Alta | Audit v3 2026-03 | Cross-squad integration limitada a 3 squads em vez de 12 | Integration | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-008 | Alta | Audit v3 2026-03 | Scorecard sem dados reais populados | Data | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-009 | Media | Audit v3 2026-03 | Frameworks sem secao 'Used By' (link bidirecional) | Frameworks | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-010 | Media | Audit v3 2026-03 | Reduzir MTTD para < 4h (atual 6.2h) | Blue Team | chris-sanders | open | 2026-03-18 | — |
| IMP-011 | Media | Audit v3 2026-03 | Aumentar Detection Coverage para > 75% (atual 62%) | Blue Team | chris-sanders | open | 2026-03-18 | — |
| IMP-012 | Media | Audit v3 2026-03 | Melhorar Vuln SLA Compliance para > 90% (atual 82%) | Red Team | omar-santos | open | 2026-03-18 | — |
| IMP-013 | Baixa | Audit v3 2026-03 | Adicionar protocolo de colaboracao inter-agente | Architecture | cyber-chief | done | 2026-03-18 | 2026-03-18 |
| IMP-014 | Baixa | Audit v3 2026-03 | Criar data/meeting-minutes/ e data/memos/ | Data | cyber-chief | open | 2026-03-18 | — |

### Prioridade
- **Critica**: Bloqueia operacao do squad
- **Alta**: Impacta qualidade significativamente
- **Media**: Melhoria incremental importante
- **Baixa**: Nice-to-have

### Status
- **open**: Identificado, aguardando trabalho
- **in-progress**: Em execucao
- **done**: Concluido e verificado
- **wont-fix**: Decidido nao implementar (com justificativa)

## Cross-References
- Scorecard: `data/scorecards/squad-scorecard.md`
- Lessons learned: `data/registries/lessons-learned-registry.md`
- Decisions log: `data/registries/decisions-log.md`
- Cadence: `docs/cadence-operations.md` (groomed monthly)
