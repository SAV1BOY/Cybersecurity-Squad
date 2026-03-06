# Cloud Security Assessment Quality Gate

Checklist de qualidade para avaliacao de seguranca em cloud.

## Identity & Access Management
- [ ] IAM policies revisadas para least privilege
- [ ] Root/admin account usage auditado
- [ ] MFA habilitado para todas as contas privilegiadas
- [ ] Service accounts e roles auditados
- [ ] Cross-account access policies revisadas
- [ ] Stale credentials e unused accounts identificados
- [ ] Federation e SSO configuration validada

## Network Security
- [ ] Security groups e NACLs revisados para over-permission
- [ ] VPC peering e transit gateway configuration auditada
- [ ] Public IP assignments revisados e justificados
- [ ] VPN e Direct Connect configurations validadas
- [ ] Network segmentation verificada entre workloads
- [ ] DNS resolution e private hosted zones revisadas

## Data Protection
- [ ] Encryption at rest habilitada e validada (KMS keys, rotation)
- [ ] Encryption in transit verificada (TLS enforcement)
- [ ] Storage buckets/blobs testados para public access
- [ ] Backup policies revisadas e testadas
- [ ] Data classification aplicada a storage resources
- [ ] DLP policies implementadas e funcionais

## Compute e Workload Security
- [ ] Instance metadata service (IMDS) v2 enforced
- [ ] AMI/image hardening verificado
- [ ] Auto-scaling configurations revisadas para seguranca
- [ ] Serverless functions auditadas (permissions, env vars, timeouts)
- [ ] Container orchestration security verificada (EKS, AKS, GKE)

## Logging e Monitoring
- [ ] CloudTrail/Activity Log/Audit Log habilitado e centralizado
- [ ] Flow logs habilitados para VPCs criticas
- [ ] Alerting configurado para eventos de seguranca
- [ ] Log retention policy adequada ao compliance
- [ ] SIEM integration funcional e testada

## Compliance e Governance
- [ ] CIS Benchmark scan executado para o cloud provider
- [ ] Resource tagging policy verificada
- [ ] Cost anomaly detection habilitado (indicador de compromise)
- [ ] Infrastructure as Code (IaC) templates auditados
- [ ] Drift detection implementado e monitorado
- [ ] Findings priorizados com business context
