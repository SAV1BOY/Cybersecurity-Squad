# Task: Detection Effectiveness Analysis

## Objetivo
Analisar a eficacia das deteccoes existentes, medindo precision, recall, false positive rate e tempo de deteccao para otimizar a estrategia de deteccao.

## Agents
- **chris-sanders** (lead) — Analisa eficacia de deteccao
- **shannon-runner** (executor) — Executa analises estatisticas

## Inputs
- Metricas de deteccao atuais
- Registros de alertas (true positives, false positives)
- Detection coverage map
- Detection rules registry

## Steps
1. Coletar metricas de todas as regras de deteccao ativas
2. Calcular precision e recall por regra e por categoria
3. Identificar regras com alto false positive rate
4. Medir mean time to detect (MTTD) por tipo de ameaca
5. Analisar regras que nunca trigaram (dormant rules)
6. Avaliar cobertura de deteccao por ATT&CK tactic
7. Comparar eficacia entre fontes de log (EDR, SIEM, cloud)
8. Identificar oportunidades de tuning e consolidacao
9. Documentar recomendacoes de otimizacao priorizadas
10. Registrar metricas no `detection-metrics`

## Output
- Relatorio de detection effectiveness com metricas
- Lista de regras para tuning ou aposentadoria
- Recomendacoes de otimizacao priorizadas
- Registro no `detection-metrics`

## Quality Gates
- [ ] Precision e recall calculados por regra
- [ ] Regras de alto FP rate identificadas
- [ ] MTTD calculado por tipo de ameaca
- [ ] Dormant rules identificadas e avaliadas
- [ ] Cobertura por ATT&CK tactic documentada
- [ ] Checklist `blueteam-detection-coverage` atendido
- [ ] Checklist `blueteam-monitoring-slo` validado
