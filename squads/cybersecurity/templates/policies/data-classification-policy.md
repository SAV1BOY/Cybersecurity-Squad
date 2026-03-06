# Data Classification Policy Template

> Politica de classificacao de dados e informacoes.
> Define niveis de classificacao, criterios e controles por nivel.

---

## 1. Informacoes do Documento

- **Titulo:** Politica de Classificacao de Dados
- **Versao:** [VERSAO]
- **Data de Vigencia:** [DATA]
- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Aprovado por:** [NOME_DO_APROVADOR]
- **Proxima Revisao:** [DATA_PROXIMA_REVISAO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DA_POLITICA_DE_CLASSIFICACAO_DE_DADOS]

## 3. Escopo

- **Aplica-se a:** Todos os dados criados, processados ou armazenados pela organizacao
- **Formatos:** Digital, fisico, verbal
- **Responsaveis:** [TODOS_OS_COLABORADORES_E_TERCEIROS]

## 4. Niveis de Classificacao

### 4.1 Publico (Public)

- **Descricao:** [DESCRICAO_DO_NIVEL_PUBLICO]
- **Exemplos:** [MATERIAIS_MARKETING / SITE_PUBLICO / PRESS_RELEASES]
- **Impacto se divulgado:** Nenhum

### 4.2 Interno (Internal)

- **Descricao:** [DESCRICAO_DO_NIVEL_INTERNO]
- **Exemplos:** [COMUNICACOES_INTERNAS / POLITICAS / PROCEDIMENTOS]
- **Impacto se divulgado:** [DESCRICAO_DO_IMPACTO]

### 4.3 Confidencial (Confidential)

- **Descricao:** [DESCRICAO_DO_NIVEL_CONFIDENCIAL]
- **Exemplos:** [DADOS_FINANCEIROS / CONTRATOS / DADOS_DE_CLIENTES]
- **Impacto se divulgado:** [DESCRICAO_DO_IMPACTO]

### 4.4 Restrito (Restricted)

- **Descricao:** [DESCRICAO_DO_NIVEL_RESTRITO]
- **Exemplos:** [DADOS_PII_SENSIVEIS / CREDENCIAIS / CHAVES_CRIPTOGRAFICAS / DADOS_SAUDE]
- **Impacto se divulgado:** [DESCRICAO_DO_IMPACTO_SEVERO]

## 5. Controles por Nivel

| Controle | Publico | Interno | Confidencial | Restrito |
|----------|---------|---------|-------------|----------|
| Criptografia em transito | Recomendado | Obrigatorio | Obrigatorio | Obrigatorio |
| Criptografia em repouso | Nao requerido | Recomendado | Obrigatorio | Obrigatorio |
| Controle de acesso | Aberto | Funcionarios | Need-to-know | Need-to-know + aprovacao |
| Logging de acesso | Nao requerido | Basico | Detalhado | Detalhado + alertas |
| Compartilhamento externo | Livre | Com aprovacao | Com aprovacao + NDA | [PROCESSO_RESTRITO] |
| Descarte | Normal | [PROCEDIMENTO] | Destruicao segura | Destruicao certificada |
| Backup | [POLITICA] | [POLITICA] | Obrigatorio + criptografado | Obrigatorio + criptografado |
| Rotulagem | Nao requerido | Recomendado | Obrigatorio | Obrigatorio |

## 6. Responsabilidades

### 6.1 Data Owner

- Classificar os dados sob sua responsabilidade
- Definir quem pode acessar os dados
- Revisar classificacao periodicamente: [FREQUENCIA]
- [RESPONSABILIDADE_ADICIONAL]

### 6.2 Data Custodian

- Implementar controles tecnicos conforme classificacao
- Proteger dados conforme nivel definido
- Reportar violacoes ao Data Owner e Security Team
- [RESPONSABILIDADE_ADICIONAL]

### 6.3 Usuarios

- Tratar dados conforme classificacao
- Nao reclassificar sem autorizacao do Data Owner
- Reportar dados sem classificacao ao gestor
- [RESPONSABILIDADE_ADICIONAL]

## 7. Processo de Classificacao

1. Data Owner identifica dados sob sua responsabilidade
2. Avalia conforme criterios de classificacao
3. Aplica rotulagem: [METODO_DE_ROTULAGEM]
4. Registra em inventario de dados: [FERRAMENTA]
5. Implementa controles correspondentes
6. Revisao periodica: [FREQUENCIA]

## 8. Dados Pessoais (LGPD)

- Dados pessoais: classificacao minima [CONFIDENCIAL / RESTRITO]
- Dados pessoais sensiveis: classificacao [RESTRITO]
- Consentimento documentado conforme LGPD
- DPO notificado para novos tratamentos: [CONTATO_DPO]
- [REQUISITO_ADICIONAL_LGPD]

## 9. Violacoes

O descumprimento desta politica pode resultar em [CONSEQUENCIAS].

## 10. Historico de Revisoes

| Versao | Data | Autor | Descricao |
|--------|------|-------|-----------|
| [VERSAO] | [DATA] | [NOME] | [DESCRICAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
