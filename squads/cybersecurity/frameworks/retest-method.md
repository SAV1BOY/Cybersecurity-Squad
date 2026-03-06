# Retest Method — Framework Interno

> Como verificar se uma correcao realmente resolveu o problema.

## Principios

1. **Mesmo teste, mesmo ambiente** — Reproduzir o teste original nas mesmas condicoes
2. **Evidencia de correcao** — Capturar prova de que o fix funciona
3. **Regressao** — Verificar se o fix nao quebrou outra coisa
4. **Bypass check** — Tentar contornar o fix de 2-3 formas diferentes
5. **Documentar resultado** — Corrigido, parcialmente corrigido, nao corrigido

## Processo de Reteste

### 1. Preparacao
```
- Obter o finding original (PoC completa)
- Confirmar que o fix foi implementado (commit/deploy)
- Preparar ambiente de teste (mesmo que o original)
- Notificar o time responsavel
```

### 2. Reproducao do Teste Original
```
- Executar exatamente os mesmos passos da PoC original
- Capturar resultado (esperado: falha do ataque)
- Se o ataque ainda funciona: NOT FIXED
- Se o ataque falha: prosseguir para bypass check
```

### 3. Bypass Check
```
Tentar contornar o fix de formas criativas:
- Variacao de encoding (URL encode, double encode, unicode)
- Variacao de case (uppercase, lowercase, mixed)
- Variacao de metodo HTTP (GET vs POST vs PUT)
- Variacao de parametro (outro campo similar)
- Null bytes, truncation
- Race conditions
- Se qualquer bypass funcionar: PARTIALLY FIXED
```

### 4. Regression Check
```
- Funcionalidade afetada ainda funciona normalmente?
- Outros endpoints/funcoes similares nao foram afetados negativamente?
- Performance nao foi degradada significativamente?
```

### 5. Documentacao
```yaml
retest_id: RT-[ANO]-[SEQ]
finding_id: CYBER-[ANO]-[SEQ]
retest_date: [YYYY-MM-DD]
retested_by: [Agente]
fix_version: [commit/version]
result: Fixed | Partially Fixed | Not Fixed
evidence: [Hash da nova evidencia]
bypass_attempts: [Descricao das tentativas]
regression_check: Pass | Fail
notes: [Observacoes adicionais]
```

## Resultados Possiveis

| Resultado | Acao |
|-----------|------|
| Fixed | Fechar finding, atualizar registry |
| Partially Fixed | Reabrir com detalhes do bypass, novo SLA |
| Not Fixed | Reabrir, escalar se SLA estourado |
| New Finding | Abrir novo finding separado |

## Quality Gate

- `retest-quality.md` — Checklist de reteste
