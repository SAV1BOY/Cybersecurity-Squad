# Task: Threat Modeling

## Objetivo
Construir threat models para os sistemas e aplicacoes in-scope, identificando ameacas, vetores de ataque e controles necessarios de forma estruturada.

## Agents
- **jim-manico** (lead) — Conduz modelagem de ameacas
- **cyber-chief** (support) — Alinha com contexto de risco do negocio

## Inputs
- Asset inventory e attack surface map
- Arquitetura dos sistemas in-scope
- Data flow diagrams (se disponiveis)
- Risk context do engagement

## Steps
1. Selecionar metodologia de threat modeling (STRIDE, PASTA, ou hibrido)
2. Decompor o sistema em componentes e trust boundaries
3. Identificar data flows entre componentes
4. Aplicar STRIDE para cada componente e data flow
5. Identificar threat actors relevantes ao contexto
6. Mapear attack vectors para cada ameaca identificada
7. Avaliar controles existentes contra cada ameaca
8. Priorizar ameacas por probabilidade e impacto
9. Documentar mitigacoes recomendadas para gaps identificados
10. Gerar relatorio de threat model usando template padrao

## Output
- Threat model documentado por sistema/aplicacao
- Lista de ameacas priorizadas com attack vectors
- Gap analysis entre controles existentes e necessarios
- Registro no `risk-register`

## Quality Gates
- [ ] Metodologia de threat modeling aplicada consistentemente
- [ ] Trust boundaries claramente definidos
- [ ] Data flows mapeados entre todos os componentes
- [ ] Ameacas classificadas por probabilidade e impacto
- [ ] Controles existentes avaliados contra cada ameaca
- [ ] Mitigacoes recomendadas sao acionaveis e especificas
- [ ] Checklist `threat-model-quality` 100% atendido

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | stride-threat-model, pasta-threat-model, appsec-layer |
| Checklists | threat-model-quality, manico/manico-owasp-top10-mapping |
| Templates | briefs/threat-model-brief, reports/threat-model-report-template |
| Registry | data/registries/risk-register |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: data-flow-mapping
- **Delivers to**: appsec tasks
