# Risk Rating Component

Componente padronizado para calculo e comunicacao de risk rating.

## Metodologia CVSS v3.1

### Base Score Metrics
- **Attack Vector (AV)**: Network, Adjacent, Local, Physical
- **Attack Complexity (AC)**: Low, High
- **Privileges Required (PR)**: None, Low, High
- **User Interaction (UI)**: None, Required
- **Scope (S)**: Unchanged, Changed
- **Confidentiality (C)**: None, Low, High
- **Integrity (I)**: None, Low, High
- **Availability (A)**: None, Low, High

### Faixas de Severidade
| Score | Severity | Cor |
|-------|----------|-----|
| 9.0 - 10.0 | Critical | Vermelho escuro |
| 7.0 - 8.9 | High | Vermelho |
| 4.0 - 6.9 | Medium | Laranja |
| 0.1 - 3.9 | Low | Amarelo |
| 0.0 | Informational | Azul |

## Ajuste Contextual

Alem do CVSS base, considerar fatores contextuais:

| Fator | Ajuste |
|-------|--------|
| Ativo em producao vs staging | +/- 1 nivel |
| Dados regulados envolvidos | + 1 nivel |
| Exploit publico disponivel | + 1 nivel |
| Controle compensatorio existente | - 1 nivel |
| Exposicao a internet | + 1 nivel |

## Comunicacao de Risco

Para audiencia tecnica: usar CVSS score com vector string completo.
Para audiencia executiva: usar categorias (Critical/High/Medium/Low)
com descricao de impacto de negocio em linguagem acessivel.

## Template de Justificativa

```
Severity: High (CVSS 7.5)
Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
Justificativa: Exploravel remotamente sem autenticacao,
com impacto em confidencialidade de dados sensiveis.
```
