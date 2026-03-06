# Web Application Assessment Quality Gate

Checklist de qualidade para avaliacao de seguranca de aplicacoes web.

## Reconhecimento da Aplicacao
- [ ] Application mapping completo (sitemap, endpoints, parameters)
- [ ] Technology stack identificado (framework, server, DB, WAF)
- [ ] Authentication mechanisms documentados
- [ ] User roles e privilege levels mapeados
- [ ] Business logic flows documentados

## OWASP Top 10 Coverage
- [ ] Injection testing realizado (SQL, NoSQL, LDAP, OS command)
- [ ] Broken Authentication verificado (brute force, session fixation, credential stuffing)
- [ ] Sensitive Data Exposure testado (data in transit, at rest)
- [ ] XML External Entities (XXE) testado
- [ ] Broken Access Control verificado (IDOR, privilege escalation, forced browsing)
- [ ] Security Misconfiguration auditada (headers, error handling, defaults)
- [ ] Cross-Site Scripting (XSS) testado (reflected, stored, DOM-based)
- [ ] Insecure Deserialization verificada
- [ ] Components with Known Vulnerabilities identificados
- [ ] Insufficient Logging & Monitoring avaliado

## Testes Complementares
- [ ] CSRF protection validada em todas as state-changing operations
- [ ] File upload security testada (type bypass, path traversal, webshell)
- [ ] CORS policy analisada e testada
- [ ] CSP (Content Security Policy) header revisado
- [ ] HTTP security headers verificados (HSTS, X-Frame-Options, etc.)
- [ ] Session management auditada (timeout, rotation, secure flags)
- [ ] Rate limiting testado em endpoints criticos
- [ ] WebSocket security verificada (se aplicavel)

## Evidencias e Documentacao
- [ ] PoC reproduzivel para cada vulnerability encontrada
- [ ] Request/Response capturados para cada finding
- [ ] Business impact descrito para cada vulnerabilidade
- [ ] Remediation guidance especifica por finding
- [ ] OWASP ASVS level de cobertura documentado

## Entrega
- [ ] Peer review do report realizado
- [ ] Raw Burp/ZAP project file salvo como backup
- [ ] Findings priorizados por risco de negocio
