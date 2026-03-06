# OWASP - Indice de Referencia

## Visao Geral
O Open Worldwide Application Security Project (OWASP) e a principal referencia
aberta para seguranca de aplicacoes. O squad utiliza projetos OWASP como base
para atividades de AppSec.

## Projetos Flagship

### OWASP Top 10 (2021)
Lista das 10 categorias de risco mais criticas para aplicacoes web:
1. A01 - Broken Access Control
2. A02 - Cryptographic Failures
3. A03 - Injection
4. A04 - Insecure Design
5. A05 - Security Misconfiguration
6. A06 - Vulnerable and Outdated Components
7. A07 - Identification and Authentication Failures
8. A08 - Software and Data Integrity Failures
9. A09 - Security Logging and Monitoring Failures
10. A10 - Server-Side Request Forgery (SSRF)

### OWASP ASVS (Application Security Verification Standard)
- Framework de requisitos de seguranca para aplicacoes
- 3 niveis: L1 (oportunista), L2 (padrao), L3 (avancado)
- Uso: definir requisitos de seguranca e scope de testes

### OWASP SAMM (Software Assurance Maturity Model)
- Modelo de maturidade para seguranca de software
- 5 business functions, 15 security practices
- Uso: avaliar e melhorar programa de AppSec

### OWASP Testing Guide (WSTG)
- Metodologia completa para testes de seguranca de aplicacoes
- Cobertura: information gathering, configuration, identity management,
  authentication, authorization, session management, input validation,
  error handling, cryptography, business logic, client-side

### OWASP Cheat Sheet Series
- Guias praticos e concisos para developers
- Topicos: authentication, session management, XSS prevention,
  SQL injection prevention, CSRF prevention e dezenas mais

## Outros Projetos Relevantes
- **OWASP ZAP**: ferramenta de teste de seguranca de aplicacoes web
- **OWASP Dependency-Check**: analise de componentes vulneraveis
- **OWASP ModSecurity Core Rule Set**: regras WAF
- **OWASP API Security Top 10**: riscos especificos de APIs
- **OWASP Mobile Top 10**: riscos para aplicacoes moveis

## Como o Squad Aplica
- **Pentest Methodology**: WSTG como base para testes web
- **Requirements**: ASVS para definir requisitos de seguranca
- **Training**: Top 10 e Cheat Sheets para developers
- **Maturity**: SAMM para avaliar programas de AppSec
- **Tooling**: ZAP e Dependency-Check em pipelines CI/CD

## Notas do Squad
OWASP e community-driven e gratuito. Contribuir de volta com traducoes
para portugues e participar de capitulos locais no Brasil.
