# Bug Bounty Launch Project

Template de projeto para lancamento de programa de bug bounty.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Tipo | [Private / Public] |
| Plataforma | [HackerOne / Bugcrowd / Intigriti / Self-hosted] |
| Escopo Inicial | [Aplicacoes e dominios incluidos] |
| Budget Anual | [Bounty pool + platform fees] |
| Timeline | [4-8 semanas para lancamento] |
| Owner | [AppSec team lead] |

## Fase 1: Preparacao (Semanas 1-3)

### Pre-requisitos
- [ ] Vulnerability management process maduro
- [ ] Capacidade de triagem de reports em < 48h
- [ ] Canais de comunicacao com engineering estabelecidos
- [ ] SLAs de remediacao definidos e respeitados
- [ ] Budget aprovado pela lideranca

### Definicao de Escopo
- [ ] Ativos in-scope listados (domains, APIs, mobile apps)
- [ ] Ativos out-of-scope definidos (staging, third-party)
- [ ] Tipos de vulnerabilidade aceitos
- [ ] Tipos de teste proibidos (DoS, social engineering)
- [ ] Safe harbor policy redigida e aprovada pelo legal

### Tabela de Bounties
| Severity | Bounty Range |
|----------|-------------|
| Critical | $2,000 - $10,000 |
| High | $1,000 - $3,000 |
| Medium | $300 - $1,000 |
| Low | $100 - $300 |

## Fase 2: Lancamento Private (Semanas 4-6)

- [ ] Programa criado na plataforma
- [ ] Policy e scope publicados
- [ ] 10-20 pesquisadores convidados inicialmente
- [ ] Processo de triagem validado com primeiros reports
- [ ] SLA de resposta: acknowledge em 24h, triagem em 72h

## Fase 3: Operacao e Expansao (Semanas 7+)

- [ ] Metricas de programa monitoradas
- [ ] Pool de pesquisadores expandido gradualmente
- [ ] Escopo expandido conforme maturidade
- [ ] Transicao para public quando pronto
- [ ] Report de resultados mensal para lideranca

## Metricas do Programa

| Metrica | Target |
|---------|--------|
| Time to first response | < 24h |
| Time to triage | < 72h |
| Time to bounty | < 14 dias |
| Valid report rate | > 30% |
| Researcher satisfaction | > 4/5 |

## Processo de Triagem

1. Report recebido na plataforma
2. AppSec analyst faz triagem inicial (valid/invalid/duplicate)
3. Se valido: severity assessment e reproducao
4. Comunicacao com researcher sobre status
5. Ticket criado para engineering com SLA
6. Bounty pago apos validacao
7. Researcher notificado sobre fix e disclosure
