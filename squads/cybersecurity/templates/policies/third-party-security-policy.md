# Third-Party Security Policy Template

> Politica de seguranca para terceiros, fornecedores e parceiros.
> Define requisitos de seguranca para relacionamentos com terceiros.

---

## 1. Informacoes do Documento

- **Titulo:** Politica de Seguranca para Terceiros
- **Versao:** [VERSAO]
- **Data de Vigencia:** [DATA]
- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Aprovado por:** [NOME_DO_APROVADOR]
- **Proxima Revisao:** [DATA_PROXIMA_REVISAO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DA_POLITICA_DE_SEGURANCA_PARA_TERCEIROS]

## 3. Escopo

- **Aplica-se a:** Todos os fornecedores, parceiros e prestadores de servico
- **Tipos de terceiros cobertos:** SaaS, IaaS, consultorias, outsourcing, APIs
- **Excecoes:** [EXCECOES_COM_APROVACAO_DE]

## 4. Classificacao de Terceiros

| Nivel de Risco | Criterios | Exemplos | Avaliacao |
|----------------|-----------|----------|-----------|
| Critico | Acesso a dados restritos ou sistemas criticos | [EXEMPLOS] | [AVALIACAO_COMPLETA] |
| Alto | Acesso a dados confidenciais | [EXEMPLOS] | [AVALIACAO_DETALHADA] |
| Medio | Acesso a dados internos | [EXEMPLOS] | [QUESTIONARIO] |
| Baixo | Sem acesso a dados ou sistemas | [EXEMPLOS] | [AVALIACAO_SIMPLIFICADA] |

## 5. Processo de Avaliacao (Due Diligence)

### 5.1 Pre-Contratacao

- [ ] Security questionnaire preenchido pelo terceiro
- [ ] Revisao de certificacoes (SOC2, ISO 27001, etc.)
- [ ] Avaliacao de risco conforme classificacao
- [ ] Verificacao de historico de incidentes publicos
- [ ] Revisao de politicas de seguranca do terceiro
- [ ] Aprovacao do Security Team: [CRITERIO]
- [ ] [ACAO_ADICIONAL]

### 5.2 Requisitos Contratuais

Contratos com terceiros devem incluir:

- [ ] Clausulas de protecao de dados e confidencialidade (NDA)
- [ ] Requisitos de seguranca da informacao
- [ ] Direito de auditoria: [FREQUENCIA]
- [ ] Obrigacao de notificacao de incidentes: [PRAZO]
- [ ] SLAs de seguranca
- [ ] Clausulas de subcontratacao
- [ ] Requisitos de conformidade LGPD (DPA)
- [ ] Penalidades por descumprimento
- [ ] [CLAUSULA_ADICIONAL]

## 6. Gestao de Acessos de Terceiros

- Principio de least privilege
- Acessos limitados ao escopo do contrato
- Contas nominais (nao genericas)
- MFA obrigatorio para acesso remoto
- Revisao de acessos: [FREQUENCIA]
- Revogacao imediata ao termino do contrato
- Monitoramento de atividades: [FERRAMENTA]
- [REQUISITO_ADICIONAL]

## 7. Monitoramento Continuo

### 7.1 Avaliacoes Periodicas

| Nivel de Risco | Frequencia de Reavaliacao | Tipo de Avaliacao |
|----------------|--------------------------|-------------------|
| Critico | [FREQUENCIA] | [TIPO_AVALIACAO] |
| Alto | [FREQUENCIA] | [TIPO_AVALIACAO] |
| Medio | [FREQUENCIA] | [TIPO_AVALIACAO] |
| Baixo | [FREQUENCIA] | [TIPO_AVALIACAO] |

### 7.2 Monitoramento de Risco

- Monitoramento de security ratings: [FERRAMENTA_SECURITY_RATINGS]
- Monitoramento de incidentes publicos envolvendo o terceiro
- Revisao de mudancas relevantes no terceiro
- [MONITORAMENTO_ADICIONAL]

## 8. Gestao de Incidentes com Terceiros

- Terceiro deve notificar incidentes em ate [HORAS]
- Canal de notificacao: [CANAL]
- Cooperacao obrigatoria na investigacao
- Acesso a logs e evidencias conforme contrato
- [REQUISITO_ADICIONAL]

## 9. Offboarding de Terceiros

- [ ] Revogar todos os acessos
- [ ] Recuperar ativos e credenciais
- [ ] Confirmar destruicao/devolucao de dados
- [ ] Registro de offboarding em [SISTEMA]
- [ ] [ACAO_ADICIONAL]

## 10. Violacoes

O descumprimento desta politica pode resultar em [CONSEQUENCIAS].

## 11. Historico de Revisoes

| Versao | Data | Autor | Descricao |
|--------|------|-------|-----------|
| [VERSAO] | [DATA] | [NOME] | [DESCRICAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
