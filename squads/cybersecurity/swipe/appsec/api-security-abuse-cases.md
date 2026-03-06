# API Security Abuse Cases

Casos de abuso em APIs e padroes de protecao baseados no OWASP API Security Top 10.

## BOLA - Broken Object Level Authorization

**Cenario:** Atacante altera `GET /api/orders/123` para `/api/orders/124` e acessa pedidos de outros usuarios.
**Impacto:** Acesso nao autorizado a dados de qualquer usuario.
**Protecao:** Validar ownership do recurso em cada request server-side.

## BFLA - Broken Function Level Authorization

**Cenario:** Usuario regular descobre `DELETE /api/admin/users/456` e executa operacao administrativa.
**Impacto:** Privilege escalation para funcoes administrativas.
**Protecao:** RBAC granular em cada endpoint, nao apenas na UI.

## Mass Assignment

**Cenario:** `PUT /api/profile` aceita `{"name":"João","role":"admin"}` e altera role.
**Impacto:** Elevacao de privilegio via campos nao esperados.
**Protecao:** Allowlist de campos aceitos por endpoint, nunca bind direto do request body.

## Rate Limiting Bypass

**Cenario:** Atacante distribui requests entre multiplos IPs para bypass de rate limit.
**Protecao:** Rate limit por API key/user alem de IP. Implementar exponential backoff.

## Padroes de Protecao Universais

- Autenticacao via OAuth 2.0 + JWT com expiracao curta
- API Gateway com rate limiting, throttling e WAF
- Logging de todos os requests para auditoria
- Schema validation rigorosa (OpenAPI spec enforcement)
- Versionamento de API com deprecation policy
- Monitoramento de anomalias no padrao de uso

## Ferramentas de Teste

- Burp Suite para interceptacao e manipulacao de requests
- Postman collections com testes de autorizacao automatizados
- OWASP ZAP para scanning automatizado de APIs
