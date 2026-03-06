# Security Review Brief

> Documento para solicitacao de revisao de seguranca de features, arquitetura ou mudancas.
> Deve ser submetido pelo time de desenvolvimento antes do deploy em producao.

---

## 1. Informacoes da Solicitacao

- **Solicitante:** [NOME_DO_SOLICITANTE]
- **Squad / Time:** [NOME_DO_SQUAD]
- **Data da Solicitacao:** [DATA]
- **Data Desejada de Conclusao:** [DATA_LIMITE]
- **Prioridade:** [CRITICA / ALTA / MEDIA / BAIXA]
- **Tipo de Review:** [DESIGN_REVIEW / CODE_REVIEW / ARCHITECTURE_REVIEW / PRE_DEPLOY]

## 2. Descricao da Mudanca

[DESCREVA_A_FEATURE_MUDANCA_OU_SISTEMA_QUE_PRECISA_DE_REVISAO_DE_SEGURANCA]

## 3. Contexto Tecnico

- **Repositorio(s):** [LINKS_DOS_REPOSITORIOS]
- **Pull Request(s):** [LINKS_DOS_PRS]
- **Linguagem / Framework:** [STACK_TECNOLOGICA]
- **Servicos afetados:** [LISTA_DE_SERVICOS]
- **Documentacao de design:** [LINK_PARA_DESIGN_DOC]

## 4. Checklist de Seguranca (preenchido pelo solicitante)

- [ ] Autenticacao e autorizacao foram implementadas
- [ ] Input validation esta aplicado em todos os entry points
- [ ] Dados sensiveis estao criptografados at rest e in transit
- [ ] Logging de seguranca esta implementado
- [ ] Secrets nao estao hardcoded no codigo
- [ ] Dependencias foram verificadas quanto a vulnerabilidades
- [ ] [ITEM_ADICIONAL]

## 5. Dados e Privacidade

- **Dados pessoais processados:** [SIM / NAO]
- **Tipos de dados:** [PII / FINANCEIRO / SAUDE / OUTRO]
- **Conformidade necessaria:** [LGPD / PCI_DSS / SOC2 / HIPAA / NA]
- **Retencao de dados:** [POLITICA_DE_RETENCAO]

## 6. Superficie de Ataque

- **Novos endpoints expostos:** [LISTA_DE_ENDPOINTS]
- **Integracao com terceiros:** [LISTA_DE_INTEGRACOES]
- **Mudancas em permissoes:** [DESCRICAO_DAS_MUDANCAS]
- **Novos mecanismos de autenticacao:** [DESCRICAO]

## 7. Threat Considerations

[DESCREVA_AMEACAS_QUE_VOCE_IDENTIFICOU_OU_PREOCUPACOES_DE_SEGURANCA]

## 8. Resultado da Review

> Secao preenchida pelo Security Reviewer

- **Reviewer:** [NOME_DO_REVIEWER]
- **Data da Review:** [DATA]
- **Status:** [APROVADO / APROVADO_COM_RESSALVAS / REPROVADO]
- **Findings:** [NUMERO_DE_FINDINGS]
- **Observacoes:** [COMENTARIOS_DO_REVIEWER]

## 9. Condicoes para Aprovacao

- [ ] [CONDICAO_1]
- [ ] [CONDICAO_2]
- [ ] [CONDICAO_3]

---

*Template versao 1.0 — Cybersecurity Squad*
