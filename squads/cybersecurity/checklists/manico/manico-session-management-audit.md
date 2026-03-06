# Manico - Session Management Audit

Checklist para auditoria de gerenciamento de sessao.

## Session ID Generation
- [ ] Session ID gerado com CSPRNG (cryptographically secure)
- [ ] Entropia do session ID suficiente (128+ bits)
- [ ] Session ID nao contém dados de usuario (nao decodificavel)
- [ ] Session ID nao previsivel (sem sequential patterns)
- [ ] Session ID unico por sessao (sem reutilizacao)
- [ ] Novo session ID gerado apos autenticacao (session fixation prevention)

## Session Storage e Transport
- [ ] Session data armazenada server-side (nao em cookies)
- [ ] Cookie flags configurados: Secure, HttpOnly, SameSite
- [ ] Cookie path restrito ao necessario
- [ ] Cookie domain configurado corretamente (sem subdomain leaking)
- [ ] Session ID transmitido apenas via cookie (nao em URL)
- [ ] TLS enforced para todas as paginas autenticadas
- [ ] Cache-Control headers prevenindo caching de paginas sensiveis

## Session Lifecycle
- [ ] Session timeout configurado (idle timeout: 15-30 min)
- [ ] Absolute session timeout definido (max 8-24h)
- [ ] Logout funcional e destroi session server-side
- [ ] Session invalidada apos password change
- [ ] Session invalidada apos privilege change
- [ ] Concurrent session control implementado (se aplicavel)
- [ ] Session renewal periodica implementada

## Session Fixation Prevention
- [ ] Session ID regenerado apos login
- [ ] Session ID regenerado apos privilege escalation
- [ ] Pre-authentication session nao aceita apos autenticacao
- [ ] Fixation via cookie injection testada
- [ ] Fixation via URL parameter testada
- [ ] Fixation via meta tag/JavaScript testada

## Cross-Site Attacks
- [ ] CSRF tokens implementados em state-changing requests
- [ ] CSRF tokens unique per session e unpredictable
- [ ] SameSite cookie attribute configurado (Strict ou Lax)
- [ ] Double-submit cookie pattern implementado (se aplicavel)
- [ ] Custom header requirement para APIs (e.g., X-Requested-With)
- [ ] Referrer validation como defense-in-depth

## Token-Based Sessions (JWT/OAuth)
- [ ] JWT signature validated em cada request
- [ ] JWT expiration (exp) verificada e razoavel
- [ ] JWT algorithm fixo (nao permitir none ou switch)
- [ ] Refresh token armazenado de forma segura
- [ ] Token revocation mecanismo implementado
- [ ] Refresh token rotation implementada

## Documentacao
- [ ] Cada vulnerabilidade de session documentada com PoC
- [ ] Session configuration auditada e documentada
- [ ] Remediation steps especificos por finding
- [ ] OWASP ASVS V3 coverage documentada
- [ ] Report revisado por peer antes de entrega
