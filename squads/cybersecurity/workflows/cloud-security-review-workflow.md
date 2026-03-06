# Cloud Security Review Workflow

Processo para avaliar a postura de seguranca de ambientes e workloads em cloud.

## Objetivo

Garantir que deployments em cloud sigam as melhores praticas de seguranca, compliance e governanca, identificando misconfiguration e riscos antes e depois do deploy.

## Inputs

- Arquitetura do workload em cloud (diagramas, IaC templates)
- Cloud security baseline da organizacao
- CIS Benchmarks para o cloud provider
- Inventario de contas e subscriptions

## Stages

### 1. Scope e Context

- Responsavel: **Cloud Security Analyst Agent**
- Identificar cloud provider, servicos utilizados e modelo de responsabilidade
- Mapear data flows e integracao com ambientes on-premises
- Classificar dados armazenados e processados por sensibilidade

### 2. Identity e Access Review

- Responsavel: **IAM Review Agent**
- Auditar policies de IAM, roles e service accounts
- Verificar principio de least privilege
- Ponto de decisao: **Permissoes excessivas encontradas?**
  - Sim -> documentar finding e recomendar restricao
  - Nao -> prosseguir

### 3. Network Security Review

- Responsavel: **Network Security Agent**
- Revisar security groups, NACLs, firewall rules
- Verificar segmentacao e isolamento de workloads
- Identificar servicos expostos publicamente sem justificativa

### 4. Data Protection Review

- Responsavel: **Data Security Agent**
- Verificar encryption at rest e in transit
- Auditar configuracoes de storage (buckets, blobs) para acesso publico
- Validar backup e disaster recovery configurations

### 5. Logging e Monitoring Review

- Responsavel: **Detection Engineer Agent**
- Verificar que CloudTrail, Cloud Audit Logs ou equivalente estao habilitados
- Validar que logs estao sendo enviados ao SIEM
- Confirmar alertas para eventos criticos de seguranca

### 6. Compliance Mapping

- Responsavel: **Compliance Agent**
- Mapear controles implementados contra frameworks exigidos
- Identificar gaps de compliance especificos ao ambiente cloud
- Documentar evidencias de conformidade

### 7. Infrastructure as Code Review

- Responsavel: **AppSec Agent**
- Escanear templates de IaC (Terraform, CloudFormation) com ferramentas automatizadas
- Identificar misconfigurations antes do deploy
- Ponto de decisao: **Misconfigurations criticas?**
  - Sim -> bloquear deploy e corrigir
  - Nao -> aprovar com findings informativos

### 8. Report e Remediation

- Responsavel: **Cloud Security Analyst Agent**
- Compilar todos os findings em relatorio estruturado
- Priorizar por risco e facilidade de correcao
- Acompanhar remediacao ate closure

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Dados expostos publicamente | Bucket ou storage aberto | Remediar imediatamente e investigar |
| Root account em uso | Atividade com root credentials | Bloquear e criar users com least privilege |
| MFA desabilitado | Contas privilegiadas sem MFA | Exigir habilitacao imediata |
| Logging desabilitado | Sem audit trail | Habilitar antes de aprovar workload |

## Outputs

- Relatorio de cloud security review
- Lista de findings priorizados com recomendacoes
- Scorecard de compliance por framework
- Action items com owners e prazos
