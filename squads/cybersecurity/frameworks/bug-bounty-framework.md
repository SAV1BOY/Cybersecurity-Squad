# Bug Bounty Framework — Framework Interno

> Como criar e gerenciar um programa de bug bounty efetivo.

## Objetivo

Bug bounty e um canal adicional de descoberta de vulnerabilidades, complementar ao pentest e code review internos. Nao substitui seguranca interna — complementa com perspectivas externas e diversidade de skill.

## Componentes

### 1. Scope Definition
```
In-scope:
- Aplicacoes web de producao (listar dominos)
- APIs publicas (listar endpoints base)
- Mobile apps (iOS/Android)

Out-of-scope:
- Infraestrutura interna
- Engenharia social contra funcionarios
- DoS/DDoS
- Testes automatizados massivos (scanners)
- Ambientes de staging/dev
- Third-party services
```

### 2. Severity & Reward Table
| Severidade | Descricao | Reward Range |
|------------|-----------|--------------|
| Critical | RCE, auth bypass, data breach | R$ 5.000 - R$ 20.000 |
| High | SQLi, IDOR com dados sensiveis, priv esc | R$ 2.000 - R$ 5.000 |
| Medium | XSS stored, CSRF com impacto, info disclosure significativo | R$ 500 - R$ 2.000 |
| Low | XSS reflected, info disclosure menor | R$ 100 - R$ 500 |

### 3. Rules of Engagement
- Nao acessar dados de outros usuarios
- Nao modificar ou deletar dados
- Nao degradar performance dos servicos
- Reportar imediatamente findings criticos
- Nao divulgar publicamente antes da correcao (90 dias)

### 4. Triage Process
```
1. Report recebido (< 24h para acknowledge)
2. Triage: valido / duplicata / out-of-scope / informativo
3. Validacao: reproduzir internamente
4. Severity assessment: usando risk-scoring-model
5. Reward decision: baseado em severity + quality do report
6. Fix: encaminhar ao dev team
7. Retest: validar correcao
8. Close: pagar reward + agradecer
```

### 5. Quality Gates
- Report deve ter: descricao clara + PoC + impacto
- Duplicatas: primeiro report valido recebe reward
- Known issues: manter lista atualizada de known issues
- Reward bonus: por report quality excepcional

## Anti-Patterns

- **Scope muito amplo sem readiness**: Nao abrir bug bounty antes de fazer pentest interno
- **Triage lento**: > 5 dias sem resposta = pesquisadores desistem
- **Reward baixo demais**: Pesquisadores bons vao para programas que pagam mais
- **Ignorar reports**: Destrui reputacao rapidamente
- **Sem fix SLA**: Bug bounty sem correcao e dinheiro jogado fora
