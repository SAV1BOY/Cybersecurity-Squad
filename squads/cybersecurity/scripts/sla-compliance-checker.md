# SLA Compliance Checker

Script para verificar conformidade com SLAs de remediacao de vulnerabilidades e resposta a incidentes.

## Descricao

Analisa findings e incidentes abertos, verifica conformidade com os SLAs definidos e gera alertas para itens em risco ou ja violados.

## Inputs

- `source` - Conexao com o sistema de tracking (ticketing system)
- `sla_config` - Arquivo de configuracao com SLAs por severidade
- `check_date` - Data de referencia para o calculo (padrao: hoje)

## SLAs Padrao

| Severidade | SLA Remediacao | SLA Resposta IR |
|------------|----------------|-----------------|
| Critical | 48 horas | 15 minutos |
| High | 15 dias uteis | 1 hora |
| Medium | 30 dias uteis | 4 horas |
| Low | 90 dias uteis | 1 dia util |

## Logica

1. Carregar configuracao de SLAs
2. Consultar todos os findings/incidentes abertos
3. Para cada item:
   - Calcular tempo decorrido desde abertura
   - Comparar com SLA da severidade correspondente
   - Classificar como: dentro do SLA, em risco (>80% do SLA), violado
4. Gerar lista priorizada de violacoes e itens em risco
5. Calcular metricas de SLA compliance geral

## Output

```
Data de verificacao: 2026-03-06
Total de itens abertos: 45

Dentro do SLA: 32 (71%)
Em risco (>80%): 6 (13%)
SLA violado: 7 (16%)

Violacoes:
  FIND-023 [Critical] - 5 dias aberto (SLA: 48h) - Owner: Team Alpha
  FIND-045 [High] - 22 dias aberto (SLA: 15 dias) - Owner: Team Beta
  ...

Em risco:
  FIND-067 [Medium] - 26 dias aberto (SLA: 30 dias) - Owner: Team Gamma
  ...
```

## Acoes Automaticas

- Itens em risco: enviar notificacao ao owner
- SLA violado: enviar escalacao ao management do owner
- SLA violado > 2x: enviar alerta ao security operations lead

## Uso

```
sla-compliance-checker --source tracker --sla sla-config.yaml --date 2026-03-06
```

## Agendamento

Recomendado executar diariamente via cron ou scheduler para deteccao precoce de violacoes.
