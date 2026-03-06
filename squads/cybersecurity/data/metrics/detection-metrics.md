# Detection Metrics

Metricas de eficacia e eficiencia das capacidades de deteccao de ameacas.

## Metricas de Eficacia

| Metric | Current | Target | Notes |
|--------|---------|--------|-------|
| True Positive Rate | 34% | > 50% | Percentual de alertas que sao incidentes reais |
| False Positive Rate | 58% | < 30% | Alertas que nao representam ameaca real |
| Detection Coverage (MITRE) | 62% | > 75% | Tecnicas ATT&CK com pelo menos 1 regra |
| Dwell Time (median) | 12 days | < 7 days | Tempo entre compromisso e deteccao |
| Alert-to-Triage Time | 18 min | < 15 min | Tempo ate inicio da triagem |

## Volume de Alertas

| Source | Daily Avg | True Positive % | Tuning Status |
|--------|-----------|-----------------|---------------|
| SIEM | 245 | 28% | In Progress |
| EDR | 52 | 45% | Tuned |
| WAF | 890 | 12% | Needs Tuning |
| Cloud Security | 38 | 62% | Tuned |
| Email Security | 127 | 71% | Tuned |

## Cobertura MITRE ATT&CK por Tatica

| Tactic | Rules Active | Coverage % |
|--------|-------------|------------|
| Initial Access | 12 | 75% |
| Execution | 18 | 68% |
| Persistence | 8 | 45% |
| Privilege Escalation | 10 | 52% |
| Defense Evasion | 6 | 32% |
| Credential Access | 14 | 70% |
| Discovery | 5 | 38% |
| Lateral Movement | 9 | 55% |
| Collection | 4 | 28% |
| Exfiltration | 7 | 48% |
| Impact | 11 | 65% |

## Metas de Melhoria

Priorizar tuning de regras com alto volume e baixo true positive rate.
Focar expansao de cobertura em Defense Evasion e Collection, que sao as
taticas com menor cobertura atual e alto impacto em deteccao de APTs.
