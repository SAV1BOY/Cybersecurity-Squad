# Cloud - Storage Exposure

Checklist para auditoria de exposicao de armazenamento em cloud.

## Inventario de Storage
- [ ] S3 buckets / Azure Blobs / GCS buckets catalogados
- [ ] EBS volumes e snapshots inventariados
- [ ] RDS snapshots e database backups catalogados
- [ ] File shares (EFS, Azure Files) inventariados
- [ ] Container registries catalogados
- [ ] CDN origins mapeados
- [ ] Data classification aplicada a cada storage resource

## Public Access Assessment
- [ ] S3 Block Public Access habilitado no account level
- [ ] Cada bucket verificado para public access (ACL e policy)
- [ ] Azure Storage public access desabilitado por default
- [ ] GCS uniform bucket-level access habilitado
- [ ] Public snapshots (EBS, RDS) identificados e remediados
- [ ] Public container images identificados e avaliados
- [ ] Pre-signed URL policies revisadas (expiration time)

## Access Control
- [ ] Bucket/container policies revisadas para over-permission
- [ ] IAM policies de acesso a storage auditadas
- [ ] Cross-account access justificado e documentado
- [ ] Service account access a storage com least privilege
- [ ] SAS tokens (Azure) com scope e expiration adequados
- [ ] CORS configuration restritiva nos buckets web-facing
- [ ] VPC endpoint/private link para acesso interno preferido

## Encryption
- [ ] Encryption at rest habilitada em todos os storage
- [ ] KMS key management adequado (rotation, access control)
- [ ] Customer-managed keys (CMK) utilizados para dados sensiveis
- [ ] Encryption in transit enforced (HTTPS only, TLS)
- [ ] Client-side encryption avaliada para dados altamente sensiveis
- [ ] Key access policies auditadas

## Data Lifecycle
- [ ] Lifecycle policies configuradas (transition, expiration)
- [ ] Versioning habilitado para buckets criticos
- [ ] MFA delete habilitado para buckets com dados sensiveis
- [ ] Backup e recovery testados
- [ ] Retention policies conforme compliance requirements
- [ ] Data deletion procedures documentadas e testadas

## Monitoramento e Deteccao
- [ ] Access logging habilitado para storage critico
- [ ] Alertas para public access changes configurados
- [ ] Alertas para unusual access patterns configurados
- [ ] Data exfiltration detection implementada
- [ ] Automated remediation para public access (auto-close)
- [ ] Regular scanning para storage exposure (Prowler, ScoutSuite)
- [ ] Report de exposicao de storage entregue
