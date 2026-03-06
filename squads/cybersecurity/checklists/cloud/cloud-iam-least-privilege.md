# Cloud - IAM Least Privilege

Checklist para auditoria de least privilege em IAM cloud.

## Inventario de Identidades
- [ ] Todas as IAM users catalogadas com ultimo acesso
- [ ] IAM roles catalogadas com trust policies
- [ ] Service accounts inventariados
- [ ] Federated identities mapeadas
- [ ] Machine identities (EC2 roles, Lambda roles) catalogadas
- [ ] Cross-account roles identificados e justificados
- [ ] Inactive identities (>90 dias sem uso) listadas

## Analise de Permissoes
- [ ] Policies com wildcard (*) actions identificadas
- [ ] Policies com wildcard (*) resources identificadas
- [ ] Admin/PowerUser policies atribuidas justificadas
- [ ] Inline policies vs managed policies analisadas
- [ ] Permission boundaries implementadas para contas privilegiadas
- [ ] Service control policies (SCPs) revisadas (AWS Organizations)
- [ ] Conditional policies verificadas (IP restriction, MFA requirement)

## User Access Review
- [ ] Cada user com permissoes justificadas pelo role/funcao
- [ ] MFA habilitado para todos os users com console access
- [ ] Access keys rotacionadas conforme policy (max 90 dias)
- [ ] Unused access keys desabilitadas
- [ ] Root account sem access keys (AWS)
- [ ] Root/global admin usage monitorado e alertado
- [ ] Password policy enforced conforme baseline

## Role e Service Account Review
- [ ] Cada role com scope minimo para sua funcao
- [ ] Service accounts com permissoes minimas necessarias
- [ ] Temporary credentials preferidas (STS, workload identity)
- [ ] Role session duration adequada (nao excessiva)
- [ ] Cross-account assume role policies restritivas
- [ ] Service account key rotation automatizada

## Automacao e Tooling
- [ ] IAM Access Analyzer habilitado (AWS)
- [ ] Azure AD Access Reviews configuradas
- [ ] GCP IAM Recommender habilitado
- [ ] Automated unused permission detection configurada
- [ ] Policy simulation testada para changes propostas
- [ ] Infrastructure as Code para IAM policies (versionado)
- [ ] Drift detection para IAM configuration implementada

## Governance
- [ ] IAM policy approval process definido
- [ ] Access review cadence definida (quarterly minimum)
- [ ] Separation of duties enforced para acoes criticas
- [ ] Break-glass procedure para emergency access definido
- [ ] IAM metrics reportadas (users with admin, unused perms)
- [ ] Remediation plan para over-permissioned identities
- [ ] Report de audit IAM entregue com findings
