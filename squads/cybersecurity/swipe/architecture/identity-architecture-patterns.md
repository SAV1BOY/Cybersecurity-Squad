# Identity Architecture Patterns

Padroes de arquitetura de identidade para autenticacao e autorizacao robustas.

## Centralized Identity Provider (IdP)

```
[Users] -> [IdP (Okta/Azure AD)] -> [SAML/OIDC] -> [Applications]
                |
          [MFA Engine]
                |
          [Conditional Access]
                |
          [Risk Engine]
```

**Beneficios:** Single pane of glass, politicas uniformes, audit trail centralizado.

## Padroes de Autorizacao

### RBAC (Role-Based Access Control)
- Roles mapeados para funcoes de negocio (Analyst, Manager, Admin)
- Adequado para organizacoes com hierarquia bem definida
- Risco: role explosion em organizacoes grandes

### ABAC (Attribute-Based Access Control)
- Decisoes baseadas em atributos (departamento, projeto, horario, device)
- Mais granular que RBAC, porem mais complexo
- Ideal para ambientes cloud-native e microsservicos

### ReBAC (Relationship-Based Access Control)
- Autorizacao baseada em relacionamento entre entidades
- Exemplo: "usuario pode editar documento SE e owner OU membro do time"
- Implementacoes: Google Zanzibar, OpenFGA, SpiceDB

## Privileged Access Management (PAM)

- Just-in-Time (JIT) elevation com aprovacao e TTL
- Session recording para acesso administrativo
- Credential vaulting com rotacao automatica
- Break-glass procedures para emergencias

## Service Identity

- Service accounts com credenciais rotacionadas automaticamente
- Workload identity federation (sem long-lived credentials)
- mTLS entre microsservicos com certificate rotation
- API keys com scoping granular e expiracao

## Anti-Patterns

- Shared accounts entre multiplos usuarios
- Long-lived API keys sem rotacao
- Service accounts com admin privileges
- MFA bypass para "conveniencia"
