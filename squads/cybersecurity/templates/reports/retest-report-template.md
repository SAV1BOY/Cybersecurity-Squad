# Retest Report Template

> Relatorio de reteste para validacao de correcoes aplicadas.
> Vinculado ao assessment original e ao plano de remediacao.

---

## 1. Informacoes do Retest

- **Assessment Original:** [ID_OU_TITULO_DO_ASSESSMENT_ORIGINAL]
- **Data do Retest:** [DATA_INICIO] a [DATA_TERMINO]
- **Retestador:** [NOME_DO_RETESTADOR]
- **Versao do Sistema Retestado:** [VERSAO_OU_BUILD]
- **Ambiente:** [PRODUCAO / STAGING / DEV]

## 2. Resumo do Retest

| Status | Quantidade | Percentual |
|--------|------------|------------|
| Remediado (Fixed) | [NUM] | [PERCENT]% |
| Parcialmente Remediado | [NUM] | [PERCENT]% |
| Nao Remediado | [NUM] | [PERCENT]% |
| Nao Retestavel | [NUM] | [PERCENT]% |
| **Total** | **[TOTAL]** | **100%** |

## 3. Resultados Detalhados

### 3.1 [FINDING_ID] — [TITULO_DO_FINDING]

- **Severidade Original:** [CRITICAL / HIGH / MEDIUM / LOW]
- **Status do Retest:** [FIXED / PARTIALLY_FIXED / NOT_FIXED / NOT_TESTABLE]
- **Nova Severidade (se alterada):** [SEVERIDADE_OU_NA]

**Correcao Aplicada:**
[DESCRICAO_DA_CORRECAO_QUE_FOI_IMPLEMENTADA]

**Teste Realizado:**
[DESCRICAO_DO_TESTE_EXECUTADO_PARA_VALIDAR]

**Resultado:**
[DESCRICAO_DO_RESULTADO_DO_RETESTE]

**Evidencia:**
```
[OUTPUT_SCREENSHOT_OU_REFERENCIA_DA_EVIDENCIA]
```

**Observacoes:**
[COMENTARIOS_ADICIONAIS_SOBRE_A_CORRECAO]

> Repita a secao 3.1 para cada finding retestado.

## 4. Novos Findings (se identificados)

| ID | Titulo | Severidade | Descricao |
|----|--------|------------|-----------|
| [NEW_FINDING_ID] | [TITULO] | [SEVERIDADE] | [DESCRICAO_BREVE] |

## 5. Findings Nao Retestados

| Finding ID | Motivo |
|------------|--------|
| [FINDING_ID] | [MOTIVO_PELO_QUAL_NAO_FOI_RETESTADO] |

## 6. Comparativo

| Metrica | Assessment Original | Retest |
|---------|---------------------|--------|
| Total de findings | [NUM] | [NUM] |
| Critical | [NUM] | [NUM] |
| High | [NUM] | [NUM] |
| Medium | [NUM] | [NUM] |
| Low | [NUM] | [NUM] |
| Risk Score geral | [SCORE] | [SCORE] |

## 7. Conclusao

[CONCLUSAO_SOBRE_A_EFETIVIDADE_DAS_CORRECOES_E_PROXIMOS_PASSOS]

## 8. Recomendacoes

- [RECOMENDACAO_1]
- [RECOMENDACAO_2]
- [RECOMENDACAO_3]

---

*Template versao 1.0 — Cybersecurity Squad*
