# Task: API Security Review

## Objetivo
Avaliar a seguranca de APIs expostas, identificando vulnerabilidades de autenticacao, autorizacao, input validation e configuracao contra OWASP API Top 10.

## Agents
- **jim-manico** (lead) — Conduz revisao de seguranca de APIs
- **fuzzer** (executor) — Executa fuzzing em endpoints de API

## Inputs
- Documentacao de APIs (OpenAPI/Swagger, GraphQL schema)
- Attack surface map com APIs identificadas
- OWASP API Top 10 como referencia
- Credenciais de teste (se grey/white-box)

## Steps
1. Inventariar todos os endpoints de API in-scope
2. Analisar mecanismos de autenticacao (OAuth, JWT, API keys)
3. Testar autorizacao em todos os endpoints (BOLA, BFLA)
4. Verificar rate limiting e throttling em endpoints criticos
5. Executar fuzzing em parametros de input
6. Testar mass assignment e excessive data exposure
7. Verificar security headers e CORS configuration
8. Avaliar error handling e information disclosure
9. Testar injection vulnerabilities (SQLi, NoSQLi, command injection)
10. Registrar findings no `findings-registry`

## Output
- Relatorio de API security review com findings classificados
- Lista de vulnerabilidades mapeadas contra OWASP API Top 10
- Recomendacoes de remediacao por endpoint
- Evidencias de testes com requests/responses

## Quality Gates
- [ ] Todos os endpoints de API in-scope testados
- [ ] OWASP API Top 10 verificado sistematicamente
- [ ] Autenticacao e autorizacao testados em cada endpoint
- [ ] Rate limiting verificado em endpoints criticos
- [ ] Fuzzing executado em parametros de input
- [ ] Checklist `api-security-assessment-quality` atendido
- [ ] Checklist `appsec-api-security-gate` validado

## Routing & Escalation
- **frameworks**: owasp-api-top-10, api-security-testing-methodology
- **checklists**: api-security-assessment-quality, appsec/appsec-api-security-gate
- **templates**: reports/finding-template
- **registry**: data/registries/findings-registry
- **receives_from**: discovery/threat-modeling
- **delivers_to**: findings-review
