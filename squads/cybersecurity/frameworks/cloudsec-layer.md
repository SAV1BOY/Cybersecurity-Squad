# CloudSec Layer — Framework Operacional

> Camada de seguranca cloud: IAM, logging, storage, network e policies.

## Objetivo

A CloudSec Layer garante que infraestrutura cloud (AWS, GCP, Azure) esteja configurada de forma segura, com principio de menor privilegio, visibilidade completa e guardrails preventivos. Cloud misconfiguration e o vetor de ataque #1 em ambientes cloud — esta camada elimina isso sistematicamente.

## Principios

1. **Identity is the new perimeter** — IAM e o controle mais critico
2. **Least privilege by default** — Nenhum acesso alem do minimo necessario
3. **Logs everywhere** — CloudTrail, VPC Flow, Access Logs — tudo habilitado
4. **Preventive > detective** — SCPs e guardrails antes de alertas
5. **Infrastructure as Code** — Config versionada, revisada, auditavel
6. **Multi-account isolation** — Workloads separados por conta/projeto
7. **Encryption by default** — Em transito e em repouso, sempre

## Pilares de Cloud Security

### 1. Identity & Access Management (IAM)
```
Checklist IAM:
- [ ] Sem usuarios root/owner em uso diario
- [ ] MFA habilitado para todos os humanos
- [ ] Service accounts com menor privilegio
- [ ] Sem access keys de longa duracao (preferir roles/federation)
- [ ] Cross-account access via assume-role (nao credentials compartilhadas)
- [ ] Revisao periodica de permissoes (quarterly)
- [ ] JIT (Just-In-Time) access para operacoes privilegiadas
- [ ] Condicoes de contexto (IP, horario, MFA) em policies criticas
```

### 2. Logging & Monitoring
```
Fontes obrigatorias:
- CloudTrail / Activity Log (management + data events)
- VPC Flow Logs / NSG Flow Logs
- S3/GCS/Blob access logs
- WAF logs
- DNS query logs
- GuardDuty / Security Center / SCC alerts
Retencao: minimo 1 ano para audit trail
```

### 3. Data Protection
- **Encryption at rest**: KMS/CMK para dados sensiveis, SSE para demais
- **Encryption in transit**: TLS 1.2+ obrigatorio
- **Storage exposure**: Zero public buckets/blobs por default
- **Data classification**: Tags de classificacao em todos os data stores
- **Backup**: Backup encryption + cross-region + access control

### 4. Network Security
- **VPC/VNet isolation**: Workloads isolados por segmento
- **Security Groups/NSGs**: Deny-all default, allow explicito
- **Egress control**: Saber e controlar o que sai da rede
- **Private endpoints**: Servicos acessados via private link
- **No public IPs**: Load balancers como unico ponto de entrada

### 5. Guardrails & Governance
- **SCPs / Organization Policies**: Preventivos no nivel da org
- **Config rules**: Compliance automatizada
- **Tag policies**: Padronizacao de tags (owner, env, classification)
- **Budget alerts**: Anomalias de custo podem indicar compromisso

### 6. Container & Serverless
- **Image scanning**: Antes do deploy (Trivy, ECR scanning)
- **RBAC**: Kubernetes RBAC com menor privilegio
- **Network policies**: Pod-to-pod isolation
- **Runtime monitoring**: Falco, GuardDuty EKS
- **Serverless permissions**: Cada function com sua propria role minima

## Cloud Attack Patterns Comuns

| Ataque | Defesa |
|--------|--------|
| Public S3 bucket | Block public access no nivel da conta |
| Stolen access keys | Federation + rotacao + monitoring |
| Privilege escalation via IAM | Policy boundaries + access analyzer |
| SSRF to metadata service | IMDSv2 obrigatorio (AWS), metadata concealment |
| Cross-account trust abuse | Conditions em trust policies |
| Crypto mining via compromised instance | Cost anomaly alerts + GuardDuty |

## Agentes Envolvidos

| Agente | Papel na CloudSec Layer |
|--------|------------------------|
| Omar Santos | IAM audit, hardening, logging, SOC integration |
| Cartographer | Cloud asset inventory, exposure mapping |
| Chris Sanders | Log analysis, detection rules para cloud |
| Cyber Chief | Policy decisions, multi-account strategy |

## Outputs

- IAM audit report com recomendacoes
- Cloud configuration assessment
- Logging coverage matrix
- Network segmentation diagram
- Guardrails documentation
- Remediation plan priorizado

## Quality Gates

- `cloud-security-assessment-quality.md`
- `cloud/cloud-iam-least-privilege.md`
- `cloud/cloud-logging-and-trails.md`
- `cloud/cloud-storage-exposure.md`

## Used By

### Tasks (config.yaml routing)
- iam-least-privilege-project
- storage-exposure-audit
- cloud-logging-setup
- network-segmentation-review
- cloud-guardrails-setup
- multi-cloud-security-review
- cloud-forensics

### Agents
- omar-santos
- cartographer
- chris-sanders

### Related Checklists
- cloud-security-assessment-quality
- cloud/cloud-iam-least-privilege

### Cross-References
- Config routing: `config.yaml`
- Quality gate system: `docs/quality-gate-system.md`
