# AppSec - API Security Gate

Checklist de quality gate para seguranca de APIs.

## API Design Security
- [ ] OpenAPI/Swagger spec revisada para security concerns
- [ ] Authentication obrigatoria em todos os endpoints (exceto public)
- [ ] Authorization model definido e consistente
- [ ] Rate limiting definido por endpoint e por usuario
- [ ] Input validation schemas definidos para cada endpoint
- [ ] Error response format padronizado sem information disclosure
- [ ] API versioning strategy definida

## OWASP API Security Top 10 Coverage
- [ ] API1: Broken Object Level Authorization (BOLA) testado
- [ ] API2: Broken Authentication testada
- [ ] API3: Broken Object Property Level Authorization testada
- [ ] API4: Unrestricted Resource Consumption verificado
- [ ] API5: Broken Function Level Authorization testada
- [ ] API6: Unrestricted Access to Sensitive Business Flows verificado
- [ ] API7: Server Side Request Forgery (SSRF) testada
- [ ] API8: Security Misconfiguration verificada
- [ ] API9: Improper Inventory Management verificado
- [ ] API10: Unsafe Consumption of APIs verificado

## Autenticacao e Autorizacao
- [ ] OAuth2/OIDC implementation revisada
- [ ] JWT validation completa (sig, exp, iss, aud, nbf)
- [ ] API key management seguro (rotation, revocation)
- [ ] Scope-based authorization implementada
- [ ] Token expiration adequada (short-lived access tokens)
- [ ] Refresh token rotation implementada
- [ ] mTLS implementado para service-to-service (se aplicavel)

## Input e Output
- [ ] Content-Type enforcement habilitado
- [ ] Request body size limits definidos
- [ ] Response filtering implementada (no excessive data)
- [ ] GraphQL depth/complexity limits (se aplicavel)
- [ ] File upload via API seguro
- [ ] Pagination implementada para prevent data dump

## Infrastructure
- [ ] HTTPS enforced para todos os endpoints
- [ ] CORS policy restritiva e adequada
- [ ] API gateway com WAF configurado
- [ ] Rate limiting e throttling enforced
- [ ] API monitoring e alerting configurados
- [ ] API versioning sem exposicao de deprecated endpoints

## Documentacao e Teste
- [ ] API inventory atualizado (nenhuma shadow API)
- [ ] Security test cases para cada endpoint
- [ ] Automated security testing integrado ao CI/CD
- [ ] Pen test realizado em API criticas
- [ ] Report de seguranca API entregue com findings
- [ ] Remediation plan definido e rastreado
