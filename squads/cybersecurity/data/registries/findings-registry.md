# Findings Registry

Registro centralizado de todos os findings de seguranca identificados em assessments, pentests e auditorias.

## Schema do Registro

| Finding ID | Title | Severity | CVSS | Category | Asset | Status | Discovered | Assignee | SLA Date |
|------------|-------|----------|------|----------|-------|--------|------------|----------|----------|
| FIND-2026-001 | SQL Injection em /api/users | Critical | 9.8 | Injection | app-prod-01 | Open | 2026-01-15 | @appsec-team | 2026-01-22 |
| FIND-2026-002 | TLS 1.0 habilitado | Medium | 5.3 | Cryptography | lb-prod-03 | Remediated | 2026-01-18 | @infra-team | 2026-02-18 |
| FIND-2026-003 | S3 Bucket publico | High | 7.5 | Cloud Misconfiguration | s3://data-backup | In Progress | 2026-02-01 | @cloud-team | 2026-02-15 |
| FIND-2026-004 | Hardcoded API Key | High | 7.2 | Secrets Management | repo:backend-api | Accepted Risk | 2026-02-10 | @dev-team | 2026-03-10 |

## Status Validos

- **Open**: Finding identificado, aguardando triagem
- **In Progress**: Remediacao em andamento
- **Remediated**: Correcao aplicada, aguardando validacao
- **Validated**: Correcao confirmada via retest
- **Accepted Risk**: Risco aceito formalmente com justificativa
- **False Positive**: Confirmado como falso positivo

## Campos Obrigatorios

Cada finding deve conter no minimo: ID unico, titulo descritivo, severidade calculada via CVSS,
categoria conforme vulnerability taxonomy, asset afetado e data de descoberta.

## SLA por Severidade

| Severity | SLA Remediacao |
|----------|---------------|
| Critical | 7 dias |
| High | 30 dias |
| Medium | 90 dias |
| Low | 180 dias |
| Informational | Best effort |

## Notas de Uso

Findings duplicados devem referenciar o finding original. Ao fechar um finding, registrar
evidencia de remediacao e data de validacao. Revisoes mensais garantem que nenhum finding
fique sem acompanhamento alem do SLA definido.
