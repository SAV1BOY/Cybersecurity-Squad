# Code Review Security Quality Gate

Checklist de qualidade para revisao de seguranca de codigo.

## Preparacao
- [ ] Repositorio clonado e ambiente de build funcional
- [ ] SAST tools configurados (Semgrep, SonarQube, CodeQL, Checkmarx)
- [ ] Linguagem e frameworks identificados para regras customizadas
- [ ] Threat model da aplicacao revisado para focar review
- [ ] Versao/commit do codigo documentado para rastreabilidade

## Analise Automatizada
- [ ] SAST scan executado com resultados triados
- [ ] SCA (Software Composition Analysis) executado para dependencies
- [ ] Secret scanning realizado (git-secrets, truffleHog, gitleaks)
- [ ] License compliance verificada para third-party libraries
- [ ] Custom rules aplicadas para padroes internos

## Input Validation e Injection
- [ ] User input sanitization verificada em todos os entry points
- [ ] Parameterized queries utilizadas para database access
- [ ] Output encoding aplicado para prevenir XSS
- [ ] Command injection prevention verificada
- [ ] Path traversal prevention verificada
- [ ] Deserialization safety verificada

## Authentication e Authorization
- [ ] Password hashing com algoritmo seguro (bcrypt, Argon2)
- [ ] Session management implementation revisada
- [ ] Authorization checks presentes em todos os endpoints
- [ ] Token generation com CSPRNG verificada
- [ ] OAuth/OIDC implementation seguindo best practices

## Criptografia e Data Protection
- [ ] Encryption algorithms atuais e seguros (AES-256, ChaCha20)
- [ ] Key management sem hardcoded keys
- [ ] Random number generation com CSPRNG
- [ ] Sensitive data nao logada ou exposta em error messages
- [ ] PII handling conforme regulamentacao (LGPD, GDPR)

## Error Handling e Logging
- [ ] Exception handling sem information disclosure
- [ ] Security events logados (auth failures, access denied)
- [ ] Logging sem sensitive data (passwords, tokens, PII)
- [ ] Stack traces desabilitados em producao

## Documentacao e Entrega
- [ ] Findings categorizados por CWE
- [ ] Code snippets incluidos para cada finding
- [ ] Fix recommendations com code examples
- [ ] Severity e exploitability avaliados
- [ ] Report revisado por peer com expertise na linguagem
