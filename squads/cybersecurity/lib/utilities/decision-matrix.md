# Decision Matrix

Ferramenta para tomada de decisoes estruturadas em seguranca.

## Weighted Decision Matrix Template

| Criteria | Weight | Option A | Score A | Option B | Score B | Option C | Score C |
|----------|--------|----------|---------|----------|---------|----------|---------|
| Security Effectiveness | 30% | - | - | - | - | - | - |
| Total Cost of Ownership | 20% | - | - | - | - | - | - |
| Ease of Implementation | 15% | - | - | - | - | - | - |
| Integration Capability | 15% | - | - | - | - | - | - |
| Vendor Reputation | 10% | - | - | - | - | - | - |
| Scalability | 10% | - | - | - | - | - | - |
| **Weighted Total** | **100%** | - | **-** | - | **-** | - | **-** |

## Escala de Scoring

| Score | Descricao |
|-------|-----------|
| 5 | Excelente - atende e excede requisitos |
| 4 | Bom - atende todos os requisitos |
| 3 | Adequado - atende requisitos minimos |
| 2 | Fraco - gaps significativos |
| 1 | Inadequado - nao atende requisitos |

## Exemplo: Selecao de SIEM

| Criteria | Weight | Elastic SIEM | Splunk | Microsoft Sentinel |
|----------|--------|:---:|:---:|:---:|
| Detection Capability | 30% | 4 (1.2) | 5 (1.5) | 4 (1.2) |
| Total Cost | 20% | 5 (1.0) | 2 (0.4) | 3 (0.6) |
| Ease of Implementation | 15% | 3 (0.45) | 4 (0.6) | 4 (0.6) |
| Integration | 15% | 4 (0.6) | 4 (0.6) | 5 (0.75) |
| Community/Support | 10% | 4 (0.4) | 5 (0.5) | 4 (0.4) |
| Scalability | 10% | 4 (0.4) | 4 (0.4) | 5 (0.5) |
| **Total** | **100%** | - | **4.05** | **4.0** | **4.05** |

## Quando Usar

- Selecao de ferramentas e plataformas de seguranca
- Escolha entre estrategias de remediacao
- Priorizacao de projetos de seguranca
- Avaliacao de vendors e parceiros

## Processo

1. Definir criterios relevantes para a decisao
2. Atribuir pesos conforme importancia relativa
3. Avaliar cada opcao em cada criterio (1-5)
4. Calcular scores ponderados
5. Documentar racional no decisions-log
