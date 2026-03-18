# Task: Trend Analysis — Vulnerability Backlog

## Objetivo
Analisar tendencias do backlog de vulnerabilidades, identificando padroes de acumulo, gargalos de remediacao e eficacia dos SLAs de correcao.

## Agents
- **cyber-chief** (lead) — Analisa trends e direciona estrategia
- **omar-santos** (support) — Contribui com dados operacionais

## Inputs
- Vulnerability backlog historico
- SLAs de remediacao por severidade
- Metricas de mean time to remediate
- Dados do `vulnerability-metrics`

## Steps
1. Extrair dados historicos de vulnerabilidades (abertura e fechamento)
2. Calcular taxa de entrada vs taxa de remediacao por periodo
3. Identificar trends de acumulo ou reducao do backlog
4. Analisar compliance com SLAs por severidade
5. Identificar categorias de vuln com maior reincidencia
6. Mapear gargalos no processo de remediacao
7. Calcular mean time to remediate por severidade e equipe
8. Projetar trajectory do backlog com ritmo atual
9. Documentar recomendacoes para melhorar velocity de remediacao
10. Registrar metricas no `vulnerability-metrics`

## Output
- Relatorio de trend analysis com graficos e projecoes
- SLA compliance rate por severidade
- Gargalos de remediacao identificados
- Recomendacoes para melhorar velocity

## Quality Gates
- [ ] Dados historicos suficientes para analise de trends
- [ ] SLA compliance calculado por severidade
- [ ] Gargalos de remediacao identificados com causa raiz
- [ ] Projecao de trajectory do backlog documentada
- [ ] Recomendacoes acionaveis para melhorar velocity
- [ ] Checklist `remediation-plan-quality` validado

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | vuln-triage-playbook, security-kpi-dashboard |
| Checklists | remediation-plan-quality |
| Templates | trackers/vuln-backlog-template, trackers/remediation-sla-tracker |
| Registry | data/metrics/vulnerability-metrics |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: weekly cadence
- **Delivers to**: remediation prioritization
