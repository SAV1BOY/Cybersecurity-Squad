# Manico - AuthN/AuthZ Audit

Checklist para auditoria de autenticacao e autorizacao.

## Autenticacao - Design
- [ ] Authentication mechanism documentado (form-based, SSO, MFA)
- [ ] Password policy conforme NIST 800-63B (min 8 chars, no complexity rules)
- [ ] Account lockout/throttling implementado contra brute force
- [ ] Multi-factor authentication disponivel e recomendado
- [ ] Password recovery flow seguro (no security questions)
- [ ] Registration flow protegido contra abuse

## Autenticacao - Implementacao
- [ ] Passwords armazenados com hash seguro (bcrypt, Argon2id, scrypt)
- [ ] Salt unico por usuario gerado via CSPRNG
- [ ] Timing-safe comparison para verificacao de credenciais
- [ ] Username enumeration prevenida (mesma resposta para valid/invalid)
- [ ] Login rate limiting implementado por IP e por conta
- [ ] Credential stuffing protection implementada
- [ ] Remember-me token seguro (random, httpOnly, secure, expiry)

## Multi-Factor Authentication
- [ ] MFA implementation revisada para bypass vulnerabilities
- [ ] TOTP implementation conforme RFC 6238
- [ ] MFA recovery codes gerados de forma segura
- [ ] MFA enrollment flow protegido (requer autenticacao previa)
- [ ] MFA bypass via session fixation testado
- [ ] Fallback authentication sem MFA nao disponivel

## Autorizacao - Design
- [ ] Authorization model documentado (RBAC, ABAC, ACL)
- [ ] Roles e permissions mapeados completamente
- [ ] Separation of duties implementada para operacoes criticas
- [ ] Default deny policy aplicada (deny unless explicitly allowed)
- [ ] Privilege escalation paths eliminados by design

## Autorizacao - Implementacao
- [ ] Authorization checks em cada endpoint (nao apenas UI)
- [ ] Server-side enforcement (nao depende de client-side)
- [ ] Horizontal privilege escalation testada (IDOR)
- [ ] Vertical privilege escalation testada (role manipulation)
- [ ] Direct object references protegidas com access control
- [ ] Admin functions segregadas e protegidas
- [ ] Authorization bypass via parameter tampering testado

## Token e Session Management
- [ ] JWT validation completa (signature, expiry, issuer, audience)
- [ ] JWT algorithm confusion prevenida (RS256 vs HS256)
- [ ] OAuth2 implementation conforme RFC 6749
- [ ] PKCE implementado para public clients
- [ ] Token revocation funcional e testada
- [ ] Refresh token rotation implementada

## Documentacao
- [ ] Matriz de autorizacao (roles x permissions) documentada
- [ ] Findings categorizados por AuthN vs AuthZ
- [ ] PoC para cada bypass encontrado
- [ ] Remediation recommendations alinhadas com OWASP ASVS
