# Task: Detection Rule Development

## Objetivo
Desenvolver, testar e implementar novas regras de deteccao para fechar gaps identificados no coverage mapping, garantindo precisao e minimo de falsos positivos.

## Agents
- **chris-sanders** (lead) — Desenvolve e valida regras
- **shannon-runner** (executor) — Testa anomaly detection
- **command-generator** (support) — Gera queries e comandos

## Inputs
- Lista de gaps priorizados (detection-coverage-mapping)
- Data sources disponiveis
- Threat intelligence relevante
- Detection rule template padrao

## Steps
1. Selecionar techniques prioritarias do gap analysis
2. Pesquisar TTPs e indicadores para cada technique
3. Desenvolver logica de deteccao (query, correlation, threshold)
4. Implementar regra no formato padrao (Sigma, SIEM-specific)
5. Testar regra contra dados historicos (backtesting)
6. Simular true positives com ATT&CK emulation
7. Medir false positive rate e tunar thresholds
8. Documentar regra com playbook de resposta associado
9. Deploy em producao com monitoramento de performance
10. Registrar no `detection-rules-registry`

## Output
- Regras de deteccao implementadas e testadas
- Documentacao por regra com playbook de resposta
- Metricas de performance (FP rate, detection rate)
- Registro no `detection-rules-registry`

## Quality Gates
- [ ] Regra testada contra dados historicos (backtesting)
- [ ] True positives validados com emulacao ATT&CK
- [ ] False positive rate dentro de threshold aceitavel
- [ ] Playbook de resposta associado a cada regra
- [ ] Performance monitorada apos deploy em producao
- [ ] Checklist `detection-engineering-quality` atendido
- [ ] Checklist `blueteam-tuning-checklist` validado

## Routing & Escalation
- **frameworks**: defense-layer, detection-coverage-matrix
- **checklists**: detection-engineering-quality, blue-team/blueteam-tuning-checklist
- **templates**: runbooks/detection-rule-template
- **registry**: data/registries/detection-rules-registry
- **receives_from**: detection-coverage-mapping
- **delivers_to**: detection-rule-review
