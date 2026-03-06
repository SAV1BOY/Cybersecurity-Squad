# Incident Registry

Registro formal de todos os incidentes de seguranca, desde a deteccao ate o encerramento.

## Schema do Registro

| Incident ID | Title | Severity | Category | Status | Detected | Contained | Resolved | Lead | Impact |
|-------------|-------|----------|----------|--------|----------|-----------|----------|------|--------|
| INC-2026-001 | Phishing campaign targeting finance | Medium | Phishing | Closed | 2026-01-10 | 2026-01-10 | 2026-01-12 | @ir-lead | 3 users compromised |
| INC-2026-002 | Unauthorized access to staging DB | High | Unauthorized Access | Closed | 2026-01-25 | 2026-01-25 | 2026-01-28 | @soc-lead | Data exposure risk |
| INC-2026-003 | Ransomware attempt on endpoint | Critical | Malware | Post-Incident | 2026-02-05 | 2026-02-05 | 2026-02-08 | @ir-lead | 1 host isolated |

## Classificacao de Severidade

- **Critical**: Impacto em producao, dados sensíveis comprometidos, ou ameaca ativa
- **High**: Potencial de impacto significativo, contencao urgente necessaria
- **Medium**: Impacto limitado, sem comprometimento de dados sensiveis
- **Low**: Evento suspeito sem impacto confirmado

## Status do Incidente

- **Detected**: Alerta triado e confirmado como incidente
- **Investigating**: Analise de escopo e impacto em andamento
- **Contained**: Ameaca contida, sem propagacao ativa
- **Eradicating**: Remocao de artefatos maliciosos
- **Recovering**: Restauracao de servicos e sistemas
- **Post-Incident**: Review e lessons learned em andamento
- **Closed**: Incidente encerrado com documentacao completa

## Metricas Rastreadas

- Mean Time to Detect (MTTD)
- Mean Time to Contain (MTTC)
- Mean Time to Resolve (MTTR)
- Incidentes por categoria e severidade

## Requisitos de Documentacao

Cada incidente encerrado deve ter: timeline detalhada, root cause analysis,
lista de IOCs identificados, acoes de remediacao e recomendacoes preventivas.
