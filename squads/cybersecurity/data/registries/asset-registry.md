# Asset Registry

Inventario de ativos criticos sob escopo de seguranca, incluindo classificacao e ownership.

## Schema do Registro

| Asset ID | Name | Type | Environment | Criticality | Owner | Data Classification | Last Scanned | Compliance Scope |
|----------|------|------|-------------|-------------|-------|--------------------|--------------|-----------------
| AST-001 | app-prod-api | Application | Production | Critical | @backend-team | Confidential | 2026-02-28 | PCI-DSS, LGPD |
| AST-002 | db-prod-primary | Database | Production | Critical | @dba-team | Restricted | 2026-02-28 | PCI-DSS, LGPD |
| AST-003 | cdn-static | Infrastructure | Production | Medium | @infra-team | Public | 2026-02-15 | - |
| AST-004 | admin-portal | Application | Production | High | @platform-team | Internal | 2026-02-20 | SOC2 |
| AST-005 | k8s-staging | Infrastructure | Staging | Low | @devops-team | Internal | 2026-01-30 | - |

## Tipos de Ativo

- **Application**: Aplicacoes web, APIs, mobile apps
- **Database**: Bancos de dados relacionais e NoSQL
- **Infrastructure**: Servidores, containers, networking
- **Endpoint**: Workstations, laptops corporativos
- **Cloud Resource**: Servicos cloud (S3, Lambda, RDS)
- **Identity**: Service accounts, API keys, certificates

## Classificacao de Dados

- **Public**: Informacao publica sem restricao
- **Internal**: Uso interno, sem dados sensiveis
- **Confidential**: Dados de clientes ou negocios sensiveis
- **Restricted**: Dados regulados (PII, financeiros, saude)

## Criticidade

Baseada no impacto ao negocio em caso de comprometimento:
- **Critical**: Impacto direto em revenue ou dados regulados
- **High**: Servico essencial com impacto significativo
- **Medium**: Servico importante mas com alternativas
- **Low**: Sistemas de suporte ou desenvolvimento

## Frequencia de Scanning

Ativos Critical e High devem ser escaneados semanalmente.
Medium mensalmente. Low trimestralmente.
