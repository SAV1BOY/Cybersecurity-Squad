# Task: IAM Least Privilege Project

## Objetivo
Implementar o principio de least privilege em todas as contas e roles de IAM cloud, reduzindo excessive permissions e eliminando overprivileged identities.

## Agents
- **omar-santos** (lead) — Conduz projeto de IAM least privilege
- **cyber-chief** (support) — Alinha com governanca e priorizacao

## Inputs
- Identity e privilege mapping (discovery)
- IAM policies atuais (AWS IAM, Azure AD, GCP IAM)
- Cloud asset inventory
- Logs de acesso e usage analytics

## Steps
1. Inventariar todas as IAM policies, roles e permissions
2. Analisar usage logs para identificar permissions nao utilizadas
3. Identificar overprivileged users, roles e service accounts
4. Mapear cross-account e cross-project access
5. Definir baseline de least privilege por role/funcao
6. Criar plano de remediacao com rollback strategy
7. Implementar permission boundaries e SCPs
8. Remover permissions nao utilizadas de forma incremental
9. Configurar alertas para privilege escalation attempts
10. Registrar findings e remediacao nos registries

## Output
- Inventario de IAM com analysis de overprivilege
- Plano de remediacao com timeline e rollback
- Permission boundaries e SCPs implementados
- Registro no `findings-registry` e `remediation-registry`

## Quality Gates
- [ ] Todas as IAM policies inventariadas e analisadas
- [ ] Usage logs consultados para validar permissions ativas
- [ ] Overprivileged identities identificadas e documentadas
- [ ] Plano de remediacao inclui rollback strategy
- [ ] Permission boundaries implementados
- [ ] Checklist `cloud-iam-least-privilege` 100% atendido
- [ ] Checklist `cloud-security-assessment-quality` validado
