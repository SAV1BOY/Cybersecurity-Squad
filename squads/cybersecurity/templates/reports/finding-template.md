# Finding Template

> Template padrao para documentacao individual de findings de seguranca.
> Um finding por documento, vinculado ao relatorio principal.

---

## 1. Identificacao

- **Finding ID:** [FINDING_ID]
- **Titulo:** [TITULO_DESCRITIVO_DO_FINDING]
- **Relatorio Pai:** [ID_DO_RELATORIO_PRINCIPAL]
- **Autor:** [NOME_DO_AUTOR]
- **Data de Identificacao:** [DATA]
- **Ultima Atualizacao:** [DATA]

## 2. Classificacao

- **Severidade:** [CRITICAL / HIGH / MEDIUM / LOW / INFORMATIONAL]
- **CVSS v3.1 Score:** [SCORE]
- **CVSS Vector:** [CVSS_VECTOR_STRING]
- **CWE ID:** [CWE_NUMERO]
- **CWE Nome:** [CWE_DESCRICAO]
- **OWASP Category:** [CATEGORIA_OWASP]
- **CVE (se aplicavel):** [CVE_ID_OU_NA]

## 3. Localizacao

- **Ativo Afetado:** [HOSTNAME_URL_IP]
- **Componente:** [COMPONENTE_ESPECIFICO]
- **Endpoint / Path:** [ENDPOINT_OU_CAMINHO]
- **Parametro:** [PARAMETRO_VULNERAVEL]
- **Codigo Fonte (se aplicavel):** [ARQUIVO:LINHA]

## 4. Descricao

[DESCRICAO_TECNICA_DETALHADA_DA_VULNERABILIDADE_EXPLICANDO_A_CAUSA_RAIZ]

## 5. Prova de Conceito (PoC)

### 5.1 Pre-requisitos

- [PREREQUISITO_1]
- [PREREQUISITO_2]

### 5.2 Passos para Reproducao

1. [PASSO_1]
2. [PASSO_2]
3. [PASSO_3]
4. [PASSO_4]

### 5.3 Payload / Request

```
[REQUEST_HTTP_PAYLOAD_OU_COMANDO]
```

### 5.4 Response / Resultado

```
[RESPONSE_OU_OUTPUT_OBTIDO]
```

## 6. Evidencias

| # | Tipo | Descricao | Referencia |
|---|------|-----------|------------|
| 1 | [SCREENSHOT / LOG / PCAP] | [DESCRICAO] | [ARQUIVO_OU_LINK] |
| 2 | [SCREENSHOT / LOG / PCAP] | [DESCRICAO] | [ARQUIVO_OU_LINK] |

## 7. Impacto

### 7.1 Impacto Tecnico

- **Confidencialidade:** [ALTO / MEDIO / BAIXO / NENHUM]
- **Integridade:** [ALTO / MEDIO / BAIXO / NENHUM]
- **Disponibilidade:** [ALTO / MEDIO / BAIXO / NENHUM]
- **Descricao:** [DESCRICAO_DO_IMPACTO_TECNICO]

### 7.2 Impacto no Negocio

[DESCRICAO_DO_IMPACTO_NO_NEGOCIO_INCLUINDO_DADOS_FINANCEIROS_OU_REGULATORIOS]

## 8. Recomendacao de Remediacao

[DESCRICAO_DETALHADA_DA_CORRECAO_RECOMENDADA_COM_EXEMPLOS_DE_CODIGO_SE_APLICAVEL]

```
[EXEMPLO_DE_CODIGO_CORRIGIDO]
```

## 9. Referencias

- [LINK_REFERENCIA_1]
- [LINK_REFERENCIA_2]
- [LINK_REFERENCIA_3]

## 10. Historico de Status

| Data | Status | Responsavel | Observacao |
|------|--------|-------------|------------|
| [DATA] | Identificado | [NOME] | [OBSERVACAO] |
| [DATA] | [EM_REMEDIACAO / REMEDIADO / ACEITO] | [NOME] | [OBSERVACAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
