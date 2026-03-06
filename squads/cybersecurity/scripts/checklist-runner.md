# Checklist Runner

Script para executar e rastrear o progresso de checklists de seguranca.

## Descricao

Carrega um checklist padronizado, guia o usuario por cada item, registra o status de cada verificacao e gera relatorio de completude.

## Inputs

- `checklist_type` - Tipo de checklist (pre-engagement, hardening, ir, code-review, closeout)
- `engagement_id` - ID do engagement associado
- `executor` - Nome de quem esta executando o checklist

## Logica

1. Carregar o checklist correspondente ao tipo informado
2. Exibir total de itens e categorias
3. Para cada item do checklist:
   - Exibir descricao do item
   - Solicitar status: pass, fail, na (not applicable)
   - Se fail: solicitar comentario obrigatorio
   - Se na: solicitar justificativa obrigatoria
   - Registrar timestamp de cada verificacao
4. Calcular metricas de completude
5. Gerar relatorio com resultados

## Metricas Calculadas

- Total de itens verificados
- Itens em conformidade (pass)
- Itens com falha (fail)
- Itens nao aplicaveis (na) com justificativa
- Porcentagem de conformidade (pass / (pass + fail))

## Output

```
Checklist: pre-engagement
Engagement: ENG-2026-015
Executor: Analyst Name
Data: 2026-03-06

Total: 15 itens
Pass: 13 (87%)
Fail: 1 (7%)
N/A: 1 (7%)

Itens com falha:
- [FAIL] Item 7: Emergency contact confirmado -> "Contato nao atualizado"

Itens N/A:
- [N/A] Item 12: VPN de teste configurada -> "Teste via rede interna"
```

## Regras de Bloqueio

- Checklists de pre-engagement com itens fail obrigatorios bloqueiam inicio do engagement
- Checklists de closeout incompletos bloqueiam entrega do relatorio final
- Itens N/A acima de 30% geram alerta para revisao do checklist

## Armazenamento

- Resultado salvo em `[engagement_id]/checklist-[tipo]-[data].json`
- Historico preservado para auditoria
