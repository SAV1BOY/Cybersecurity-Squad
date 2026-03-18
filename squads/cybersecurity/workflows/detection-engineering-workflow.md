# Detection Engineering Workflow

Processo estruturado para criar, testar, deployar e manter detection rules no ambiente de seguranca.

## Objetivo

Garantir que cada detection rule seja baseada em inteligencia de ameacas, testada contra dados reais, e mantida ao longo do tempo para evitar alert fatigue e falsos negativos.

## Inputs

- Threat intelligence reports e IOCs relevantes
- MITRE ATT&CK techniques mapeadas ao ambiente
- Log sources disponiveis e seus schemas
- Historico de incidentes e gaps de deteccao identificados

## Stages

### 1. Detection Hypothesis

- Responsavel: **chris-sanders**
- Formular hipotese de deteccao baseada em threat intelligence
- Mapear a tecnica ATT&CK correspondente
- Documentar o comportamento esperado do adversario

### 2. Data Source Validation

- Responsavel: **chris-sanders**
- Verificar se os log sources necessarios estao disponiveis
- Validar que os campos requeridos estao sendo coletados
- Ponto de decisao: **Dados suficientes para a deteccao?**
  - Sim -> prosseguir com desenvolvimento
  - Nao -> abrir ticket para onboarding de log source

### 3. Rule Development

- Responsavel: **chris-sanders**
- Escrever a detection rule na linguagem do SIEM (Sigma, KQL, SPL)
- Incluir campos de contexto para facilitar triage
- Documentar logic e thresholds utilizados

### 4. Testing e Validation

- Responsavel: **rogue + chris-sanders**
- Executar atomic test ou simulacao da tecnica em lab
- Validar que a rule dispara corretamente (true positive)
- Testar contra dados normais para medir false positive rate
- Ponto de decisao: **False positive rate aceitavel?**
  - Sim -> aprovar para deploy
  - Nao -> refinar rule e re-testar

### 5. Peer Review

- Responsavel: **chris-sanders**
- Revisar logica, performance e cobertura da rule
- Validar que a documentacao esta completa
- Aprovar ou solicitar mudancas

### 6. Deployment

- Responsavel: **chris-sanders**
- Deployar rule em ambiente de producao
- Configurar severity e notification routing
- Ativar em modo de observacao por periodo definido

### 7. Tuning e Manutencao

- Responsavel: **chris-sanders**
- Monitorar metricas de disparo (true/false positive rates)
- Ajustar thresholds e exclusions conforme necessario
- Revisar periodicamente contra novas threat intelligence

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Log source ausente | Dados criticos nao coletados | Priorizar onboarding antes de deployar rule |
| Alta taxa de false positives | FP rate > 20% | Retornar ao development para tuning |
| Tecnica deprecada | ATT&CK technique reclassificada | Revisar e atualizar ou aposentar rule |
| Incidente nao detectado | Gap identificado pos-incidente | Priorizar nova rule como P1 |

## Outputs

- Detection rule deployada e documentada
- Resultado de testes (true positive, false positive rates)
- Mapeamento ATT&CK atualizado com cobertura
- Runbook de triage associado a rule

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
