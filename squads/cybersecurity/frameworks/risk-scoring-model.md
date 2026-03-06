# Risk Scoring Model — Framework Interno

> Como o squad classifica risco: impacto x probabilidade x detectabilidade x esforco.

## Objetivo

Modelo padronizado de scoring de risco para todos os findings do squad. Substitui o "High/Medium/Low" subjetivo por um modelo multidimensional que considera contexto real.

## Formula

```
Risk Score = Impacto x Probabilidade x (1 - Detectabilidade) x Facilidade
```

Cada fator e avaliado de 1 a 5:

### Impacto (ao negocio)
| Score | Descricao |
|-------|-----------|
| 5 | Catastrofico: breach massivo, regulatorio, existencial |
| 4 | Severo: perda financeira significativa, dados sensiveis expostos |
| 3 | Moderado: disrupcao operacional, dados internos expostos |
| 2 | Menor: impacto limitado, sem dados sensiveis |
| 1 | Insignificante: teorico, sem impacto pratico |

### Probabilidade (de exploracao real)
| Score | Descricao |
|-------|-----------|
| 5 | Quase certo: exploit publico, trivial, internet-facing |
| 4 | Provavel: exploit disponivel, requer pouca customizacao |
| 3 | Possivel: requer conhecimento, mas factivel |
| 2 | Improvavel: requer acesso privilegiado + skill avancado |
| 1 | Raro: cenario teorico, dependencias multiplas |

### Detectabilidade (defesas atuais detectariam?)
| Score | Descricao |
|-------|-----------|
| 5 | Alta: regras ativas, alertas configurados, testados |
| 4 | Boa: cobertura parcial, alertas existem |
| 3 | Media: logs existem mas sem regra especifica |
| 2 | Baixa: logs parciais, sem alerta |
| 1 | Nenhuma: sem visibilidade, blind spot |

### Facilidade (para o atacante)
| Score | Descricao |
|-------|-----------|
| 5 | Trivial: script kiddie, ferramenta automatizada |
| 4 | Facil: atacante intermediario, 1-2 passos |
| 3 | Moderado: requer planejamento e skill |
| 2 | Dificil: requer expertise e multiplos passos |
| 1 | Muito dificil: APT-level, recursos significativos |

## Severidade Final

| Score Range | Severidade | SLA de Correcao |
|-------------|------------|-----------------|
| 75-125 | Critical | 72 horas |
| 40-74 | High | 2 semanas |
| 15-39 | Medium | 30 dias |
| 5-14 | Low | 90 dias |
| 1-4 | Informational | Backlog |

## Contexto Adicional

O score numerico e o ponto de partida. Sempre considerar:
- **Exposicao**: Internet-facing vs. interno vs. air-gapped
- **Dados**: Tipo de dados acessiveis (PII, financeiro, saude, credentials)
- **Blast radius**: Quantos sistemas/usuarios sao afetados
- **Chained risk**: Este finding habilita outros ataques?
- **Business context**: E um sistema critico para o negocio?

## Uso no Squad

1. Todo finding usa este modelo no campo "Risk Assessment"
2. Remediation priority segue o SLA definido
3. Exceptions documentadas no exception-registry com justificativa
4. Review trimestral dos scores para calibracao
