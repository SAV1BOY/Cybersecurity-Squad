# Task: Maturity Assessment

## Objetivo
Avaliar o nivel de maturidade de seguranca da organizacao usando modelo estruturado, identificando areas de forca e oportunidades de evolucao por dominio.

## Agents
- **cyber-chief** (lead) — Conduz avaliacao de maturidade
- **marcus-carey** (support) — Avalia maturidade cultural e operacional

## Inputs
- Red Team Maturity Model do squad
- Security KPI dashboard
- Resultados de assessments anteriores
- Feedback de stakeholders e equipes

## Steps
1. Selecionar modelo de maturidade (interno ou CMMI/OWASP SAMM)
2. Definir dominios de avaliacao (governance, offense, defense, appsec, cloud, IR)
3. Coletar evidencias de maturidade por dominio
4. Avaliar cada dominio em escala definida (1-5 ou Initial-Optimized)
5. Identificar areas de forca e areas com maior gap
6. Comparar com assessment anterior para medir evolucao
7. Priorizar areas de investimento por impacto no risk posture
8. Definir targets de maturidade para proximo periodo
9. Gerar relatorio de maturity assessment com roadmap
10. Registrar no `maturity-score-history`

## Output
- Relatorio de maturity assessment por dominio
- Score de maturidade atual vs target
- Roadmap de evolucao com prioridades
- Registro historico no `maturity-score-history`

## Quality Gates
- [ ] Modelo de maturidade aplicado consistentemente
- [ ] Todos os dominios avaliados com evidencias
- [ ] Comparacao com assessment anterior realizada
- [ ] Targets de maturidade realistas e acordados
- [ ] Roadmap de evolucao com prioridades definidas
- [ ] Checklist `compliance-audit-quality` atendido

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | red-team-maturity-model, security-kpi-dashboard, governance-layer |
| Checklists | compliance-audit-quality |
| Templates | reports/security-posture-report-template |
| Registry | data/metrics/maturity-score-history |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: quarterly/annual cadence
- **Delivers to**: improvement-backlog
