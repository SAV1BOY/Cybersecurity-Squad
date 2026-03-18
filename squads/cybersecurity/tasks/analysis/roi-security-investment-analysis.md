# Task: ROI Security Investment Analysis

## Objetivo
Analisar o retorno sobre investimento em seguranca, quantificando o valor de controles implementados, reducao de risco e justificando investimentos futuros.

## Agents
- **cyber-chief** (lead) — Conduz analise de ROI
- **marcus-carey** (support) — Contextualiza valor de cultura e awareness

## Inputs
- Custos de seguranca (ferramentas, equipe, servicos)
- Metricas de reducao de risco (before/after)
- Dados de incidentes evitados ou contidos
- FAIR risk quantification framework

## Steps
1. Inventariar investimentos em seguranca por categoria
2. Quantificar reducao de risco por controle implementado
3. Estimar custo evitado por incidentes prevenidos ou contidos
4. Calcular ROI por investimento usando FAIR ou modelo equivalente
5. Comparar custo de breach vs custo de prevencao
6. Identificar investimentos com maior retorno
7. Identificar areas sub-investidas com alto risco residual
8. Projetar ROI de investimentos futuros propostos
9. Gerar relatorio de ROI para justificar budget
10. Registrar no `security-kpis`

## Output
- Relatorio de ROI de seguranca com quantificacao
- Analise de investimentos com maior e menor retorno
- Projecao de ROI para investimentos futuros
- Justificativa de budget para proximo ciclo

## Quality Gates
- [ ] Investimentos inventariados por categoria
- [ ] Reducao de risco quantificada com metodologia FAIR
- [ ] Custo evitado estimado com premissas documentadas
- [ ] ROI calculado por investimento relevante
- [ ] Projecoes de ROI futuro com premissas claras
- [ ] Relatorio adequado para audiencia executiva

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | fair-risk-quantification, governance-layer |
| Checklists | — |
| Templates | reports/quarterly-security-report-template |
| Registry | data/metrics/security-kpis |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: quarterly cadence
- **Delivers to**: cyber-chief / stakeholders
