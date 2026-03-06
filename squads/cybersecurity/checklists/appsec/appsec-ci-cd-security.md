# AppSec - CI/CD Security

Checklist para seguranca de pipelines CI/CD.

## Access Control do Pipeline
- [ ] Autenticacao obrigatoria para acessar CI/CD platform
- [ ] MFA habilitado para contas de CI/CD
- [ ] RBAC implementado (quem pode criar/editar/executar pipelines)
- [ ] Branch protection rules configuradas (required reviews, status checks)
- [ ] Merge request approvals obrigatorios para branches protegidas
- [ ] Service accounts com least privilege para pipeline operations
- [ ] Audit logging de todas as acoes no CI/CD habilitado

## Pipeline Configuration Security
- [ ] Pipeline-as-code versionado no repositorio
- [ ] Pipeline configuration protegida contra modificacao nao autorizada
- [ ] Self-hosted runners hardened e isolados
- [ ] Runner images atualizados regularmente
- [ ] Ephemeral runners preferidos (destroy apos cada job)
- [ ] Network segmentation para runners implementada
- [ ] Docker-in-Docker usage minimizado e controlado

## Secrets no Pipeline
- [ ] Secrets armazenados no vault do CI/CD (nao em code)
- [ ] Secrets masked em logs automaticamente
- [ ] Secrets nao exportados para steps nao autorizados
- [ ] Secrets com scope restrito (environment-specific)
- [ ] Secret rotation policy implementada
- [ ] Nenhum secret em pipeline output/artifacts
- [ ] Secret scanning em pipeline logs habilitado

## Security Checks Integrados
- [ ] SAST executado automaticamente em cada PR/MR
- [ ] SCA/dependency scanning executado em cada build
- [ ] Secret scanning executado em cada commit
- [ ] Container image scanning executado antes do deploy
- [ ] IaC scanning executado (Terraform, CloudFormation)
- [ ] DAST executado em ambiente de staging
- [ ] License compliance check executado
- [ ] Quality gate definido com thresholds de seguranca

## Artifact Security
- [ ] Build artifacts armazenados em registry seguro
- [ ] Artifact integrity verificada (checksums, signatures)
- [ ] Artifact promotion process definido (dev -> staging -> prod)
- [ ] Old artifacts cleaned up automaticamente
- [ ] Container images tagged com immutable tags (digest)
- [ ] Artifact access control restrito por environment

## Deployment Security
- [ ] Deployment approval gates para producao
- [ ] Rollback automatico configurado para falhas
- [ ] Blue/green ou canary deployment implementado
- [ ] Post-deployment security verification automatizada
- [ ] Deployment audit trail completo
- [ ] Infrastructure drift detection pos-deployment

## Monitoramento e Resposta
- [ ] Pipeline execution monitoring configurado
- [ ] Alertas para pipeline modifications inesperadas
- [ ] Failed security checks escalados automaticamente
- [ ] Incident response para pipeline compromise definido
- [ ] Regular audit de CI/CD security realizado
