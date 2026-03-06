# Cloud - Multi-Account Security

Checklist para seguranca em ambientes cloud multi-account/multi-project.

## Estrategia de Accounts
- [ ] Account/project strategy documentada (por env, por app, por team)
- [ ] Naming convention definida e seguida
- [ ] Account hierarchy documentada (Organizations, Management Groups)
- [ ] Account vending process automatizado e seguro
- [ ] Decommissioning process para accounts definido
- [ ] Account inventory atualizado e acessivel

## Governance Centralizada
- [ ] Organizations/Management Groups configurados
- [ ] Service Control Policies (SCPs) aplicadas
- [ ] Azure Policies aplicadas em Management Group level
- [ ] GCP Organization Policies configuradas
- [ ] Guardrails preventivos implementados (prevent public S3, etc.)
- [ ] Tag policies enforced para cost e security tracking
- [ ] Compliance baselines aplicadas em todas as accounts

## Identity Centralizada
- [ ] SSO configurado para acesso a todas as accounts
- [ ] Identity Provider centralizado (AWS SSO, Azure AD, GCP Identity)
- [ ] Role-based access definido por account e por funcao
- [ ] Break-glass accounts configurados e monitored
- [ ] Root account credentials secured e monitored por account
- [ ] Cross-account roles auditados e com least privilege
- [ ] Access reviews realizados regularmente

## Logging e Monitoring Centralizado
- [ ] CloudTrail/Audit Logs centralizados em account dedicada
- [ ] Security Hub/Defender/SCC habilitado centralmente
- [ ] GuardDuty/Defender for Cloud habilitado em todas as accounts
- [ ] Log aggregation em SIEM centralizado
- [ ] Alerting centralizado para eventos de seguranca
- [ ] Dashboards de seguranca multi-account operacionais
- [ ] Cost anomaly detection habilitado em todas as accounts

## Network Architecture
- [ ] Network topology multi-account documentada
- [ ] Transit gateway/hub-spoke architecture implementada
- [ ] Shared services account/VPC definida
- [ ] DNS resolution centralizada e segura
- [ ] Internet egress centralizado (se aplicavel)
- [ ] Network isolation entre accounts verificada

## Security Baselines
- [ ] CIS Benchmark aplicado em todas as accounts
- [ ] Config Rules/Policy Compliance monitorada
- [ ] Automated remediation para violacoes criticas
- [ ] New account bootstrapping inclui security baseline
- [ ] Drift detection implementada e monitorada
- [ ] Compliance score por account rastreado

## Operacao
- [ ] Incident response process para multi-account definido
- [ ] Vulnerability management centralizado
- [ ] Patch management coordenado entre accounts
- [ ] Backup strategy por account definida
- [ ] Disaster recovery testado para multi-account
- [ ] Report de security posture multi-account gerado
