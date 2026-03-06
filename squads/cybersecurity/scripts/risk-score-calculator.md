# Risk Score Calculator

Script para calcular risk scores de vulnerabilidades considerando contexto organizacional.

## Descricao

Calcula um risk score contextualizado que vai alem do CVSS base, incorporando fatores como criticidade do asset, exposicao, exploitability e valor para o negocio.

## Inputs

- `finding` - Dados do finding (CVSS base, tipo, descricao)
- `asset` - Dados do asset afetado (criticidade, exposicao, funcao)
- `threat_intel` - Informacoes de exploitability (exploit publico, ameaca ativa)
- `compensating_controls` - Controles mitigadores existentes

## Formula de Calculo

```
Risk Score = (CVSS_Base * Asset_Criticality * Exposure_Factor * Threat_Factor) / Control_Reduction

Onde:
- CVSS_Base: Score CVSS 3.1 (0.0 a 10.0)
- Asset_Criticality: Multiplicador do asset (0.5 a 2.0)
- Exposure_Factor: Nivel de exposicao (0.5 a 2.0)
- Threat_Factor: Ameaca ativa (1.0 a 2.0)
- Control_Reduction: Eficacia de controles compensatorios (1.0 a 3.0)
```

## Fatores Detalhados

### Asset Criticality
| Classificacao | Multiplicador |
|---------------|---------------|
| Tier 1 (critico) | 2.0 |
| Tier 2 (importante) | 1.5 |
| Tier 3 (padrao) | 1.0 |
| Tier 4 (baixo impacto) | 0.5 |

### Exposure Factor
| Exposicao | Multiplicador |
|-----------|---------------|
| Internet-facing | 2.0 |
| DMZ | 1.5 |
| Rede interna | 1.0 |
| Rede isolada | 0.5 |

### Threat Factor
| Condicao | Multiplicador |
|----------|---------------|
| Exploit ativo em campanhas | 2.0 |
| Exploit publico disponivel | 1.5 |
| PoC disponivel | 1.2 |
| Sem exploit conhecido | 1.0 |

### Control Reduction
| Controle | Divisor |
|----------|---------|
| Sem controles compensatorios | 1.0 |
| Controle detectivo ativo | 1.5 |
| Controle preventivo parcial | 2.0 |
| Controle preventivo completo | 3.0 |

## Output

```
Finding: FIND-023 (CVE-2026-1234)
CVSS Base: 8.1
Asset: portal-web (Tier 1, Internet-facing)
Threat: Exploit publico disponivel
Controls: WAF ativo (preventivo parcial)

Risk Score: (8.1 * 2.0 * 2.0 * 1.5) / 2.0 = 24.3
Risk Level: CRITICAL (>20)
```

## Classificacao Final

| Risk Score | Nivel |
|------------|-------|
| > 20 | Critical |
| 10 - 20 | High |
| 5 - 10 | Medium |
| < 5 | Low |
