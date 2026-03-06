# Threat Hunting Sprint Workflow

Processo estruturado para conduzir sprints de threat hunting proativos e baseados em hipoteses.

## Objetivo

Identificar ameacas que escaparam dos controles de deteccao existentes, utilizando uma abordagem proativa e hipotetica para descobrir atividade maliciosa no ambiente.

## Inputs

- Threat intelligence atualizada e relevante ao setor
- Hipoteses de hunting derivadas de gaps de deteccao
- Acesso a log sources e ferramentas de query
- MITRE ATT&CK navigator com cobertura atual

## Stages

### 1. Sprint Planning

- Responsavel: **Hunt Lead Agent**
- Selecionar hipoteses para o sprint com base em threat intel
- Definir escopo temporal e de dados para cada hunt
- Alocar hunters e definir timebox por hipotese

### 2. Hypothesis Formulation

- Responsavel: **Threat Hunter Agent**
- Estruturar hipotese no formato: "Se o adversario usou [tecnica], entao devemos observar [indicador] em [data source]"
- Mapear a hipotese ao ATT&CK framework
- Definir criterios de sucesso e metricas de cobertura

### 3. Data Collection e Exploration

- Responsavel: **Threat Hunter Agent**
- Identificar e acessar data sources relevantes
- Executar queries exploratarias para entender baseline
- Ponto de decisao: **Dados suficientes para testar hipotese?**
  - Sim -> prosseguir com analise
  - Nao -> documentar gap e solicitar onboarding de data source

### 4. Analysis e Investigation

- Responsavel: **Threat Hunter Agent**
- Executar queries analiticas para testar a hipotese
- Investigar anomalias e outliers identificados
- Ponto de decisao: **Atividade suspeita encontrada?**
  - Sim -> escalar para incident response se necessario
  - Nao -> documentar como hipotese testada sem findings

### 5. Finding Documentation

- Responsavel: **Threat Hunter Agent**
- Documentar todas as descobertas com evidencias
- Classificar findings como confirmed threat, suspicious activity ou informational
- Recomendar novas detection rules baseadas nos resultados

### 6. Detection Rule Creation

- Responsavel: **Detection Engineer Agent**
- Converter findings em detection rules automatizadas
- Testar rules conforme o detection engineering workflow
- Deployar para prevenir recorrencia

### 7. Sprint Retrospective

- Responsavel: **Hunt Lead Agent**
- Revisar metricas do sprint (hipoteses testadas, findings, rules criadas)
- Coletar feedback dos hunters sobre tooling e data quality
- Priorizar hipoteses para o proximo sprint

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Ameaca ativa confirmada | Evidencia de comprometimento | Escalar imediatamente para IR |
| Data source insuficiente | Logs nao coletados | Registrar gap e buscar fontes alternativas |
| Hipotese inconclusiva | Dados ambiguos | Refinar hipotese para proximo sprint |
| Hunt excede timebox | Tempo esgotado sem conclusao | Pausar e re-priorizar no sprint planning |

## Outputs

- Relatorio de sprint com hipoteses testadas e resultados
- Novas detection rules criadas ou propostas
- Lista de gaps de visibilidade identificados
- Hipoteses priorizadas para proximo sprint
