# Cloud Security Architectures

Padroes de arquitetura de seguranca para ambientes cloud (AWS, Azure, GCP).

## Landing Zone Segura (AWS)

```
Organization Root
├── Security OU
│   ├── Log Archive Account (centralized logging)
│   └── Security Tooling Account (GuardDuty, SecurityHub)
├── Infrastructure OU
│   ├── Network Account (Transit Gateway, DNS)
│   └── Shared Services Account
├── Workloads OU
│   ├── Production Accounts
│   └── Staging Accounts
└── Sandbox OU
    └── Developer Accounts (SCPs restritivos)
```

## Controles Essenciais por Camada

### Account Level
- SCPs para prevenir desabilitacao de CloudTrail e GuardDuty
- Billing alerts para detectar crypto mining
- Root account com MFA hardware e sem uso diario

### Network Level
- VPC per workload com private subnets para dados
- Security Groups como principal controle (deny by default)
- VPC Flow Logs habilitados em todas as VPCs
- AWS PrivateLink para servicos internos

### Data Level
- Encryption at rest (KMS CMK) para todos os data stores
- Encryption in transit (TLS 1.2+) obrigatorio
- S3 Block Public Access habilitado na organization
- Data classification tags em todos os recursos

### Identity Level
- AWS SSO com IdP corporativo (Okta, Azure AD)
- Permission boundaries em todas as IAM roles
- Access Analyzer para identificar acessos excessivos

## Monitoramento Cloud-Native

- CloudTrail -> S3 -> Athena para analise forense
- GuardDuty para threat detection automatizada
- SecurityHub para compliance posture consolidado
- Config Rules para drift detection continuo
