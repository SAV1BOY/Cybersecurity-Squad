# Task: Purple Team Exercise

## Objetivo
Conduzir exercicio colaborativo Purple Team onde Red Team executa tecnicas e Blue Team valida deteccao em tempo real, fechando gaps de cobertura de forma iterativa.

## Agents
- **rogue** (lead) — Executa tecnicas adversarias
- **chris-sanders** (support) — Valida deteccao em tempo real
- **peter-kim** (support) — Direciona attack paths para teste

## Inputs
- Detection coverage map com gaps identificados
- MITRE ATT&CK techniques selecionadas para teste
- Regras de deteccao existentes
- ROE para exercicio Purple Team

## Steps
1. Selecionar ATT&CK techniques para testar (priorizadas por gap)
2. Preparar environment de teste com deconfliction protocol
3. Red Team executa technique com logging detalhado
4. Blue Team verifica se deteccao trigou em tempo real
5. Se nao detectado: analisar gap e desenvolver regra on-the-spot
6. Re-executar technique para validar nova deteccao
7. Documentar resultado por technique (detected/not detected/partial)
8. Iterar para proxima technique do backlog
9. Consolidar resultados e atualizar detection coverage map
10. Registrar no `findings-registry` e `detection-rules-registry`

## Output
- Relatorio de Purple Team com resultados por technique
- Novas regras de deteccao desenvolvidas durante exercicio
- Detection coverage map atualizado
- Gap closure metrics (antes vs depois)

## Quality Gates
- [ ] Deconfliction protocol ativo durante exercicio
- [ ] Cada technique documentada com resultado (detected/not/partial)
- [ ] Gaps identificados geraram novas regras de deteccao
- [ ] Detection coverage map atualizado pos-exercicio
- [ ] Checklist `purple-team-exercise-quality` atendido
- [ ] Checklist `redteam-deconfliction-checklist` validado

## Routing & Escalation
- **frameworks**: purple-team-method, mitre-att-ck
- **checklists**: purple-team-exercise-quality, red-team/redteam-deconfliction-checklist
- **templates**: reports/technical-report-template
- **registry**: data/registries/findings-registry, data/registries/detection-rules-registry
- **receives_from**: detection gaps identified
- **delivers_to**: detection-rule-development
