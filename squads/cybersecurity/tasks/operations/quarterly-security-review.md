# Task: Quarterly Security Review

## Objetivo
Conduzir revisao trimestral de seguranca, consolidando metricas, avaliando progresso contra targets e definindo prioridades para o proximo trimestre.

## Agents
- **cyber-chief** (lead) — Conduz revisao trimestral
- **marcus-carey** (support) — Contribui com perspectiva cultural e operacional

## Inputs
- Security KPIs do trimestre
- Findings e remediações do periodo
- Maturity assessment atual
- OKRs e targets de seguranca

## Steps
1. Consolidar metricas de seguranca do trimestre (KPIs)
2. Comparar metricas com targets definidos
3. Analisar progresso de remediacao e closure rates
4. Revisar detection coverage evolution
5. Avaliar incidentes do periodo e lessons learned
6. Medir progresso de maturity assessment
7. Identificar top wins e top risks do trimestre
8. Definir prioridades e targets para proximo trimestre
9. Gerar relatorio trimestral para stakeholders
10. Registrar no `security-kpis` e `decisions-log`

## Output
- Relatorio trimestral de seguranca
- Comparativo de KPIs vs targets
- Prioridades do proximo trimestre definidas
- Registro no `security-kpis`

## Quality Gates
- [ ] KPIs do trimestre consolidados e comparados
- [ ] Progresso de remediacao documentado
- [ ] Incidentes do periodo analisados
- [ ] Top wins e top risks identificados
- [ ] Prioridades do proximo trimestre acordadas
- [ ] Relatorio adequado para audiencia executiva

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer, security-kpi-dashboard |
| Checklists | compliance-audit-quality |
| Templates | reports/quarterly-security-report-template |
| Registry | data/metrics/security-kpis, data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: quarterly cadence
- **Delivers to**: stakeholders
