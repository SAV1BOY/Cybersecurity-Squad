# Task: Logging & Visibility Gap Audit

## Objetivo
Auditar a cobertura de logging e visibilidade de seguranca, identificando gaps que impediriam a deteccao de ameacas e a resposta a incidentes.

## Agents
- **chris-sanders** (lead) — Avalia cobertura de logging e NSM
- **omar-santos** (support) — Valida visibilidade em cloud e infraestrutura

## Inputs
- Asset inventory atualizado
- Arquitetura de rede e cloud
- Lista de fontes de log existentes
- Detection coverage matrix atual

## Steps
1. Inventariar todas as fontes de log ativas (endpoints, rede, cloud, apps)
2. Mapear cobertura atual contra MITRE ATT&CK techniques
3. Identificar gaps de visibilidade por layer (network, host, app, cloud)
4. Avaliar qualidade dos logs (completude, formato, retencao)
5. Verificar centralizacao e correlacao de logs (SIEM, SOAR)
6. Auditar retencao de logs contra requisitos regulatorios
7. Identificar blind spots em segmentacao de rede
8. Avaliar cobertura de endpoint detection (EDR/XDR)
9. Documentar gaps com recomendacoes de remediacao priorizadas
10. Atualizar `detection-coverage-tracker`

## Output
- Relatorio de visibility gaps por layer e por tecnica ATT&CK
- Mapa de cobertura de logging atualizado
- Recomendacoes priorizadas para fechar gaps
- Registro no `detection-rules-registry`

## Quality Gates
- [ ] Todas as fontes de log inventariadas e classificadas
- [ ] Cobertura mapeada contra MITRE ATT&CK matrix
- [ ] Gaps de visibilidade documentados por layer
- [ ] Retencao de logs validada contra requisitos regulatorios
- [ ] Recomendacoes sao acionaveis com prioridade definida
- [ ] Checklist `blueteam-logging-coverage` atendido
- [ ] Checklist `santos-visibility-matrix` validado
