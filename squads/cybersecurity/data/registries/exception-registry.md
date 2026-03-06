# Exception Registry

Registro de todas as excecoes de seguranca aprovadas, incluindo justificativa e prazo de validade.

## Schema do Registro

| Exception ID | Policy/Control | Justification | Requestor | Approver | Risk Level | Start Date | Expiry Date | Status |
|-------------|----------------|---------------|-----------|----------|------------|------------|-------------|--------|
| EXC-2026-001 | Password Policy - MFA | Legacy system incompativel com MFA | @legacy-team | @ciso | High | 2026-01-01 | 2026-06-30 | Active |
| EXC-2026-002 | Encryption at Rest | Performance degradation em batch processing | @data-team | @security-lead | Medium | 2026-02-01 | 2026-04-30 | Active |
| EXC-2026-003 | Network Segmentation | Integracao temporaria entre ambientes | @devops | @ciso | High | 2026-01-15 | 2026-03-15 | Expired |

## Status Validos

- **Requested**: Excecao solicitada, aguardando avaliacao
- **Active**: Aprovada e dentro do prazo de validade
- **Expired**: Prazo expirado, requer renovacao ou remediacao
- **Renewed**: Renovada com nova data de expiracao
- **Revoked**: Cancelada antes do prazo por mudanca de risco
- **Remediated**: Controle compensatorio implementado

## Criterios de Aprovacao

Excecoes de risco High ou Critical requerem aprovacao do CISO.
Medium pode ser aprovada pelo security lead. Low pelo security analyst senior.

## Controles Compensatorios

Toda excecao deve listar controles compensatorios implementados para mitigar
o risco durante o periodo de excecao. Exemplo: monitoramento adicional,
restricao de acesso, logging aprimorado.

## Renovacao

Excecoes podem ser renovadas por no maximo 2 ciclos. Apos isso, requerem
plano de remediacao definitivo com timeline aprovada pela lideranca.

## Auditoria

Excecoes ativas sao revisadas mensalmente. Expiradas sem renovacao geram
alerta automatico ao owner e ao approver original.
