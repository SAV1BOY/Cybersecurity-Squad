# Task: Detection Coverage Mapping

## Objetivo
Mapear a cobertura de deteccao atual contra o framework MITRE ATT&CK, identificando tecnicas com e sem deteccao ativa para priorizar desenvolvimento de regras.

## Agents
- **chris-sanders** (lead) — Mapeia cobertura de deteccao
- **omar-santos** (support) — Valida cobertura em cloud e infraestrutura
- **shannon-runner** (executor) — Analisa entropia e anomalias

## Inputs
- Regras de deteccao existentes (SIEM, EDR, IDS)
- MITRE ATT&CK matrix como referencia
- Fontes de log disponiveis
- Detection coverage matrix atual

## Steps
1. Inventariar todas as regras de deteccao ativas
2. Mapear cada regra contra MITRE ATT&CK techniques
3. Identificar ATT&CK techniques sem cobertura de deteccao
4. Classificar gaps por prioridade (baseado em threat landscape)
5. Avaliar qualidade das deteccoes existentes (precision, recall)
6. Identificar data sources necessarios para fechar gaps
7. Priorizar desenvolvimento de novas regras por impacto
8. Atualizar detection coverage tracker com status atual
9. Gerar heatmap de cobertura ATT&CK
10. Registrar no `detection-rules-registry`

## Output
- Heatmap de cobertura MITRE ATT&CK
- Lista de gaps priorizados por relevancia ao threat landscape
- Plano de desenvolvimento de regras priorizadas
- Detection coverage tracker atualizado

## Quality Gates
- [ ] Todas as regras de deteccao inventariadas e mapeadas
- [ ] Cobertura ATT&CK calculada por tactic e technique
- [ ] Gaps priorizados por relevancia ao threat landscape
- [ ] Data sources necessarios identificados para fechar gaps
- [ ] Checklist `blueteam-detection-coverage` atendido
- [ ] Checklist `detection-engineering-quality` validado

## Routing & Escalation
- **frameworks**: detection-coverage-matrix, mitre-att-ck, mitre-d3fend
- **checklists**: blue-team/blueteam-detection-coverage, detection-engineering-quality
- **templates**: trackers/detection-coverage-tracker
- **registry**: data/registries/detection-rules-registry
- **receives_from**: logging-and-visibility-gap-audit
- **delivers_to**: detection-rule-development
