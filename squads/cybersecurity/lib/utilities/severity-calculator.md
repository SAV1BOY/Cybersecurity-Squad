# Severity Calculator

Utilitario para calculo padronizado de severidade de findings de seguranca.

## Metodologia CVSS v3.1

### Passo 1: Base Score Metrics

| Metric | Values | Weight |
|--------|--------|--------|
| Attack Vector (AV) | Network (0.85) / Adjacent (0.62) / Local (0.55) / Physical (0.20) | Alto |
| Attack Complexity (AC) | Low (0.77) / High (0.44) | Medio |
| Privileges Required (PR) | None (0.85) / Low (0.62/0.68) / High (0.27/0.50) | Alto |
| User Interaction (UI) | None (0.85) / Required (0.62) | Medio |
| Scope (S) | Unchanged / Changed | Modificador |
| Confidentiality (C) | High (0.56) / Low (0.22) / None (0) | Alto |
| Integrity (I) | High (0.56) / Low (0.22) / None (0) | Alto |
| Availability (A) | High (0.56) / Low (0.22) / None (0) | Medio |

### Passo 2: Calculo

```
ISS = 1 - [(1-C) x (1-I) x (1-A)]

Se Scope = Unchanged:
  Impact = 6.42 x ISS
Se Scope = Changed:
  Impact = 7.52 x [ISS - 0.029] - 3.25 x [ISS - 0.02]^15

Exploitability = 8.22 x AV x AC x PR x UI

Se Impact <= 0: Base Score = 0
Se Scope = Unchanged: Base Score = min(Impact + Exploitability, 10)
Se Scope = Changed: Base Score = min(1.08 x (Impact + Exploitability), 10)
```

### Passo 3: Ajuste Contextual

| Fator Contextual | Ajuste |
|-------------------|--------|
| Exploit disponivel publicamente | +0.5 a +1.0 |
| Ativo em producao com dados regulados | +0.5 |
| Controle compensatorio efetivo | -0.5 a -1.0 |
| Exposicao limitada (rede interna) | -0.5 |

## Tabela de Referencia Rapida

| Cenario Comum | CVSS Tipico | Severity |
|---------------|-------------|----------|
| RCE sem autenticacao | 9.8 | Critical |
| SQL Injection com exfiltracao | 9.1 | Critical |
| SSRF para rede interna | 7.5 | High |
| Stored XSS | 6.1 | Medium |
| Information disclosure | 5.3 | Medium |
| Missing security headers | 3.0 | Low |

## Notas

Sempre documentar o vector string completo para transparencia.
Em caso de duvida, discutir com peer antes de finalizar o rating.
