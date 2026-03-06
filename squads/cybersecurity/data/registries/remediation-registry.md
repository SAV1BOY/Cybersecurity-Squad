# Remediation Registry

Registro de todas as acoes de remediacao planejadas, em andamento e concluidas.

## Schema do Registro

| Remediation ID | Finding ID | Action | Owner | Priority | Status | Start Date | Target Date | Completion Date |
|----------------|------------|--------|-------|----------|--------|------------|-------------|-----------------|
| REM-2026-001 | FIND-2026-001 | Implementar parameterized queries | @dev-team | P1 | Completed | 2026-01-16 | 2026-01-22 | 2026-01-20 |
| REM-2026-002 | FIND-2026-002 | Desabilitar TLS 1.0/1.1 no load balancer | @infra-team | P2 | In Progress | 2026-01-20 | 2026-02-18 | - |
| REM-2026-003 | FIND-2026-003 | Aplicar bucket policy restritiva | @cloud-team | P1 | Planned | - | 2026-02-15 | - |

## Status Validos

- **Planned**: Acao definida, aguardando inicio
- **In Progress**: Remediacao sendo executada
- **Completed**: Acao concluida, aguardando validacao
- **Validated**: Eficacia confirmada via retest
- **Blocked**: Impedimento identificado
- **Cancelled**: Acao cancelada com justificativa

## Processo de Validacao

Toda remediacao completada deve passar por retest executado por membro diferente
do responsavel pela correcao. O retest deve confirmar que a vulnerabilidade nao
e mais exploravel e que nenhuma regressao foi introduzida.

## Metricas de Acompanhamento

- Mean Time to Remediate (MTTR) por severidade
- Percentual de remediacoes dentro do SLA
- Taxa de remediacoes que falharam no retest
- Numero de remediacoes bloqueadas e motivos

## Escalation Path

Remediacoes que ultrapassam o SLA sao escaladas automaticamente:
1. SLA + 7 dias: Notificacao ao tech lead
2. SLA + 14 dias: Escalacao ao engineering manager
3. SLA + 30 dias: Escalacao ao CISO
