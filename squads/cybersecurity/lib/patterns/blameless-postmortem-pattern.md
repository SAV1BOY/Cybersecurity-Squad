# Blameless Postmortem Pattern

Padrao para conducao de post-mortems focados em melhoria de processos, nao em culpa.

## Principio

Incidentes sao sintomas de falhas sistemicas, nao de erros individuais.
O objetivo do postmortem e melhorar o sistema, nao punir pessoas.

## Estrutura do Postmortem

```
## Postmortem: [INC-ID] - [Title]
**Data**: [Data do incidente]
**Autor**: [Quem escreveu]
**Revisores**: [Quem revisou]

### Summary
[Resumo em 2-3 frases do que aconteceu e do impacto]

### Timeline
[Timeline detalhada do incidente - usar timeline-component]

### Root Cause Analysis
[Analise de causa raiz usando 5 Whys ou Fishbone]

### Impact
- Usuarios afetados: [numero]
- Duracao: [tempo total]
- Dados comprometidos: [tipo e volume]
- Custo estimado: [financeiro se aplicavel]

### What Went Well
- [Coisas que funcionaram durante a resposta]

### What Could Be Improved
- [Areas de melhoria identificadas]

### Action Items
| Action | Owner | Priority | Due Date | Status |
|--------|-------|----------|----------|--------|
| [Acao 1] | @owner | P1 | [data] | Open |

### Lessons Learned
[Licoes registradas no lessons-learned-registry]
```

## 5 Whys - Exemplo

1. Por que o atacante acessou o banco? Credenciais expostas.
2. Por que as credenciais estavam expostas? Hardcoded no repositorio.
3. Por que estavam hardcoded? Sem processo de secrets management.
4. Por que nao havia processo? Nunca foi priorizado.
5. Por que nao foi priorizado? Falta de security requirements no SDLC.

## Regras de Conducao

- Focar em "o que" e "como", nunca em "quem"
- Linguagem neutra e factual
- Todos os envolvidos participam sem hierarquia
- Action items concretos com owners e prazos
- Publicar internamente para aprendizado organizacional

## Anti-Patterns

- Nomear individuos como causa do incidente
- Concluir sem action items concretos
- Nao fazer follow-up dos action items
- Restringir acesso ao postmortem (transparencia e essencial)
