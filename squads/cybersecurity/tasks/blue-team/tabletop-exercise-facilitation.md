# Task: Tabletop Exercise Facilitation

## Objetivo
Facilitar exercicios tabletop de resposta a incidentes, testando a capacidade da organizacao de responder a cenarios de ameaca sem impacto no ambiente real.

## Agents
- **marcus-carey** (lead) — Facilita exercicio e modera discussoes
- **cyber-chief** (support) — Avalia prontidao organizacional

## Inputs
- Cenarios de ameaca relevantes ao setor
- Plano de resposta a incidentes existente
- Lista de participantes (IR team, management, legal, comms)
- Lessons learned de incidentes anteriores

## Steps
1. Definir cenario de ameaca realistico baseado em threat landscape
2. Preparar injects (novos eventos) para cada fase do cenario
3. Identificar e convidar participantes de todas as areas relevantes
4. Apresentar cenario inicial e contexto para participantes
5. Facilitar discussao guiada com injects em cada fase
6. Avaliar decisoes dos participantes contra IR playbooks
7. Identificar gaps em processos, comunicacao e decisao
8. Conduzir hotwash imediato apos exercicio
9. Documentar findings e recomendacoes de melhoria
10. Registrar no `lessons-learned-registry`

## Output
- Relatorio do exercicio tabletop com cenario e resultados
- Lista de gaps identificados em processos de IR
- Recomendacoes de melhoria priorizadas
- Registro no `lessons-learned-registry`

## Quality Gates
- [ ] Cenario realistico e relevante ao threat landscape
- [ ] Participantes de todas as areas criticas presentes
- [ ] Injects testaram cada fase do IR lifecycle
- [ ] Gaps de processo e comunicacao documentados
- [ ] Recomendacoes sao acionaveis com responsaveis definidos
- [ ] Checklist `tabletop-exercise-quality` atendido
- [ ] Checklist `carey-communication-under-pressure` validado

## Routing & Escalation
- **frameworks**: ir-layer
- **checklists**: tabletop-exercise-quality, carey/carey-communication-under-pressure
- **templates**: reports/postmortem-template
- **registry**: data/registries/lessons-learned-registry
- **receives_from**: quarterly cadence
- **delivers_to**: improvement-backlog
