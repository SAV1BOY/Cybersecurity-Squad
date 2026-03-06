# Task: Security Metrics Reporting

## Objetivo
Gerar e publicar relatorios de metricas de seguranca periodicos, fornecendo visibilidade sobre KPIs, trends e postura de seguranca para stakeholders.

## Agents
- **cyber-chief** (lead) — Consolida e apresenta metricas
- **marcus-carey** (support) — Contextualiza metricas com narrativa

## Inputs
- Security KPI dashboard
- Dados de todos os registries (findings, detection, remediation, incidents)
- Targets e SLOs definidos
- Templates de reporting

## Steps
1. Coletar metricas de todas as fontes de dados do squad
2. Calcular KPIs do periodo (MTTD, MTTR, vuln SLA compliance)
3. Comparar KPIs com targets e SLOs definidos
4. Gerar visualizacoes (graficos, heatmaps, trend lines)
5. Identificar desvios significativos e outliers
6. Contextualizar metricas com narrativa explicativa
7. Destacar top wins e areas de atencao
8. Gerar relatorio para audiencia executiva e operacional
9. Publicar dashboard atualizado
10. Registrar no `security-kpis`

## Output
- Relatorio de metricas periodico com visualizacoes
- Dashboard de KPIs atualizado
- Narrativa contextual para metricas-chave
- Registro no `security-kpis`

## Quality Gates
- [ ] KPIs calculados com dados de todas as fontes
- [ ] Comparacao com targets e SLOs documentada
- [ ] Visualizacoes claras e informativas
- [ ] Desvios significativos destacados e explicados
- [ ] Relatorio adequado para audiencia executiva
- [ ] Dashboard publicado e acessivel
