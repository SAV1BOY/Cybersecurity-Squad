# Cloud Security Lab

## Objetivo
Ambiente para pratica de seguranca em cloud (AWS, Azure, GCP), incluindo
assessment, exploitation e defesa de infraestruturas cloud.

## Ambientes Disponveis

### AWS Lab Account
- **Organizacao**: lab-org com multiple accounts
- **Identidade**: IAM users, roles, policies com misconfigurations
- **Compute**: EC2 instances com IMDS vulneravel
- **Storage**: S3 buckets com permissoes variadas
- **Network**: VPCs com security groups misconfigured
- **Serverless**: Lambda functions com vulnerabilidades
- **Container**: ECS/EKS com configuracoes inseguras

### Azure Lab Tenant
- **Identity**: Azure AD com usuarios e grupos
- **Compute**: VMs com NSGs misconfigured
- **Storage**: Blob storage com acesso publico
- **AKS**: Kubernetes cluster para container security
- **App Services**: web apps com vulnerabilidades

### GCP Lab Project
- **IAM**: service accounts com excessive permissions
- **GCE**: instances com metadata exposure
- **GCS**: buckets com permissoes inadequadas
- **GKE**: cluster Kubernetes para pratica

## Cenarios de Ataque

### AWS Attack Paths
1. SSRF via IMDS para credential theft
2. S3 bucket enumeration e data exfiltration
3. IAM privilege escalation paths
4. Lambda function exploitation
5. Cross-account access abuse

### Azure Attack Paths
1. Azure AD enumeration e password spray
2. Managed Identity abuse
3. Storage account key exposure
4. Key Vault access exploitation
5. Runbook-based privilege escalation

### Cloud Defense Exercises
1. Implementar least privilege IAM
2. Configurar cloud logging e monitoring
3. Deploy GuardDuty/Defender/SCC
4. Network segmentation com VPC/NSG
5. Encryption at rest e in transit

## Ferramentas Utilizadas
- **Assessment**: Prowler, ScoutSuite, Checkov
- **Attack**: Pacu, CloudFox, enumerate-iam
- **Defense**: CloudTrail, GuardDuty, AWS Config
- **IaC**: Terraform com tfsec/Trivy

## Controle de Custos
- Budget alerts configurados por account
- Auto-shutdown de resources fora de horario
- Usar instancias spot/preemptible quando possivel
- Cleanup automatico de resources de lab
- Limites de spending por membro

## Notas do Squad
Cloud security e area de maior crescimento. Cada membro deve ter
experiencia pratica em pelo menos uma cloud provider.
