# Security Metrics Reporting Workflow

Processo para coletar, analisar e reportar metricas de seguranca de forma consistente e acionavel.

## Objetivo

Fornecer visibilidade sobre o desempenho do programa de seguranca atraves de metricas objetivas, permitindo decisoes baseadas em dados e demonstrando valor para stakeholders.

## Inputs

- Fontes de dados de seguranca (SIEM, vuln scanner, ticketing, IR tracker)
- Definicao de KPIs e metas aprovados
- Template de relatorio padronizado
- Periodo de reporting definido

## Stages

### 1. Metric Definition

- Responsavel: **shannon-runner**
- Definir ou revisar KPIs alinhados aos objetivos do programa
- Categorizar metricas: operational, tactical, strategic
- Definir fonte de dados, formula de calculo e frequencia para cada metrica

### 2. Data Collection

- Responsavel: **cartographer**
- Extrair dados de cada fonte conforme definicao
- Validar integridade e completude dos dados
- Ponto de decisao: **Dados completos e confiaveis?**
  - Sim -> prosseguir com analise
  - Nao -> investigar gaps e documentar limitacoes

### 3. Data Analysis

- Responsavel: **shannon-runner**
- Calcular cada KPI conforme formula definida
- Comparar com periodos anteriores para identificar tendencias
- Identificar outliers e anomalias que requerem investigacao

### 4. Contextualization

- Responsavel: **shannon-runner**
- Adicionar contexto qualitativo aos numeros
- Correlacionar metricas com eventos conhecidos (incidentes, projetos, mudancas)
- Ponto de decisao: **Metrica fora do threshold?**
  - Sim -> investigar root cause e documentar
  - Nao -> registrar como within expected range

### 5. Visualization

- Responsavel: **shannon-runner**
- Criar ou atualizar dashboards com dados do periodo
- Gerar graficos de tendencia e comparativos
- Destacar metricas que requerem atencao da lideranca

### 6. Report Generation

- Responsavel: **shannon-runner**
- Compilar relatorio seguindo template padronizado
- Incluir executive summary com insights principais
- Adicionar recomendacoes baseadas nos dados

### 7. Review e Distribution

- Responsavel: **cyber-chief**
- Revisar relatorio antes da distribuicao
- Validar que narrativa esta alinhada com contexto organizacional
- Distribuir para audiencias apropriadas (operacional, tatico, executivo)

### 8. Feedback e Refinement

- Responsavel: **shannon-runner**
- Coletar feedback dos consumidores do relatorio
- Ajustar metricas e formato conforme necessidade
- Atualizar definicoes de KPIs para o proximo ciclo

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| KPI em declinio consistente | Tendencia negativa por 3+ periodos | Acionar plano de melhoria |
| Fonte de dados indisponivel | Sistema fora ou dados corrompidos | Documentar gap e usar estimativa |
| Nova metrica solicitada | Stakeholder pede indicador novo | Avaliar viabilidade e adicionar ao proximo ciclo |
| Metrica sem acao | KPI coletado mas nunca utilizado | Considerar remocao para evitar overhead |

## Outputs

- Relatorio de metricas de seguranca (mensal/trimestral)
- Dashboard atualizado e acessivel
- Lista de insights e recomendacoes acionaveis
- Definicao atualizada de KPIs para proximo ciclo

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
