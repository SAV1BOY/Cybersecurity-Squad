# Task: Identity & Privilege Mapping

## Objetivo
Mapear identidades, privilegios e acessos nos sistemas in-scope, identificando excessive permissions, shadow admins e violacoes do principio de least privilege.

## Agents
- **cartographer** (lead) — Mapeia identidades e acessos
- **omar-santos** (support) — Valida IAM em cloud e infraestrutura

## Inputs
- Asset inventory atualizado
- Diretorio de identidades (Active Directory, IdP, IAM)
- Politicas de acesso existentes

## Steps
1. Enumerar todas as identidades (usuarios, service accounts, roles)
2. Mapear group memberships e role assignments
3. Identificar privileged accounts (domain admins, root, cloud admins)
4. Detectar shadow admins e delegacoes excessivas
5. Auditar service accounts quanto a overprivileged permissions
6. Mapear cross-account e cross-tenant access (cloud)
7. Verificar MFA enforcement em contas privilegiadas
8. Identificar stale accounts e orphaned permissions
9. Documentar findings com recomendacoes de least privilege
10. Registrar no `asset-registry`

## Output
- Mapa de identidades e privilegios por sistema
- Lista de shadow admins e excessive permissions
- Relatorio de stale accounts e orphaned permissions
- Recomendacoes de least privilege por ativo

## Quality Gates
- [ ] Todas as identidades privilegiadas identificadas e catalogadas
- [ ] Shadow admins detectados e reportados
- [ ] Service accounts auditadas quanto a overprivilege
- [ ] MFA enforcement verificado em contas privilegiadas
- [ ] Stale accounts e orphaned permissions listados
- [ ] Checklist `identity-and-ad-assessment-quality` atendido
- [ ] Checklist `cloud-iam-least-privilege` validado
