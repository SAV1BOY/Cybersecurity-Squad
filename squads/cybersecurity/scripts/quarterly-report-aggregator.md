# Quarterly Report Aggregator

Script para consolidar dados de multiplas fontes e gerar o relatorio trimestral de seguranca.

## Descricao

Agrega metricas, findings, incidentes e atividades do trimestre em um relatorio executivo padronizado, pronto para apresentacao na quarterly security operating review.

## Inputs

- `quarter` - Trimestre de referencia (ex: Q1-2026)
- `metrics_files` - Arquivos mensais de metricas coletadas
- `incident_reports` - Relatorios de incidentes do periodo
- `engagement_reports` - Relatorios de pentests e reviews do periodo
- `previous_quarter` - Dados do trimestre anterior para comparacao

## Logica

1. Validar que todos os inputs estao disponiveis e completos
2. Agregar metricas mensais em visao trimestral:
   - Calcular medias, totais e tendencias
   - Identificar melhorias e deterioracoes
3. Sumarizar incidentes do trimestre:
   - Total por severidade e categoria
   - Destaques e lessons learned principais
4. Sumarizar engagements:
   - Pentests e reviews conduzidos
   - Findings totais por severidade
   - Taxa de remediacao
5. Comparar com trimestre anterior
6. Gerar secoes do relatorio automaticamente
7. Inserir graficos e visualizacoes

## Secoes Geradas

### Executive Summary
- Resumo da postura de seguranca do trimestre
- Destaques positivos e areas de preocupacao
- Recomendacoes estrategicas

### Metricas Operacionais
- MTTD, MTTR, MTTC com tendencia
- SLA compliance por severidade
- Cobertura de deteccao ATT&CK

### Incidentes
- Resumo por tipo e severidade
- Casos notaveis e impacto
- Status de action items de postmortems

### Avaliacao de Seguranca
- Engagements conduzidos e resultados
- Vulnerabilidades identificadas vs remediadas
- Tendencia do risco organizacional

### Programa e Equipe
- Headcount e capacidade
- Projetos e iniciativas em andamento
- Treinamentos e certificacoes

### Proximo Trimestre
- OKRs propostos
- Projetos planejados
- Recursos necessarios

## Output

```
Quarterly Security Report - Q1 2026
Gerado em: 2026-03-06

Secoes: 6
Paginas estimadas: 15-20
Graficos: 8
Tabelas: 12

Arquivo: quarterly-report-Q1-2026-draft.md
```

## Uso

```
quarterly-report-aggregator --quarter Q1-2026 --metrics ./metrics/ --incidents ./incidents/ --engagements ./engagements/
```

## Observacoes

- O relatorio gerado e um draft que requer revisao humana
- Narrativa e insights devem ser adicionados pelo security operations lead
- Dados sensiveis devem ser sanitizados antes da distribuicao executiva
