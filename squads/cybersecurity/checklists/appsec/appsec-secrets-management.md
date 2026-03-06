# AppSec - Secrets Management

Checklist para gestao de segredos em aplicacoes.

## Inventario de Secrets
- [ ] Todos os tipos de secrets catalogados (API keys, passwords, certs, tokens)
- [ ] Owners de cada secret identificados
- [ ] Sistemas que consomem cada secret mapeados
- [ ] Classification de cada secret por criticidade
- [ ] Secrets em uso vs deprecated identificados
- [ ] Lifecycle de cada secret documentado (creation, rotation, revocation)

## Armazenamento Seguro
- [ ] Secrets centralizados em vault (HashiCorp Vault, AWS Secrets Manager)
- [ ] Nenhum secret hardcoded em source code
- [ ] Nenhum secret em configuration files do repositorio
- [ ] Nenhum secret em environment variables nao protegidas
- [ ] Nenhum secret em CI/CD pipeline logs
- [ ] Nenhum secret em container images ou Dockerfiles
- [ ] Nenhum secret em wikis, Confluence, ou documentacao
- [ ] Encryption at rest para secrets storage verificada

## Deteccao de Vazamento
- [ ] Pre-commit hooks para secret detection habilitados (gitleaks, detect-secrets)
- [ ] CI/CD pipeline scanning para secrets implementado
- [ ] Git history scanning executado periodicamente
- [ ] Public repository monitoring configurado (GitHub alerts)
- [ ] Alerting para secret exposure configurado
- [ ] Incident response process para leaked secrets definido
- [ ] Past leaks investigados e remediados

## Rotacao e Lifecycle
- [ ] Rotation policy definida por tipo de secret
- [ ] Automated rotation implementada onde possivel
- [ ] Manual rotation process documentado para secrets nao automatizaveis
- [ ] Rotation testing realizado (funcionalidade apos rotacao)
- [ ] Emergency rotation process definido para compromised secrets
- [ ] Old secrets revoked apos rotacao
- [ ] Rotation audit trail mantido

## Access Control
- [ ] Least privilege para acesso a secrets enforced
- [ ] Access logs para secret retrieval habilitados
- [ ] Service-specific credentials (nao shared entre apps)
- [ ] Dynamic secrets utilizados onde possivel
- [ ] Short-lived credentials preferidos
- [ ] Human vs machine access diferenciado

## Monitoramento e Auditoria
- [ ] Secret access patterns monitorados para anomalias
- [ ] Unused secrets identificados e removidos
- [ ] Compliance com rotation policy verificada periodicamente
- [ ] Secret management audit realizado semestralmente
- [ ] Metricas de secrets management reportadas (age, rotation compliance)
- [ ] Report de audit entregue com findings e recommendations
