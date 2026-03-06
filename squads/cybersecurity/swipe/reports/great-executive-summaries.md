# Great Executive Summaries

Exemplos de executive summaries que comunicam risco de forma clara para stakeholders nao-tecnicos.

## Estrutura Recomendada

1. **Objetivo do Assessment** - Uma frase descrevendo escopo e motivacao
2. **Risk Posture Overview** - Classificacao geral (Critical/High/Medium/Low)
3. **Top Findings** - 3-5 achados mais impactantes em linguagem de negocio
4. **Business Impact** - Traducao de vulnerabilidades em risco financeiro/operacional
5. **Recommended Actions** - Proximos passos priorizados por impacto

## Exemplo: Pentest de Aplicacao Web

> "Durante o periodo de 10 dias, identificamos 3 vulnerabilidades criticas que permitiriam
> acesso nao-autorizado a dados de 500k clientes. O risco estimado de breach e de R$2.4M.
> Recomendamos remediation imediata dos findings criticos em ate 72 horas."

## Padroes de Qualidade

- Evitar jargao tecnico sem contexto de negocio
- Incluir metricas quantificaveis (numero de findings, CVSS scores agregados)
- Usar visual risk matrix para facilitar compreensao
- Comparar com benchmarks do setor quando disponivel
- Limitar a 1-2 paginas no maximo

## Anti-Patterns

- Executive summary com mais de 2 paginas
- Listar CVEs sem explicar impacto de negocio
- Usar linguagem alarmista sem dados de suporte
- Omitir recomendacoes acionaveis
- Nao incluir timeline de remediation sugerida
