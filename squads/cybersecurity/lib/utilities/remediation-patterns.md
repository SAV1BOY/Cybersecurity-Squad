# Remediation Patterns

Padroes de remediacao reutilizaveis para categorias comuns de vulnerabilidades.

## Injection Vulnerabilities

### SQL Injection
- **Fix**: Parameterized queries / prepared statements
- **Framework**: Use ORM (SQLAlchemy, Hibernate, ActiveRecord)
- **Validacao**: Input validation com whitelist de caracteres permitidos
- **Defesa adicional**: Least privilege no usuario de banco

### Command Injection
- **Fix**: Evitar execucao de comandos do SO; usar APIs nativas
- **Se necessario**: Whitelist de comandos permitidos, escapar inputs
- **Defesa adicional**: Sandboxing, containers com capabilities restritas

### XSS
- **Fix**: Output encoding context-aware (HTML, JS, URL, CSS)
- **Framework**: Template engines com auto-escaping (React, Jinja2)
- **Defesa adicional**: Content Security Policy (CSP) restritiva

## Authentication Issues

### Weak Password Policy
- **Fix**: Minimo 12 caracteres, verificacao contra breach databases
- **Implementar**: bcrypt/argon2 para hashing com salt unico
- **Defesa adicional**: MFA obrigatorio para contas privilegiadas

### Session Management
- **Fix**: Tokens criptograficamente seguros, HttpOnly + Secure flags
- **Implementar**: Session timeout, re-autenticacao para acoes sensiveis
- **Defesa adicional**: Bind session ao IP/device fingerprint

## Access Control

### IDOR
- **Fix**: Authorization check server-side em cada request
- **Implementar**: UUIDs nao sequenciais + ownership validation
- **Defesa adicional**: Rate limiting, logging de acessos negados

### Privilege Escalation
- **Fix**: RBAC centralizado com enforcement em cada endpoint
- **Implementar**: Decorators/middleware de authorization
- **Defesa adicional**: Audit logging de mudancas de permissao

## Cloud Misconfiguration

### Public Storage
- **Fix**: Block Public Access no nivel de conta
- **Implementar**: IaC com policies restritivas por default
- **Defesa adicional**: Monitoramento continuo com alertas

### Overly Permissive IAM
- **Fix**: Least privilege baseado em Access Analyzer
- **Implementar**: Permission boundaries, SCPs
- **Defesa adicional**: Alertas para policy changes
