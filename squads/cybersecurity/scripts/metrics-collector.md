# Metrics Collector

Script para coletar e consolidar metricas de seguranca de multiplas fontes.

## Descricao

Conecta-se a diversas fontes de dados de seguranca, extrai metricas relevantes e consolida em formato padronizado para dashboards e relatorios.

## Inputs

- `period` - Periodo de coleta (ex: 2026-02-01 a 2026-02-28)
- `sources` - Lista de fontes a consultar (siem, vuln_scanner, ticketing, ir_tracker)
- `output_format` - Formato de saida (json, csv, dashboard)

## Fontes de Dados e Metricas

### SIEM
- Total de alertas gerados no periodo
- Alertas por severidade e categoria
- False positive rate
- Mean Time to Detect (MTTD)

### Vulnerability Scanner
- Total de vulnerabilidades por severidade
- Novas vulnerabilidades no periodo
- Vulnerabilidades remediadas no periodo
- Aging de vulnerabilidades abertas

### Ticketing System
- Findings abertos vs fechados
- SLA compliance por severidade
- Mean Time to Remediate (MTTR)
- Findings por owner/equipe

### IR Tracker
- Total de incidentes por severidade
- Mean Time to Contain (MTTC)
- Incidentes por categoria
- Postmortems concluidos vs pendentes

## Logica

1. Validar periodo e fontes informados
2. Para cada fonte configurada:
   - Autenticar via API ou credenciais armazenadas
   - Executar queries para extrair metricas do periodo
   - Validar integridade dos dados retornados
3. Normalizar dados em formato padrao
4. Calcular metricas derivadas (taxas, medias, tendencias)
5. Comparar com periodo anterior para calcular variacao
6. Gerar output no formato solicitado

## Output

Arquivo consolidado com todas as metricas coletadas, incluindo:
- Metadados (periodo, fontes, data de coleta)
- Metricas por fonte com valores e variacao
- Alertas para metricas fora de threshold
- Log de erros ou fontes indisponiveis

## Alertas Automaticos

- Metrica fora do threshold definido -> alerta para o squad lead
- Fonte de dados indisponivel -> alerta para equipe de operacoes
- Variacao maior que 50% vs periodo anterior -> alerta para investigacao
