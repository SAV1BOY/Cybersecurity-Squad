# Cloud - Logging and Trails

Checklist para auditoria de logging e audit trails em cloud.

## AWS CloudTrail
- [ ] CloudTrail habilitado em todas as regions
- [ ] Multi-region trail configurado
- [ ] Management events logging habilitado
- [ ] Data events habilitados para S3 e Lambda criticos
- [ ] CloudTrail log file validation habilitado
- [ ] CloudTrail logs enviados para S3 com encryption
- [ ] CloudTrail integrated com CloudWatch Logs
- [ ] S3 bucket de CloudTrail com access logging habilitado

## Azure Monitoring
- [ ] Azure Activity Log habilitado e retido por 90+ dias
- [ ] Azure AD Sign-in Logs coletados
- [ ] Azure AD Audit Logs coletados
- [ ] Diagnostic Settings configuradas para recursos criticos
- [ ] NSG Flow Logs habilitados
- [ ] Azure Monitor Alerts configurados para eventos criticos
- [ ] Log Analytics Workspace configurado e funcional

## GCP Cloud Audit Logs
- [ ] Admin Activity Audit Logs habilitados (default)
- [ ] Data Access Audit Logs habilitados para servicos criticos
- [ ] System Event Audit Logs habilitados
- [ ] Logs exported para Cloud Storage ou BigQuery
- [ ] Log-based metrics configuradas para eventos criticos
- [ ] VPC Flow Logs habilitados para subnets criticas

## Protecao de Logs
- [ ] Logs armazenados em bucket/storage com immutability
- [ ] Log deletion protegida por policy (MFA delete, retention lock)
- [ ] Encryption at rest habilitada para log storage
- [ ] Access control restrito para log data
- [ ] Cross-account/cross-project log replication configurada
- [ ] Alertas para log tampering ou deletion configurados
- [ ] Backup de logs em regiao/conta separada

## Integracao e Centralizacao
- [ ] Logs centralizados em SIEM ou log management platform
- [ ] Log parsing e normalization funcionais
- [ ] Retention policy adequada (hot: 90 dias, cold: 1 ano+)
- [ ] Search e query capabilities verificadas
- [ ] Alerting baseado em cloud logs funcional
- [ ] Dashboard de cloud security events operacional

## Cobertura e Gaps
- [ ] Todos os servicos criticos com logging habilitado
- [ ] Gaps de logging identificados e documentados
- [ ] Cost optimization de logging realizado (sem perder cobertura)
- [ ] Compliance requirements para logging atendidos
- [ ] Log volume monitorado para anomalias
- [ ] Report de audit de logging entregue com recommendations
