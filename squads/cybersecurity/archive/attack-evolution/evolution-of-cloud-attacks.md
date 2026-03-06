# Evolution of Cloud Attacks

Historia e evolucao dos ataques direcionados a ambientes cloud.

## Timeline Evolutiva

### Era 1: Misconfiguration Era (2015-2018)
- S3 buckets publicos como principal vetor
- Databases expostas sem autenticacao (MongoDB, Elasticsearch)
- Credenciais hardcoded em repositorios publicos
- Atacantes faziam scan massivo por recursos mal configurados
- Breaches de alto perfil por erros basicos de configuracao

### Era 2: Identity Attacks (2019-2021)
- Foco muda para compromisso de identidades cloud (IAM)
- Stolen access keys e session tokens
- Cross-account attacks via trust relationships
- Instance metadata service (IMDS) exploitation
- SSRF para roubo de credenciais via metadata endpoint

### Era 3: Control Plane Attacks (2021-2023)
- Ataques ao management plane dos cloud providers
- Exploitation de servicos serverless (Lambda, Functions)
- Container escape e Kubernetes exploitation
- Abuse de permissoes excessivas em service accounts
- Cloud-native malware e cryptomining

### Era 4: Multi-Cloud e SaaS Targeting (2023-presente)
- Ataques cross-cloud explorando complexidade multi-cloud
- SaaS application compromise (OAuth token theft)
- API abuse em servicos cloud-native
- AI/ML service exploitation
- Data exfiltration via servicos cloud legitimos

## Ataques Notaveis

| Ataque | Ano | Vetor | Impacto |
|--------|-----|-------|---------|
| Capital One | 2019 | SSRF + metadata | 100M registros |
| Microsoft Exchange (Hafnium) | 2021 | Zero-day exploit | 30K+ organizacoes |
| Uber | 2022 | MFA fatigue + Slack | Acesso total |
| CircleCI | 2023 | Session token theft | Secrets de clientes |
| Microsoft Storm-0558 | 2023 | Forged auth tokens | Emails gov dos EUA |

## Defesas Essenciais

- Cloud Security Posture Management (CSPM)
- IMDSv2 enforcement (AWS)
- Least privilege IAM com permission boundaries
- Cloud workload protection (CWPP)
- Logging centralizado (CloudTrail, Activity Log)
- Network controls (security groups, NACLs)
- Secrets management (nao hardcode, usar vaults)

## Tendencia

Complexidade de ambientes multi-cloud amplia a superfície de ataque.
Seguranca cloud requer expertise especializada e tooling dedicado.
