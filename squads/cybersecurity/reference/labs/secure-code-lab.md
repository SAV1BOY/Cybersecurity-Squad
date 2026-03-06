# Secure Code Lab - Ambiente de Codigo Seguro

## Objetivo
Ambiente para treinamento em secure coding, code review e demonstracao de
vulnerabilidades de aplicacao para developers e security champions.

## Aplicacoes Vulneraveis Hospedadas

### Web Applications
- **OWASP Juice Shop**: loja virtual com 100+ vulnerabilidades
- **OWASP WebGoat**: plataforma de aprendizado interativa
- **DVWA**: aplicacao PHP com niveis de dificuldade
- **HackTheBox Academy**: modulos de web security
- **Damn Vulnerable GraphQL Application**: vulns em GraphQL

### API Applications
- **OWASP crAPI**: Completely Ridiculous API
- **VAmPI**: Vulnerable API (Python)
- **Damn Vulnerable RESTaurant**: API REST vulneravel

### Mobile Applications
- **DIVA** (Damn Insecure and Vulnerable App) - Android
- **OWASP iGoat** - iOS
- **InsecureBankv2** - Android banking app

### Language-Specific
- **RailsGoat**: Ruby on Rails vulneravel
- **NodeGoat**: Node.js/Express vulneravel
- **DVNA**: Damn Vulnerable Node Application
- **WebGoat.NET**: .NET vulneravel

## Exercicios Estruturados

### Modulo 1: Input Validation
- SQL Injection (todos os tipos)
- Cross-Site Scripting (XSS)
- Command Injection
- Path Traversal
- LDAP Injection

### Modulo 2: Authentication & Session
- Broken authentication
- Session fixation e hijacking
- Insecure password storage
- MFA bypass techniques

### Modulo 3: Access Control
- IDOR (Insecure Direct Object Reference)
- Privilege escalation
- Missing function-level access control
- CORS misconfiguration

### Modulo 4: Secure Design Patterns
- Input validation frameworks
- Output encoding strategies
- Parameterized queries
- Secure session management
- Security headers implementation

## Code Review Exercises
- Repositorio com PRs contendo vulnerabilidades intencionais
- Exercicios de identificacao de security bugs
- Pratica com ferramentas SAST (Semgrep, CodeQL)
- Templates de code review checklist

## Integracoes
- CI/CD pipeline com security gates
- SAST integrado em pre-commit hooks
- SCA scanning em dependencias
- DAST automatizado pos-deploy

## Notas do Squad
O Secure Code Lab deve ser atualizado com vulnerabilidades novas
regularmente. Usar como base para workshops com times de desenvolvimento.
