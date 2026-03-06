# Task: Storage Exposure Audit

## Objetivo
Auditar servicos de cloud storage (S3, Azure Blob, GCS) quanto a exposicao publica, misconfiguracao de permissoes e dados sensiveis acessiveis sem autorizacao.

## Agents
- **omar-santos** (lead) — Conduz auditoria de storage
- **cartographer** (support) — Mapeia storage assets

## Inputs
- Cloud asset inventory
- Politicas de storage existentes
- Classificacao de dados da organizacao
- ROE com escopo de cloud

## Steps
1. Inventariar todos os storage buckets, containers e blobs
2. Verificar ACLs e bucket policies para exposicao publica
3. Identificar buckets com public access habilitado
4. Scan de dados sensiveis em storage exposto (PII, secrets, backups)
5. Verificar encryption at rest em todos os storage services
6. Auditar logging de acesso em storage (access logs, CloudTrail)
7. Verificar versioning e lifecycle policies
8. Testar cross-account access em storage compartilhado
9. Documentar findings com evidencia de exposicao
10. Registrar findings no `findings-registry`

## Output
- Inventario de storage com status de exposicao
- Lista de buckets/containers publicamente acessiveis
- Findings de dados sensiveis expostos
- Recomendacoes de remediacao por storage service

## Quality Gates
- [ ] Todos os storage services inventariados
- [ ] Public access verificado em cada bucket/container
- [ ] Encryption at rest validado
- [ ] Dados sensiveis em storage exposto identificados
- [ ] Access logging verificado em storage critico
- [ ] Checklist `cloud-storage-exposure` 100% atendido
