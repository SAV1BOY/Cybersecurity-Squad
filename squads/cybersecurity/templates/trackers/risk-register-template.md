# Risk Register Template

> Registro de riscos de seguranca da informacao.
> Documenta, prioriza e acompanha o tratamento de riscos identificados.

---

## 1. Informacoes do Registro

- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Ultima Atualizacao:** [DATA]
- **Frequencia de Revisao:** [MENSAL / TRIMESTRAL]
- **Metodologia:** [ISO_27005 / NIST / FAIR / CUSTOM]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Criterios de Avaliacao

### 2.1 Probabilidade

| Nivel | Score | Descricao |
|-------|-------|-----------|
| Muito Alta | 5 | [DESCRICAO — FREQUENCIA_ESPERADA] |
| Alta | 4 | [DESCRICAO] |
| Media | 3 | [DESCRICAO] |
| Baixa | 2 | [DESCRICAO] |
| Muito Baixa | 1 | [DESCRICAO] |

### 2.2 Impacto

| Nivel | Score | Financeiro | Operacional | Reputacional |
|-------|-------|------------|-------------|--------------|
| Critico | 5 | [FAIXA_VALOR] | [DESCRICAO] | [DESCRICAO] |
| Alto | 4 | [FAIXA_VALOR] | [DESCRICAO] | [DESCRICAO] |
| Medio | 3 | [FAIXA_VALOR] | [DESCRICAO] | [DESCRICAO] |
| Baixo | 2 | [FAIXA_VALOR] | [DESCRICAO] | [DESCRICAO] |
| Minimo | 1 | [FAIXA_VALOR] | [DESCRICAO] | [DESCRICAO] |

### 2.3 Classificacao de Risco

| Score (P x I) | Classificacao | Cor |
|---------------|---------------|-----|
| 20-25 | Critico | Vermelho |
| 12-19 | Alto | Laranja |
| 6-11 | Medio | Amarelo |
| 1-5 | Baixo | Verde |

## 3. Registro de Riscos

| Risk ID | Titulo | Descricao | Categoria | Prob. | Imp. | Score Inerente | Controles | Score Residual | Tratamento | Owner | Status | Prazo |
|---------|--------|-----------|-----------|-------|------|----------------|-----------|----------------|------------|-------|--------|-------|
| [RISK_001] | [TITULO] | [DESCRICAO] | [CATEGORIA] | [1-5] | [1-5] | [SCORE] | [CONTROLES] | [SCORE] | [MITIGAR/ACEITAR/TRANSFERIR/EVITAR] | [NOME] | [ABERTO/EM_TRATAMENTO/FECHADO] | [DATA] |
| [RISK_002] | [TITULO] | [DESCRICAO] | [CATEGORIA] | [1-5] | [1-5] | [SCORE] | [CONTROLES] | [SCORE] | [TRATAMENTO] | [NOME] | [STATUS] | [DATA] |
| [RISK_003] | [TITULO] | [DESCRICAO] | [CATEGORIA] | [1-5] | [1-5] | [SCORE] | [CONTROLES] | [SCORE] | [TRATAMENTO] | [NOME] | [STATUS] | [DATA] |

## 4. Categorias de Risco

- **Tecnico:** Vulnerabilidades, misconfigurations, falhas de arquitetura
- **Operacional:** Processos, pessoas, procedimentos
- **Compliance:** Regulatorio, contratual, normativo
- **Terceiros:** Fornecedores, supply chain, parceiros
- **[CATEGORIA_ADICIONAL]:** [DESCRICAO]

## 5. Riscos Aceitos

| Risk ID | Titulo | Score | Justificativa | Aprovado por | Data Aprovacao | Revisao |
|---------|--------|-------|---------------|--------------|----------------|---------|
| [RISK_ID] | [TITULO] | [SCORE] | [JUSTIFICATIVA] | [NOME_CARGO] | [DATA] | [DATA_REVISAO] |

## 6. Plano de Tratamento Resumido

| Risk ID | Acao de Tratamento | Responsavel | Prazo | Investimento | Status |
|---------|-------------------|-------------|-------|--------------|--------|
| [RISK_ID] | [ACAO] | [NOME] | [DATA] | [VALOR] | [STATUS] |
| [RISK_ID] | [ACAO] | [NOME] | [DATA] | [VALOR] | [STATUS] |

## 7. Historico de Revisoes

| Data | Riscos Adicionados | Riscos Fechados | Riscos Reclassificados | Revisor |
|------|--------------------|-----------------|------------------------|---------|
| [DATA] | [NUM] | [NUM] | [NUM] | [NOME] |
| [DATA] | [NUM] | [NUM] | [NUM] | [NOME] |

---

*Template versao 1.0 — Cybersecurity Squad*
