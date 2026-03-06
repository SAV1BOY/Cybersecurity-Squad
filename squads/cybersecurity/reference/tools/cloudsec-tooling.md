# Cloud Security Tooling

## Visao Geral
Ferramentas para avaliacao e monitoramento de seguranca em ambientes cloud
(AWS, Azure, GCP). O squad utiliza estas ferramentas em assessments e
operacoes continuas de seguranca.

## Cloud Security Posture Management (CSPM)

### Prowler
- **Tipo**: open-source cloud security assessment (AWS, Azure, GCP)
- **Uso**: verificar conformidade com CIS, PCI DSS, NIST, GDPR
- **Checks**: centenas de verificacoes automatizadas
- **Output**: HTML, CSV, JSON para integracao

### ScoutSuite
- **Tipo**: multi-cloud security auditing tool
- **Uso**: assessment de configuracao de seguranca
- **Clouds**: AWS, Azure, GCP, Oracle Cloud, Alibaba Cloud
- **Diferencial**: relatorio HTML interativo

### CloudSploit
- **Tipo**: cloud security scanning open-source
- **Uso**: detectar riscos de configuracao
- **Plugins**: modular e extensivel

## Cloud Pentesting

### Pacu
- **Tipo**: AWS exploitation framework
- **Uso**: pentesting de ambientes AWS
- **Modulos**: IAM enum, privilege escalation, data exfiltration
- **Analogia**: Metasploit para AWS

### CloudFox
- **Tipo**: ferramenta para encontrar attack paths em cloud
- **Uso**: enumerar permissoes e caminhos de escalacao
- **Clouds**: AWS, Azure, GCP

### enumerate-iam
- **Tipo**: IAM permission enumeration
- **Uso**: descobrir permissoes de credenciais AWS comprometidas

## Infrastructure as Code (IaC) Security

### Checkov
- **Tipo**: IaC scanning tool
- **Uso**: analisar Terraform, CloudFormation, Kubernetes, Dockerfile
- **Regras**: centenas de policies pre-definidas
- **Integracao**: CI/CD, IDE plugins

### tfsec / Trivy
- **Tipo**: Terraform security scanner (tfsec agora parte do Trivy)
- **Uso**: detectar misconfigurations em Terraform
- **Diferencial**: rapido e facil de integrar

### KICS (Keeping Infrastructure as Code Secure)
- **Tipo**: IaC scanner multi-formato
- **Uso**: Terraform, CloudFormation, Ansible, Docker, Kubernetes

## Cloud Forensics e IR

### CloudTrail / Activity Log / Audit Log
- **Tipo**: native cloud audit logging
- **Uso**: investigacao de incidentes e compliance
- **Dica**: garantir que estao habilitados e centralizados

### Cartography
- **Tipo**: graph-based cloud asset inventory
- **Uso**: visualizar relacoes entre recursos cloud
- **Diferencial**: Neo4j para queries complexas

## Workflow do Squad para Cloud Assessments
1. IaC review com Checkov/tfsec
2. Configuration assessment com Prowler/ScoutSuite
3. IAM review com CloudFox/enumerate-iam
4. Attack path analysis com Pacu
5. Remediation guidance com referencia a CIS Benchmarks

## Notas do Squad
Cloud security e uma das areas de maior crescimento. Manter certificacoes
cloud atualizadas e praticar em ambientes de lab proprios.
