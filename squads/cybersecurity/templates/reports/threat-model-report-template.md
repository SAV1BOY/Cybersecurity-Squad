# Threat Model Report Template

> Relatorio de resultados da modelagem de ameacas.
> Documenta threats identificadas, riscos e mitigacoes recomendadas.

---

## 1. Informacoes do Relatorio

- **Sistema / Aplicacao:** [NOME_DO_SISTEMA]
- **Versao Analisada:** [VERSAO]
- **Data da Analise:** [DATA]
- **Analista(s):** [NOMES_DOS_ANALISTAS]
- **Metodologia:** [STRIDE / PASTA / ATTACK_TREES / LINDDUN]
- **Threat Model Brief:** [REFERENCIA_AO_BRIEF]

## 2. Resumo Executivo

[RESUMO_DOS_PRINCIPAIS_ACHADOS_DA_MODELAGEM_DE_AMEACAS]

## 3. Arquitetura do Sistema

### 3.1 Descricao

[DESCRICAO_DA_ARQUITETURA_DO_SISTEMA_ANALISADO]

### 3.2 Componentes

| Componente | Tipo | Tecnologia | Trust Level |
|------------|------|------------|-------------|
| [COMPONENTE_1] | [WEB_SERVER / DB / API / CACHE] | [TECNOLOGIA] | [TRUSTED / UNTRUSTED] |
| [COMPONENTE_2] | [WEB_SERVER / DB / API / CACHE] | [TECNOLOGIA] | [TRUSTED / UNTRUSTED] |

### 3.3 Data Flow Diagram

[REFERENCIA_AO_DFD_OU_DESCRICAO_DOS_FLUXOS]

## 4. Trust Boundaries Identificadas

| ID | Boundary | Descricao | Componentes Separados |
|----|----------|-----------|----------------------|
| TB-[NUM] | [NOME_DA_BOUNDARY] | [DESCRICAO] | [COMPONENTES] |
| TB-[NUM] | [NOME_DA_BOUNDARY] | [DESCRICAO] | [COMPONENTES] |

## 5. Threats Identificadas

### 5.1 [THREAT_ID] — [TITULO_DA_THREAT]

- **Categoria (STRIDE):** [SPOOFING / TAMPERING / REPUDIATION / INFO_DISCLOSURE / DOS / ELEVATION_OF_PRIVILEGE]
- **Componente Afetado:** [COMPONENTE]
- **Trust Boundary:** [TB_ID]
- **Descricao:** [DESCRICAO_DA_AMEACA]
- **Cenario de Ataque:** [DESCRICAO_DO_CENARIO]
- **Probabilidade:** [ALTA / MEDIA / BAIXA]
- **Impacto:** [CRITICO / ALTO / MEDIO / BAIXO]
- **Risco Resultante:** [CRITICO / ALTO / MEDIO / BAIXO]
- **MITRE ATT&CK:** [TECHNIQUE_ID — NOME]

**Mitigacao Existente:**
[DESCRICAO_DOS_CONTROLES_JA_EXISTENTES_OU_NENHUM]

**Mitigacao Recomendada:**
[DESCRICAO_DA_MITIGACAO_RECOMENDADA]

> Repita a secao 5.1 para cada threat.

## 6. Matriz de Risco

| Threat ID | Probabilidade | Impacto | Risco | Mitigacao | Risco Residual |
|-----------|---------------|---------|-------|-----------|----------------|
| [THREAT_ID] | [A/M/B] | [A/M/B] | [A/M/B] | [EXISTENTE/RECOMENDADA] | [A/M/B] |

## 7. Recomendacoes Priorizadas

| Prioridade | Recomendacao | Threat(s) Mitigada(s) | Esforco |
|------------|--------------|----------------------|---------|
| 1 | [RECOMENDACAO] | [THREAT_IDS] | [BAIXO/MEDIO/ALTO] |
| 2 | [RECOMENDACAO] | [THREAT_IDS] | [BAIXO/MEDIO/ALTO] |
| 3 | [RECOMENDACAO] | [THREAT_IDS] | [BAIXO/MEDIO/ALTO] |

## 8. Premissas e Limitacoes

- [PREMISSA_OU_LIMITACAO_1]
- [PREMISSA_OU_LIMITACAO_2]

## 9. Conclusao

[CONCLUSAO_GERAL_SOBRE_A_POSTURA_DE_SEGURANCA_DO_SISTEMA]

---

*Template versao 1.0 — Cybersecurity Squad*
