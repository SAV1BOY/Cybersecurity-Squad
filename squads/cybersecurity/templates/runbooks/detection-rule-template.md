# Detection Rule Template

> Template padrao para criacao e documentacao de regras de deteccao.
> Cada regra deve ser documentada antes de ser implantada no SIEM/EDR.

---

## 1. Informacoes da Regra

- **Rule ID:** [RULE_ID_UNICO]
- **Nome da Regra:** [NOME_DESCRITIVO_DA_REGRA]
- **Autor:** [NOME_DO_AUTOR]
- **Data de Criacao:** [DATA]
- **Ultima Revisao:** [DATA]
- **Status:** [DRAFT / EM_TESTE / ATIVA / DESATIVADA / DEPRECATED]
- **Plataforma:** [SIEM / EDR / IDS / WAF / CLOUD]

## 2. Objetivo

[DESCREVA_O_QUE_ESTA_REGRA_DETECTA_E_POR_QUE_E_IMPORTANTE]

## 3. Classificacao

- **MITRE ATT&CK Tactic:** [TACTIC_ID — NOME]
- **MITRE ATT&CK Technique:** [TECHNIQUE_ID — NOME]
- **MITRE ATT&CK Sub-technique:** [SUB_TECHNIQUE_ID — NOME]
- **Kill Chain Phase:** [RECONNAISSANCE / WEAPONIZATION / DELIVERY / EXPLOITATION / INSTALLATION / C2 / ACTIONS]
- **Severidade do Alerta:** [CRITICAL / HIGH / MEDIUM / LOW / INFORMATIONAL]
- **Tipo:** [DETECTION / HUNTING / CORRELATION]

## 4. Data Sources

| Fonte de Dados | Tipo de Log | Campo Chave |
|----------------|-------------|-------------|
| [FONTE_1] | [WINDOWS_EVENT / SYSLOG / CLOUD_TRAIL / NETFLOW] | [CAMPO] |
| [FONTE_2] | [TIPO_LOG] | [CAMPO] |

## 5. Logica da Regra

### 5.1 Descricao da Logica

[DESCRICAO_EM_LINGUAGEM_NATURAL_DA_LOGICA_DE_DETECCAO]

### 5.2 Pseudo-codigo

```
[PSEUDO_CODIGO_DA_REGRA]
Exemplo:
WHEN event.type = "process_creation"
AND process.name IN [LISTA_DE_PROCESSOS]
AND process.parent NOT IN [LISTA_DE_PAIS_LEGITIMOS]
AND [CONDICAO_ADICIONAL]
THEN alert(severity=[SEVERIDADE])
```

### 5.3 Query (implementacao)

```
[QUERY_NA_LINGUAGEM_DO_SIEM — SPL / KQL / SIGMA / YARA_L / OUTRO]
```

## 6. Threshold e Tuning

- **Threshold:** [NUMERO_DE_EVENTOS_EM_JANELA_DE_TEMPO]
- **Janela de tempo:** [MINUTOS / HORAS]
- **Agrupamento:** [CAMPOS_DE_AGRUPAMENTO]
- **Supressao:** [PERIODO_DE_SUPRESSAO]
- **Whitelist/Exclusoes:**
  - [EXCLUSAO_1 — JUSTIFICATIVA]
  - [EXCLUSAO_2 — JUSTIFICATIVA]

## 7. Cenarios de Teste

| # | Cenario | Input | Resultado Esperado | Status |
|---|---------|-------|--------------------|--------|
| 1 | True positive | [DESCRICAO_DO_CENARIO_TP] | Alerta disparado | [PASS / FAIL] |
| 2 | True negative | [DESCRICAO_DO_CENARIO_TN] | Sem alerta | [PASS / FAIL] |
| 3 | False positive conhecido | [DESCRICAO_FP] | [FILTRADO / ACEITO] | [PASS / FAIL] |

## 8. Resposta ao Alerta

### 8.1 Playbook Associado

- **Runbook vinculado:** [NOME_DO_RUNBOOK]
- **SLA de triagem:** [MINUTOS]
- **Escalacao automatica:** [SIM_CONDICAO / NAO]

### 8.2 Passos de Triagem

1. [PASSO_TRIAGEM_1]
2. [PASSO_TRIAGEM_2]
3. [PASSO_TRIAGEM_3]

## 9. Metricas de Performance

| Metrica | Valor | Periodo |
|---------|-------|---------|
| Alertas gerados | [NUM] | [PERIODO] |
| True positive rate | [PERCENT]% | [PERIODO] |
| False positive rate | [PERCENT]% | [PERIODO] |
| MTTD | [MINUTOS] | [PERIODO] |

## 10. Referencias

- [REFERENCIA_1]
- [REFERENCIA_2]
- [SIGMA_RULE_REFERENCIA]

## 11. Historico de Alteracoes

| Data | Autor | Alteracao |
|------|-------|----------|
| [DATA] | [NOME] | Criacao da regra |
| [DATA] | [NOME] | [DESCRICAO_DA_ALTERACAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
