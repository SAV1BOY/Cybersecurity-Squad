# Cloud Security Assessment Project

Template de projeto para assessment de seguranca em ambiente cloud.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Cloud Provider | [AWS / Azure / GCP / Multi-cloud] |
| Scope | [Contas, subscriptions, projetos] |
| Tipo | Cloud Security Posture Assessment |
| Duracao | [2-4 semanas] |
| Framework | CIS Benchmarks + custom checks |
| Equipe | [Cloud security engineers] |

## Areas de Avaliacao

### Identity & Access Management
- [ ] MFA enforcement para todos os usuarios
- [ ] Root/admin account protection
- [ ] IAM policies least privilege analysis
- [ ] Service account permissions review
- [ ] Cross-account trust relationships
- [ ] Access key rotation e age audit

### Network Security
- [ ] Security group rules review (overly permissive)
- [ ] Network ACL configuration
- [ ] VPC flow logs habilitados
- [ ] Public-facing resources inventory
- [ ] VPN e connectivity security
- [ ] DNS security configuration

### Data Protection
- [ ] Encryption at rest (EBS, S3, RDS, etc.)
- [ ] Encryption in transit enforcement
- [ ] Public access blocks (S3, storage accounts)
- [ ] Data classification e tagging
- [ ] Backup configuration e retention

### Logging & Monitoring
- [ ] CloudTrail / Activity Log habilitado em todas regioes
- [ ] Log centralization e retention
- [ ] Alertas para acoes administrativas criticas
- [ ] Cost anomaly detection

### Compute Security
- [ ] Instance metadata service v2 enforcement
- [ ] Container image scanning
- [ ] Kubernetes RBAC e pod security
- [ ] Serverless function permissions
- [ ] Patch management para VMs

### Compliance
- [ ] CIS Benchmark compliance score
- [ ] Regulatory requirements mapping
- [ ] Tagging policy compliance
- [ ] Region restrictions

## Ferramentas

- **AWS**: Prowler, ScoutSuite, AWS Security Hub
- **Azure**: AzureHound, ScoutSuite, Defender for Cloud
- **GCP**: ScoutSuite, Forseti, SCC
- **Multi-cloud**: Wiz, Orca, Prisma Cloud

## Deliverables

- Relatorio com findings categorizados por severidade e area
- CIS Benchmark compliance score
- Remediation roadmap priorizado
- Comparacao com assessment anterior (se disponivel)
