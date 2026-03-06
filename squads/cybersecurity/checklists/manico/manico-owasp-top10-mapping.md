# Manico - OWASP Top 10 Mapping

Checklist para mapeamento de cobertura do OWASP Top 10 em aplicacoes.

## A01:2021 - Broken Access Control
- [ ] Violation of least privilege verificada
- [ ] Bypass of access control checks testado (URL tampering, API manipulation)
- [ ] IDOR (Insecure Direct Object Reference) testado em todos os endpoints
- [ ] CORS misconfiguration verificada
- [ ] Forced browsing testado para paginas autenticadas
- [ ] Directory traversal testado em file operations
- [ ] Metadata manipulation (JWT, cookies) testada

## A02:2021 - Cryptographic Failures
- [ ] Data classification realizada (sensitive data identified)
- [ ] Encryption at rest verificada para dados sensiveis
- [ ] TLS enforcement verificado (HSTS, secure redirects)
- [ ] Weak algorithms identificados (MD5, SHA1, DES, RC4)
- [ ] Key management practices revisadas
- [ ] Password storage com hashing adequado (bcrypt, Argon2)

## A03:2021 - Injection
- [ ] SQL injection testado com payloads automatizados e manuais
- [ ] NoSQL injection verificada
- [ ] OS command injection testada
- [ ] LDAP injection verificada (se aplicavel)
- [ ] Template injection (SSTI) testada
- [ ] ORM injection verificada

## A04:2021 - Insecure Design
- [ ] Threat modeling realizado para fluxos criticos
- [ ] Business logic flaws testados
- [ ] Rate limiting implementado em operacoes sensiveis
- [ ] Segregation of duties verificada

## A05:2021 - Security Misconfiguration
- [ ] Default credentials verificadas
- [ ] Unnecessary features desabilitadas
- [ ] Error handling sem stack traces em producao
- [ ] Security headers configurados corretamente
- [ ] Cloud permissions revisadas (S3, Azure Blob)

## A06:2021 - Vulnerable Components
- [ ] SCA scan executado (Dependency-Check, Snyk, npm audit)
- [ ] Known CVEs em dependencies identificadas
- [ ] Component update plan definido

## A07-A10 Coverage
- [ ] A07: Authentication failures testadas (brute force, default creds)
- [ ] A08: Software integrity failures verificadas (CI/CD, deserialization)
- [ ] A09: Logging e monitoring gaps identificados
- [ ] A10: SSRF testada em todos os inputs que aceitam URLs

## Documentacao
- [ ] Coverage matrix OWASP Top 10 vs findings preenchida
- [ ] Gaps de cobertura identificados e documentados
- [ ] Cada finding mapeado ao OWASP Top 10 category
- [ ] Report inclui referencia ao OWASP Top 10 para cada finding
