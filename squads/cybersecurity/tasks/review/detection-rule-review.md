# Task: Detection Rule Review

## Objetivo
Revisar regras de deteccao antes de deploy em producao, validando logica, performance, false positive rate e documentacao associada.

## Agents
- **chris-sanders** (lead) — Revisa logica e qualidade de deteccao
- **shannon-runner** (executor) — Valida anomaly detection

## Inputs
- Regras de deteccao para review
- Resultados de backtesting e emulacao
- Detection rule template padrao
- Metricas de performance de regras similares

## Steps
1. Verificar que regra segue o detection rule template padrao
2. Revisar logica de deteccao (query, correlation, threshold)
3. Validar que backtesting foi executado com resultados documentados
4. Verificar false positive rate contra threshold aceitavel
5. Confirmar que data sources necessarios estao disponiveis
6. Validar que playbook de resposta esta associado
7. Verificar performance impact no SIEM (resource consumption)
8. Confirmar mapeamento contra MITRE ATT&CK
9. Aprovar ou devolver para ajustes
10. Registrar no `detection-rules-registry`

## Output
- Regras aprovadas para deploy em producao
- Feedback para ajustes (se necessario)
- Registro de review no `detection-rules-registry`

## Quality Gates
- [ ] Regra segue template padrao com documentacao completa
- [ ] Backtesting executado com resultados aceitaveis
- [ ] False positive rate dentro de threshold
- [ ] Playbook de resposta associado e documentado
- [ ] Mapeamento ATT&CK correto e completo
- [ ] Checklist `detection-engineering-quality` atendido
- [ ] Checklist `blueteam-tuning-checklist` validado

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | detection-coverage-matrix |
| Checklists | detection-engineering-quality, blue-team/blueteam-tuning-checklist |
| Templates | runbooks/detection-rule-template |
| Registry | data/registries/detection-rules-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: detection-rule-development
- **Delivers to**: SOC deployment
