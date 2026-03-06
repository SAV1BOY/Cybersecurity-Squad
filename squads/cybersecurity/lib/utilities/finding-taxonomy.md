# Finding Taxonomy

Taxonomia padronizada para categorizacao de findings de seguranca.

## Categorias Principais (baseado em OWASP e CWE)

### Injection
- SQL Injection (CWE-89)
- Command Injection (CWE-78)
- LDAP Injection (CWE-90)
- XPath Injection (CWE-91)
- Server-Side Template Injection (CWE-1336)

### Broken Authentication
- Weak Password Policy (CWE-521)
- Missing MFA (CWE-308)
- Session Fixation (CWE-384)
- Credential Stuffing Vulnerability (CWE-307)
- Insecure Password Recovery (CWE-640)

### Sensitive Data Exposure
- Cleartext Transmission (CWE-319)
- Insecure Storage (CWE-312)
- Information Disclosure (CWE-200)
- Hardcoded Credentials (CWE-798)

### Broken Access Control
- IDOR (CWE-639)
- Privilege Escalation (CWE-269)
- Missing Authorization (CWE-862)
- Path Traversal (CWE-22)
- CORS Misconfiguration (CWE-942)

### Security Misconfiguration
- Default Credentials (CWE-1188)
- Unnecessary Services (CWE-1188)
- Missing Security Headers (CWE-693)
- Verbose Error Messages (CWE-209)
- Outdated Software (CWE-1104)

### Cross-Site Scripting (XSS)
- Reflected XSS (CWE-79)
- Stored XSS (CWE-79)
- DOM-based XSS (CWE-79)

### Cryptographic Failures
- Weak Algorithms (CWE-327)
- Insufficient Key Length (CWE-326)
- Missing Encryption (CWE-311)

### Cloud Security
- Public S3 Bucket (CWE-732)
- Overly Permissive IAM (CWE-250)
- Unencrypted Resources (CWE-311)
- Missing Logging (CWE-778)

## Uso

Ao registrar um finding, selecionar a categoria e subcategoria mais especifica.
Incluir o CWE ID para referencia padronizada e interoperabilidade com ferramentas.
