# Technical Report Template

> Relatorio tecnico detalhado de assessment de seguranca.
> Destinado a equipes tecnicas responsaveis pela remediacao.

---

## 1. Informacoes do Relatorio

- **Titulo:** [TITULO_DO_ASSESSMENT]
- **Autor(es):** [NOMES_DOS_AUTORES]
- **Revisor:** [NOME_DO_REVISOR]
- **Data:** [DATA_DO_RELATORIO]
- **Versao:** [VERSAO_DO_DOCUMENTO]
- **Classificacao:** [CONFIDENCIAL / RESTRITO]

## 2. Sumario Executivo

[RESUMO_BREVE_PARA_CONTEXTO_TECNICO_2_A_3_PARAGRAFOS]

## 3. Escopo e Metodologia

### 3.1 Escopo

- **Alvos testados:** [LISTA_DE_ALVOS_COM_IPS_URLS]
- **Tipo de teste:** [BLACKBOX / GREYBOX / WHITEBOX]
- **Ambiente:** [PRODUCAO / STAGING / DEDICADO]

### 3.2 Metodologia

- **Framework:** [OWASP_TESTING_GUIDE / PTES / NIST / OSSTMM]
- **Fases executadas:** [RECONHECIMENTO / SCANNING / EXPLORACAO / POST_EXPLOITATION]
- **Ferramentas utilizadas:**
  - [FERRAMENTA_1] — versao [VERSAO]
  - [FERRAMENTA_2] — versao [VERSAO]
  - [FERRAMENTA_3] — versao [VERSAO]

## 4. Sumario de Findings

| ID | Titulo | Severidade | CVSS | Status |
|----|--------|------------|------|--------|
| [FINDING_ID_1] | [TITULO] | [CRITICAL/HIGH/MEDIUM/LOW] | [SCORE] | [ABERTO / REMEDIADO] |
| [FINDING_ID_2] | [TITULO] | [CRITICAL/HIGH/MEDIUM/LOW] | [SCORE] | [ABERTO / REMEDIADO] |
| [FINDING_ID_3] | [TITULO] | [CRITICAL/HIGH/MEDIUM/LOW] | [SCORE] | [ABERTO / REMEDIADO] |

## 5. Findings Detalhados

### 5.1 [FINDING_ID] — [TITULO_DO_FINDING]

- **Severidade:** [CRITICAL / HIGH / MEDIUM / LOW]
- **CVSS Score:** [SCORE] ([VECTOR_STRING])
- **CWE:** [CWE_ID] — [CWE_NOME]
- **Localizacao:** [URL_ENDPOINT_COMPONENTE]
- **Status:** [ABERTO / REMEDIADO / ACEITO]

**Descricao:**
[DESCRICAO_TECNICA_DETALHADA_DA_VULNERABILIDADE]

**Prova de Conceito (PoC):**
```
[PAYLOAD_OU_COMANDO_UTILIZADO]
```

**Evidencia:**
[SCREENSHOTS_OUTPUTS_OU_REFERENCIAS]

**Impacto:**
[DESCRICAO_DO_IMPACTO_TECNICO_E_DE_NEGOCIO]

**Recomendacao:**
[DESCRICAO_TECNICA_DA_CORRECAO_RECOMENDADA]

**Referencias:**
- [LINK_REFERENCIA_1]
- [LINK_REFERENCIA_2]

> Repita a secao 5.1 para cada finding identificado.

## 6. Observacoes Positivas

- [CONTROLE_POSITIVO_1]
- [CONTROLE_POSITIVO_2]
- [CONTROLE_POSITIVO_3]

## 7. Conclusao e Proximos Passos

[CONCLUSAO_GERAL_E_RECOMENDACOES_DE_PROXIMOS_PASSOS]

## 8. Anexos

- Anexo A: [DESCRICAO_DO_ANEXO]
- Anexo B: [DESCRICAO_DO_ANEXO]

---

*Template versao 1.0 — Cybersecurity Squad*
