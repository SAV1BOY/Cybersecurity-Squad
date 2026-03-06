# API Security Assessment Quality Gate

Checklist de qualidade para avaliacao de seguranca de APIs.

## Descoberta e Documentacao da API
- [ ] API documentation (Swagger/OpenAPI) obtida ou gerada
- [ ] Todos os endpoints enumerados e catalogados
- [ ] HTTP methods suportados por endpoint documentados
- [ ] Request/response schemas validados
- [ ] API versioning strategy identificada
- [ ] Rate limiting e throttling policies documentadas

## Autenticacao e Autorizacao
- [ ] Authentication mechanism testado (OAuth2, JWT, API Key, mTLS)
- [ ] Token validation verificada (expiry, signature, revocation)
- [ ] Broken Object Level Authorization (BOLA/IDOR) testado
- [ ] Broken Function Level Authorization verificado
- [ ] Mass Assignment vulnerabilities testadas
- [ ] JWT implementation auditada (algorithm confusion, none alg, weak secrets)
- [ ] API key exposure verificada em client-side code e repos

## Input Validation e Injection
- [ ] SQL injection testado em todos os parametros
- [ ] NoSQL injection testado (se aplicavel)
- [ ] Server-Side Request Forgery (SSRF) testado
- [ ] GraphQL injection e introspection testados (se aplicavel)
- [ ] Parameter tampering verificado em todos os endpoints
- [ ] Content-type validation testada (JSON, XML, multipart)

## Business Logic e Data
- [ ] Business logic flaws testados em fluxos criticos
- [ ] Excessive Data Exposure verificado em responses
- [ ] Pagination e data filtering bypass testados
- [ ] Batch/bulk operations testadas para abuse
- [ ] Race conditions testadas em operacoes concorrentes

## Seguranca de Infraestrutura
- [ ] TLS configuration validada (versao, cipher suites)
- [ ] CORS policy testada para API endpoints
- [ ] Error handling verificado (no stack traces, verbose errors)
- [ ] Security headers presentes em API responses
- [ ] Logging de API calls verificado para auditoria

## Documentacao e Entrega
- [ ] OWASP API Security Top 10 cobertura documentada
- [ ] Postman/Insomnia collection exportada com test cases
- [ ] PoC requests documentados para cada finding
- [ ] Remediation recommendations especificas por endpoint
- [ ] Severity ratings validados com CVSS contextual
