# Web App Assessment Project

Template de projeto para assessment de seguranca de aplicacoes web.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Aplicacao | [Nome e URL] |
| Tipo | Web Application Security Assessment |
| Metodologia | OWASP Testing Guide v4.2 |
| Modalidade | [Grey-box recomendado] |
| Duracao | [1-3 semanas por app] |
| Equipe | [AppSec engineers] |

## Checklist OWASP

### Information Gathering
- [ ] Application fingerprinting e technology stack
- [ ] Application entry points mapping
- [ ] API endpoint discovery e documentation review

### Configuration & Deployment
- [ ] Security headers (CSP, HSTS, X-Frame-Options)
- [ ] CORS configuration
- [ ] Error handling e information disclosure
- [ ] TLS configuration e certificate validation

### Identity Management
- [ ] User registration process
- [ ] Account provisioning e enumeration
- [ ] Password policy e reset mechanism

### Authentication
- [ ] Brute force protection
- [ ] Default credentials
- [ ] Session management (cookies, tokens)
- [ ] Multi-factor authentication bypass

### Authorization
- [ ] IDOR e direct object references
- [ ] Privilege escalation (horizontal e vertical)
- [ ] Missing function-level access control
- [ ] JWT/OAuth implementation

### Input Validation
- [ ] SQL Injection (all parameter types)
- [ ] Cross-Site Scripting (reflected, stored, DOM)
- [ ] Command Injection
- [ ] SSRF (Server-Side Request Forgery)
- [ ] File upload vulnerabilities
- [ ] XML External Entity (XXE)

### Business Logic
- [ ] Workflow bypass
- [ ] Rate limiting e abuse prevention
- [ ] Race conditions
- [ ] Price manipulation e business logic flaws

### API Security (OWASP API Top 10)
- [ ] Broken Object Level Authorization
- [ ] Broken Authentication
- [ ] Excessive Data Exposure
- [ ] Mass Assignment
- [ ] Security Misconfiguration

## Deliverables

- Relatorio completo com findings padronizados
- Executive summary
- Remediation plan priorizado
- Retest apos 30 dias
