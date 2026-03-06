# Cloud Assessment Brief

> Documento de escopo para avaliacao de seguranca em ambientes cloud.
> Preencha antes de iniciar o assessment de infraestrutura cloud.

---

## 1. Informacoes Gerais

- **Nome do Projeto:** [NOME_DO_PROJETO]
- **Cloud Provider(s):** [AWS / GCP / AZURE / MULTI_CLOUD]
- **Assessment Lead:** [NOME_DO_LIDER]
- **Cloud Architect / Contact:** [NOME_DO_ARQUITETO_CLOUD]
- **Data de Inicio:** [DATA_INICIO]
- **Data de Termino:** [DATA_TERMINO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DO_CLOUD_ASSESSMENT_E_MOTIVACAO]

## 3. Escopo do Ambiente

### 3.1 Contas e Subscriptions

| Account ID | Alias / Nome | Ambiente | Regiao |
|------------|--------------|----------|--------|
| [ACCOUNT_ID] | [ALIAS] | [PROD / STAGING / DEV] | [REGIAO] |
| [ACCOUNT_ID] | [ALIAS] | [PROD / STAGING / DEV] | [REGIAO] |

### 3.2 Servicos em Uso

- Compute: [EC2 / ECS / LAMBDA / GKE / OUTRO]
- Storage: [S3 / GCS / BLOB_STORAGE / OUTRO]
- Database: [RDS / DYNAMODB / CLOUD_SQL / OUTRO]
- Networking: [VPC / CLOUDFRONT / LOAD_BALANCERS]
- Identity: [IAM / SSO / ACTIVE_DIRECTORY]
- [SERVICOS_ADICIONAIS]

## 4. Framework de Avaliacao

- **Benchmark utilizado:** [CIS_BENCHMARK / AWS_WELL_ARCHITECTED / NIST_CSF / CSA_CCM]
- **Dominios avaliados:**
  - [ ] Identity & Access Management (IAM)
  - [ ] Network Security
  - [ ] Data Protection
  - [ ] Logging & Monitoring
  - [ ] Incident Response readiness
  - [ ] Compliance & Governance
  - [ ] [DOMINIO_ADICIONAL]

## 5. Acessos Necessarios

| Tipo de Acesso | Nivel | Justificativa |
|----------------|-------|---------------|
| [READ_ONLY_IAM_ROLE] | [VIEWER / AUDITOR] | [JUSTIFICATIVA] |
| [SECURITY_AUDIT_ROLE] | [SECURITY_AUDITOR] | [JUSTIFICATIVA] |
| [ACESSO_ADICIONAL] | [NIVEL] | [JUSTIFICATIVA] |

## 6. Ferramentas

- Scanner de configuracao: [PROWLER / SCOUT_SUITE / CLOUD_CUSTODIAN / OUTRO]
- CSPM: [PLATAFORMA_CSPM_UTILIZADA]
- Analise de IAM: [IAMLIVE / CLOUDSPLAINING / OUTRO]
- [FERRAMENTA_ADICIONAL]

## 7. Restricoes

- Ambientes que nao devem ser alterados: [LISTA]
- Recursos criticos com restricao de scan: [LISTA]
- Janela de execucao: [HORARIO_PERMITIDO]
- [RESTRICAO_ADICIONAL]

## 8. Entregaveis

- [ ] Relatorio de compliance com benchmark
- [ ] Inventario de misconfigurations
- [ ] Mapa de attack surface cloud
- [ ] Recomendacoes priorizadas
- [ ] [ENTREGAVEL_ADICIONAL]

## 9. Aprovacoes

| Nome | Cargo | Assinatura | Data |
|------|-------|------------|------|
| [NOME] | [CARGO] | __________ | [DATA] |
| [NOME] | [CARGO] | __________ | [DATA] |

---

*Template versao 1.0 — Cybersecurity Squad*
