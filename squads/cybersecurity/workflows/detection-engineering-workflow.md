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

- Responsavel: **Detection Engineer Agent**
- Formular hipotese de deteccao baseada em threat intelligence
- Mapear a tecnica ATT&CK correspondente
- Documentar o comportamento esperado do adversario

### 2. Data Source Validation

- Responsavel: **Data Engineer Agent**
- Verificar se os log sources necessarios estao disponiveis
- Validar que os campos requeridos estao sendo coletados
- Ponto de decisao: **Dados suficientes para a deteccao?**
  - Sim -> prosseguir com desenvolvimento
  - Nao -> abrir ticket para onboarding de log source

### 3. Rule Development

- Responsavel: **Detection Engineer Agent**
- Escrever a detection rule na linguagem do SIEM (Sigma, KQL, SPL)
- Incluir campos de contexto para facilitar triage
- Documentar logic e thresholds utilizados

### 4. Testing e Validation

- Responsavel: **Purple Team Agent**
- Executar atomic test ou simulacao da tecnica em lab
- Validar que a rule dispara corretamente (true positive)
- Testar contra dados normais para medir false positive rate
- Ponto de decisao: **False positive rate aceitavel?**
  - Sim -> aprovar para deploy
  - Nao -> refinar rule e re-testar

### 5. Peer Review

- Responsavel: **Senior Detection Engineer Agent**
- Revisar logica, performance e cobertura da rule
- Validar que a documentacao esta completa
- Aprovar ou solicitar mudancas

### 6. Deployment

- Responsavel: **Detection Ops Agent**
- Deployar rule em ambiente de producao
- Configurar severity e notification routing
- Ativar em modo de observacao por periodo definido

### 7. Tuning e Manutencao

- Responsavel: **Detection Engineer Agent**
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
