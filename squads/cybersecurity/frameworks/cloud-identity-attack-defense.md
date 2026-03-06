# Cloud Identity Attack & Defense

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de seguranca de identidades em ambientes cloud (AWS, Azure,
GCP). Cobre abuso de IAM, role chaining, cross-account exploitation e federation attacks.
Perspectiva dual de ataque e defesa para protecao de identidades cloud.

## Requisitos de Autorizacao
- Permissao explicita do cloud account owner para cada conta testada
- Credenciais de teste com escopo limitado ao necessario
- Ambiente sandbox ou contas de teste dedicadas preferencial
- Acordo sobre limites de custo para recursos provisionados
- Plano de cleanup para remocao de todos os artefatos pos-teste

## Etapas de Ataque (Red Team)

### 1. IAM Enumeration
- Listagem de usuarios, roles, groups e policies (aws iam, az ad, gcloud iam)
- Identificacao de policies excessivamente permissivas (AdministratorAccess, Owner)
- Mapeamento de service accounts e suas permissoes efetivas
- Analise de trust policies e assume role conditions
- Identificacao de unused credentials e access keys antigos

### 2. IAM Privilege Escalation
- Abuso de iam:PassRole para atribuir roles privilegiados a recursos
- Exploiting iam:CreatePolicyVersion para elevar proprias permissoes
- Lambda function creation com execution role privilegiado
- EC2 instance profile abuse para obtencao de credenciais temporarias
- Azure: abuso de Managed Identity e custom role assignments

### 3. Role Chaining e Lateral Movement
- Encadeamento de AssumeRole para alcançar roles mais privilegiados
- Cross-account role assumption via trust relationship abuse
- Service account impersonation em GCP via iam.serviceAccountTokenCreator
- Pivoteamento entre subscriptions e projects via shared identities

### 4. Federation e SSO Attacks
- SAML assertion manipulation para privilege escalation
- Golden SAML: forja de assertions com signing certificate comprometido
- OAuth token theft e refresh token abuse em aplicacoes cloud
- OIDC provider misconfiguration exploitation
- Azure AD Connect abuse para sync de credenciais on-prem para cloud

### 5. Credential Harvesting em Cloud
- Instance metadata service (IMDS) exploitation (169.254.169.254)
- Environment variable extraction em serverless functions
- Secrets Manager e Parameter Store enumeration
- Cloud Shell e CloudTrail credential exposure

## Etapas de Defesa (Blue Team)

### 6. IAM Hardening
- Implementacao de least privilege com IAM Access Analyzer
- Habilitacao de MFA obrigatorio para todas as identidades humanas
- Rotacao automatica de access keys e service account credentials
- SCPs (Service Control Policies) para guardrails organizacionais
- Conditional access policies baseadas em risco e localizacao

### 7. Monitoramento e Deteccao
- CloudTrail/Activity Log/Audit Log para todas as acoes de IAM
- Alertas para AssumeRole anomalo e cross-account access incomum
- Deteccao de credential usage de IP addresses inesperados
- Monitoramento de IMDS access patterns em workloads
- Revisao periodica de IAM permissions com automated tools

## Ferramentas de Referencia
- Pacu, Prowler, ScoutSuite, CloudFox, Steampipe, enumerate-iam
- AzureHound, ROADtools, GCPBucketBrute, IAM Access Analyzer

## Integracao com Outros Frameworks
- Correlaciona com: active-directory-attack-defense.md (hybrid identity)
- Correlaciona com: container-security-methodology.md (cloud RBAC)
- Alimenta: lateral-movement-methodology.md (cross-account movement)
- Alimenta: persistence-analysis-methodology.md (cloud persistence)
