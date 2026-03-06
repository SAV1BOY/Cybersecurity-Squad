# Threat Model Examples

Exemplos praticos de threat modeling usando diferentes metodologias.

## STRIDE Model - Aplicacao Web E-Commerce

| Categoria | Ameaca | Mitigacao |
|-----------|--------|-----------|
| Spoofing | Roubo de session token | Secure cookies, session timeout, MFA |
| Tampering | Manipulacao de preco no cart | Validacao server-side de precos |
| Repudiation | Usuario nega transacao | Audit logging com integridade |
| Info Disclosure | Leak de dados de cartao | Tokenizacao, PCI-DSS compliance |
| DoS | Flood no checkout | Rate limiting, CDN, auto-scaling |
| Elevation | Acesso admin via IDOR | RBAC, authorization checks |

## Data Flow Diagram (DFD) - Componentes

```
[Browser] --> [CDN/WAF] --> [Load Balancer] --> [App Server]
                                                     |
                                              [Database] [Cache]
                                                     |
                                              [Payment Gateway]
```

**Trust Boundaries:**
- Internet -> WAF (boundary 1)
- WAF -> App Server (boundary 2)
- App Server -> Database (boundary 3)
- App Server -> Payment Gateway (boundary 4)

## PASTA Methodology (7 Stages)

1. Definir objetivos de negocio
2. Definir escopo tecnico
3. Decompor a aplicacao
4. Analisar ameacas (threat intelligence)
5. Analisar vulnerabilidades
6. Modelar ataques (attack trees)
7. Analisar risco e definir controles

## Quando Fazer Threat Modeling

- Novos projetos ou features significativas
- Mudancas em arquitetura ou data flows
- Integracao com novos third-party services
- Apos incidente de seguranca relevante
- Revisao periodica anual de sistemas criticos
