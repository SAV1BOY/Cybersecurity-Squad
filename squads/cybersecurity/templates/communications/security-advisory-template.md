# Security Advisory Template

> Template de advisory de seguranca para comunicacao de ameacas e vulnerabilidades.
> Distribuldo internamente para orientar times sobre acoes necessarias.

---

## Security Advisory

**Classificacao:** [INTERNO / CONFIDENCIAL]
**Prioridade:** [CRITICA / ALTA / MEDIA / BAIXA / INFORMATIVA]

---

### Cabecalho

- **Advisory ID:** [ADV-YYYY-NNN]
- **Data de Publicacao:** [DATA]
- **Ultima Atualizacao:** [DATA]
- **Autor:** [SECURITY_TEAM / NOME]
- **Status:** [ATIVO / ATUALIZADO / ENCERRADO]
- **Assunto:** [TITULO_DESCRITIVO_DO_ADVISORY]

---

### 1. Resumo

[DESCRICAO_RESUMIDA_DA_AMEACA_OU_VULNERABILIDADE_E_POR_QUE_E_RELEVANTE]

### 2. Detalhes da Ameaca / Vulnerabilidade

- **Tipo:** [CVE / ZERO_DAY / CAMPANHA_DE_ATAQUE / MISCONFIGURATION / OUTRO]
- **CVE (se aplicavel):** [CVE_ID]
- **CVSS Score:** [SCORE]
- **Produtos Afetados:** [LISTA_DE_PRODUTOS_E_VERSOES]
- **Exploit Disponivel:** [SIM — PUBLICO / SIM — PRIVADO / NAO]
- **Exploracao Ativa (In the Wild):** [SIM / NAO]
- **MITRE ATT&CK:** [TECHNIQUE_ID — NOME]

### 3. Impacto

[DESCRICAO_DO_IMPACTO_POTENCIAL_SE_A_VULNERABILIDADE_FOR_EXPLORADA]

- **Confidencialidade:** [ALTO / MEDIO / BAIXO / NENHUM]
- **Integridade:** [ALTO / MEDIO / BAIXO / NENHUM]
- **Disponibilidade:** [ALTO / MEDIO / BAIXO / NENHUM]

### 4. Avaliacao de Exposicao Interna

- **Sistemas internos afetados:** [SIM — LISTA / NAO / EM_AVALIACAO]
- **Numero de ativos expostos:** [NUMERO_OU_EM_AVALIACAO]
- **Exposicao externa:** [SIM / NAO]
- **Nivel de risco para a organizacao:** [CRITICO / ALTO / MEDIO / BAIXO]

### 5. Acoes Requeridas

> Acoes que devem ser executadas pelos times responsaveis.

| Acao | Responsavel | Prazo | Prioridade |
|------|-------------|-------|------------|
| [ACAO_1 — ex: Aplicar patch versao X.Y.Z] | [TIME_RESPONSAVEL] | [PRAZO] | [IMEDIATO / URGENTE / NORMAL] |
| [ACAO_2 — ex: Verificar exposicao dos ativos] | [TIME_RESPONSAVEL] | [PRAZO] | [PRIORIDADE] |
| [ACAO_3 — ex: Implementar mitigacao temporaria] | [TIME_RESPONSAVEL] | [PRAZO] | [PRIORIDADE] |
| [ACAO_4] | [TIME] | [PRAZO] | [PRIORIDADE] |

### 6. Mitigacao Temporaria (Workaround)

> Se o patch nao estiver disponivel ou nao puder ser aplicado imediatamente.

[DESCRICAO_DA_MITIGACAO_TEMPORARIA_COM_PASSOS_DETALHADOS]

```
[COMANDOS_OU_CONFIGURACOES_PARA_MITIGACAO]
```

### 7. Indicadores de Comprometimento (IOCs)

| Tipo | Valor | Contexto |
|------|-------|----------|
| [IP / DOMAIN / HASH / URL / EMAIL] | [VALOR] | [CONTEXTO] |
| [TIPO] | [VALOR] | [CONTEXTO] |
| [TIPO] | [VALOR] | [CONTEXTO] |

### 8. Deteccao

- Regra de deteccao adicionada ao SIEM: [SIM — RULE_ID / EM_DESENVOLVIMENTO / NA]
- Assinatura de EDR/IDS atualizada: [SIM / NAO / NA]
- Query de hunting: [LINK_OU_DESCRICAO]

### 9. Referencias

- [LINK_ADVISORY_VENDOR]
- [LINK_CVE_DETAILS]
- [LINK_BLOG_ANALISE]
- [REFERENCIA_ADICIONAL]

### 10. Contato

Para duvidas sobre este advisory, entre em contato com [SECURITY_TEAM] via [CANAL].

---

*Template versao 1.0 — Cybersecurity Squad*
