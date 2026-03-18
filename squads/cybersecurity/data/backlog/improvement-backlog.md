# Improvement Backlog — Cybersecurity Squad

> Lista priorizada de melhorias identificadas via postmortems, quality gate failures, metrics reviews e auditorias.
> Gerenciado pelo cyber-chief. Revisado mensalmente (ver docs/cadence-operations.md).

## Backlog

| ID | Prioridade | Origem | Descricao | Dominio | Owner | Status | Data Criacao | Data Resolucao |
|----|------------|--------|-----------|---------|-------|--------|--------------|----------------|
| IMP-001 | Alta | Audit 2026-03 | Adicionar cross-references em todos os task files | Governance | cyber-chief | open | 2026-03-18 | — |
| IMP-002 | Alta | Audit 2026-03 | Workflow files usam nomes genericos em vez de agent IDs reais | Workflows | cyber-chief | open | 2026-03-18 | — |
| IMP-003 | Media | Audit 2026-03 | Task files sem subtask breakdown com dependencias | Tasks | cyber-chief | open | 2026-03-18 | — |
| IMP-004 | Media | Audit 2026-03 | Scripts nao integrados com workflows | Scripts | cyber-chief | open | 2026-03-18 | — |
| IMP-005 | Baixa | Audit 2026-03 | Projects templates sem workflow mapping | Projects | cyber-chief | open | 2026-03-18 | — |

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
