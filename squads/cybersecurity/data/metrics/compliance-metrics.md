# Compliance Metrics

Metricas de conformidade com frameworks regulatorios e standards de seguranca.

## Status por Framework

| Framework | Total Controls | Compliant | Partial | Non-Compliant | Score |
|-----------|---------------|-----------|---------|---------------|-------|
| SOC 2 Type II | 64 | 58 | 4 | 2 | 91% |
| PCI-DSS v4.0 | 78 | 68 | 7 | 3 | 87% |
| LGPD | 45 | 40 | 3 | 2 | 89% |
| ISO 27001 | 114 | 95 | 12 | 7 | 83% |
| NIST CSF | 108 | 88 | 14 | 6 | 81% |
| CIS Controls v8 | 153 | 118 | 22 | 13 | 77% |

## Tendencia de Conformidade

| Framework | Q3 2025 | Q4 2025 | Q1 2026 | Trend |
|-----------|---------|---------|---------|-------|
| SOC 2 | 85% | 88% | 91% | Up |
| PCI-DSS | 82% | 84% | 87% | Up |
| LGPD | 80% | 85% | 89% | Up |
| ISO 27001 | 75% | 79% | 83% | Up |

## Controles com Gap Critico

| Control | Framework | Gap Description | Owner | Target Date |
|---------|-----------|-----------------|-------|-------------|
| Access Review | SOC 2 CC6.1 | Reviews nao realizados trimestralmente | @iam-team | 2026-03-31 |
| Encryption at Rest | PCI-DSS 3.4 | Dados de cartao sem criptografia em legacy DB | @dba-team | 2026-04-30 |
| Data Retention | LGPD Art.15 | Politica de retencao nao implementada | @data-team | 2026-03-31 |

## Auditorias Agendadas

| Audit | Type | Date | Auditor | Status |
|-------|------|------|---------|--------|
| SOC 2 Type II | External | 2026-06-01 | Deloitte | Preparando |
| PCI-DSS | External | 2026-09-01 | QSA Partner | Planejado |
| ISO 27001 Surveillance | External | 2026-04-15 | BSI | Agendado |
| Internal Security Audit | Internal | 2026-03-15 | @audit-team | Em andamento |

## Meta

Atingir e manter 90%+ de conformidade em todos os frameworks aplicaveis.
