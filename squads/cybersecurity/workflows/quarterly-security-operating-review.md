# Quarterly Security Operating Review

Processo para conduzir a revisao operacional trimestral do programa de seguranca.

## Objetivo

Avaliar o desempenho do programa de seguranca no trimestre, reportar metricas para a lideranca, ajustar prioridades e alinhar recursos para o proximo periodo.

## Inputs

- Metricas de seguranca coletadas ao longo do trimestre
- Relatorios de incidentes, pentests e auditorias do periodo
- OKRs e metas de seguranca definidos no inicio do trimestre
- Feedback de stakeholders e equipes parceiras

## Stages

### 1. Data Collection

- Responsavel: **shannon-runner**
- Consolidar metricas de todas as fontes (vuln management, IR, detection, compliance)
- Calcular KPIs principais: MTTD, MTTR, SLA compliance, cobertura de deteccao
- Preparar comparativos com trimestres anteriores

### 2. Performance Analysis

- Responsavel: **cyber-chief**
- Analisar tendencias nas metricas coletadas
- Identificar areas de melhoria e deterioracao
- Ponto de decisao: **Metas do trimestre atingidas?**
  - Sim -> documentar fatores de sucesso
  - Nao -> analisar root causes e propor correcoes

### 3. Incident Review

- Responsavel: **chris-sanders + cyber-chief**
- Sumarizar incidentes do trimestre por tipo e severidade
- Destacar lessons learned mais significativas
- Avaliar eficacia das melhorias implementadas pos-incidente

### 4. Program Health Assessment

- Responsavel: **cyber-chief**
- Avaliar saude do time (headcount, turnover, skill gaps)
- Revisar status de projetos e iniciativas em andamento
- Identificar riscos e bloqueadores para o proximo trimestre

### 5. Risk Landscape Update

- Responsavel: **chris-sanders + rogue + shannon-runner**
- Atualizar o panorama de ameacas relevantes ao setor
- Identificar novas ameacas emergentes que requerem atencao
- Recomendar ajustes na estrategia de seguranca

### 6. Executive Presentation

- Responsavel: **cyber-chief**
- Preparar apresentacao executiva com metricas-chave
- Destacar conquistas, riscos e necessidades de investimento
- Propor OKRs e prioridades para o proximo trimestre

### 7. Action Planning

- Responsavel: **cyber-chief**
- Definir action items baseados na revisao
- Atribuir owners e deadlines para cada item
- Priorizar iniciativas para o proximo trimestre

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Metricas em declinio | KPIs pioraram vs trimestre anterior | Investigar root cause e alocar recursos |
| Budget insuficiente | Necessidades excedem orcamento | Preparar business case para investimento |
| Skill gap critico | Capacidade ausente no time | Planejar contratacao ou treinamento |
| Mudanca regulatoria | Novo requisito de compliance | Avaliar impacto e ajustar roadmap |

## Outputs

- Relatorio trimestral de seguranca para a lideranca
- Dashboard de metricas atualizado
- OKRs e prioridades para o proximo trimestre
- Action items com owners e deadlines
- Risk register atualizado

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
