# Risk Matrix

Matriz de risco para avaliacao padronizada de likelihood vs impact.

## Matriz 5x5

|                    | Negligible (1) | Minor (2) | Moderate (3) | Major (4) | Catastrophic (5) |
|--------------------|:-:|:-:|:-:|:-:|:-:|
| Almost Certain (5) | 5 Medium | 10 High | 15 Critical | 20 Critical | 25 Critical |
| Likely (4)         | 4 Low | 8 Medium | 12 High | 16 Critical | 20 Critical |
| Possible (3)       | 3 Low | 6 Medium | 9 Medium | 12 High | 15 Critical |
| Unlikely (2)       | 2 Low | 4 Low | 6 Medium | 8 Medium | 10 High |
| Rare (1)           | 1 Low | 2 Low | 3 Low | 4 Low | 5 Medium |

## Definicoes de Likelihood

| Level | Descricao | Frequencia Estimada |
|-------|-----------|-------------------|
| 5 - Almost Certain | Esperado que ocorra em breve | > 1x por mes |
| 4 - Likely | Provavelmente ocorrera | 1x por trimestre |
| 3 - Possible | Pode ocorrer em algum momento | 1x por ano |
| 2 - Unlikely | Improvavel mas possivel | 1x a cada 3 anos |
| 1 - Rare | Excepcional, apenas em circunstancias extremas | 1x a cada 5+ anos |

## Definicoes de Impact

| Level | Financeiro | Dados | Reputacao | Operacional |
|-------|-----------|-------|-----------|-------------|
| 5 - Catastrophic | > R$10M | Breach massivo de dados regulados | Cobertura nacional | Interrupcao > 1 semana |
| 4 - Major | R$1M-10M | Exposicao de PII significativa | Cobertura setorial | Interrupcao 1-7 dias |
| 3 - Moderate | R$100K-1M | Dados internos expostos | Reclamacoes de clientes | Interrupcao 4-24h |
| 2 - Minor | R$10K-100K | Dados nao sensiveis | Impacto interno | Interrupcao 1-4h |
| 1 - Negligible | < R$10K | Sem exposicao de dados | Sem impacto | Interrupcao < 1h |

## Apetite de Risco

| Risk Score | Tratamento |
|-----------|------------|
| 15-25 (Critical) | Acao imediata obrigatoria, escalacao ao CISO |
| 8-14 (High) | Plano de mitigacao em 30 dias |
| 4-7 (Medium) | Monitorar e mitigar em 90 dias |
| 1-3 (Low) | Aceitar ou mitigar no proximo ciclo |
