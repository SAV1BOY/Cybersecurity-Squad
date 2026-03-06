# Detection to Coverage Loop

Ciclo continuo que mede e melhora a cobertura de deteccao contra o framework MITRE ATT&CK.

## Objetivo

Manter visibilidade sobre quais tecnicas de ataque possuem deteccao ativa, identificar gaps criticos e priorizar desenvolvimento de novas rules para maximizar cobertura.

## Inputs

- MITRE ATT&CK matrix com tecnicas relevantes ao ambiente
- Inventario atual de detection rules
- Threat intelligence sobre grupos adversarios relevantes
- Resultados de purple team exercises anteriores

## Stages

### 1. Coverage Assessment

- Responsavel: **Coverage Analyst Agent**
- Mapear todas as detection rules existentes ao ATT&CK
- Calcular porcentagem de cobertura por tactic e technique
- Identificar tecnicas sem nenhuma deteccao (blind spots)

### 2. Gap Prioritization

- Responsavel: **Threat Intel Agent**
- Cruzar blind spots com threat intelligence relevante
- Priorizar tecnicas usadas por adversarios que targetam o setor
- Ponto de decisao: **Gap alinhado com ameaca ativa?**
  - Sim -> prioridade alta para desenvolvimento
  - Nao -> backlog para desenvolvimento futuro

### 3. Data Source Feasibility

- Responsavel: **Data Engineer Agent**
- Verificar se os log sources necessarios existem para cada gap
- Ponto de decisao: **Log source disponivel?**
  - Sim -> encaminhar para detection engineering
  - Nao -> criar requisicao de onboarding e compensar com hunting

### 4. Detection Development

- Responsavel: **Detection Engineer Agent**
- Desenvolver rules para os gaps priorizados
- Seguir o detection engineering workflow padrao
- Testar e validar antes do deploy

### 5. Coverage Re-Assessment

- Responsavel: **Coverage Analyst Agent**
- Recalcular metricas de cobertura apos novos deploys
- Atualizar heat map de cobertura ATT&CK
- Comparar evolucao com o assessment anterior

### 6. Reporting

- Responsavel: **Metrics Agent**
- Gerar relatorio de cobertura para stakeholders
- Incluir tendencia historica e metas para o proximo ciclo
- Destacar melhorias e gaps remanescentes

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Cobertura abaixo da meta | < 60% das tecnicas prioritarias | Alocar sprint dedicado a deteccao |
| Nova threat intelligence | Novo grupo adversario relevante | Re-priorizar gaps imediatamente |
| Log source descontinuado | Fonte de dados removida | Reavaliar rules afetadas e buscar alternativas |
| Falso senso de cobertura | Rule existe mas nao dispara | Marcar como ineffective e re-desenvolver |

## Outputs

- Heat map de cobertura ATT&CK atualizado
- Lista priorizada de gaps para o proximo sprint
- Relatorio de evolucao de cobertura
- Requisicoes de onboarding de log sources

## Loop Condition

Este ciclo se repete a cada sprint de detection engineering ou quando nova threat intelligence significativa e recebida. Meta minima de revisao: mensal.
