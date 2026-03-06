# IR Runbook — Credential Leak

> Runbook de resposta a vazamento ou comprometimento de credenciais.
> Aplicavel a senhas, API keys, tokens, certificados e secrets.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Credential Leak / Compromise
- **Severidade Padrao Inicial:** HIGH
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Fontes de Deteccao

- Alerta de credential monitoring: [FERRAMENTA_DARK_WEB_MONITORING]
- Secret scanning em repositorios: [GITHUB_SECRET_SCANNING / GITLEAKS / TRUFFLEHOG]
- Report de paste site / dark web
- Alerta de login anomalo no SIEM
- Report de terceiro ou pesquisador
- [FONTE_ADICIONAL]

### 2.2 Tipo de Credencial Comprometida

- [ ] Senha de usuario corporativo
- [ ] Credencial de conta privilegiada / admin
- [ ] API key / access token
- [ ] Service account credential
- [ ] Certificado digital / private key
- [ ] Database connection string
- [ ] Cloud IAM credentials
- [ ] [OUTRO_TIPO]

## 3. Triage (Triagem)

- [ ] Identificar tipo e escopo da credencial vazada
- [ ] Determinar onde a credencial foi exposta: [REPOSITORIO / PASTE / DARK_WEB / PHISHING]
- [ ] Verificar se a credencial ainda e valida
- [ ] Identificar todos os servicos que utilizam a credencial
- [ ] Verificar logs de uso da credencial por acessos nao autorizados
- [ ] Classificar severidade: [CRITICAL / HIGH / MEDIUM / LOW]

## 4. Containment (Contencao)

### 4.1 Acoes Imediatas

- [ ] Revogar / rotacionar a credencial comprometida imediatamente
- [ ] Invalidar todas as sessoes ativas associadas
- [ ] Bloquear IP(s) suspeito(s) que utilizaram a credencial
- [ ] Se API key: revogar no provider e gerar nova
- [ ] Se certificado: revogar e emitir novo
- [ ] Se service account: desabilitar temporariamente

### 4.2 Verificacao de Acesso Nao Autorizado

- [ ] Revisar logs de autenticacao: [FERRAMENTA_DE_LOGS]
- [ ] Verificar acoes realizadas com a credencial comprometida
- [ ] Identificar dados acessados ou exfiltrados
- [ ] Verificar criacao de backdoors ou persistence
- [ ] Verificar lateral movement a partir da conta

## 5. Eradication (Erradicacao)

- [ ] Remover credencial de qualquer local publico (repositorio, paste)
- [ ] Solicitar takedown se publicado externamente
- [ ] Limpar historico do git se commited em repositorio: `[PROCEDIMENTO_GIT_FILTER]`
- [ ] Verificar e limpar qualquer artefato de persistence
- [ ] Atualizar credencial em todos os servicos dependentes
- [ ] Implementar secret rotation automatica se nao existente

## 6. Recovery (Recuperacao)

- [ ] Distribuir nova credencial de forma segura: [VAULT / SECRET_MANAGER]
- [ ] Validar funcionamento dos servicos com nova credencial
- [ ] Confirmar que credencial antiga nao funciona mais
- [ ] Monitorar conta por [PERIODO] para atividade anomala
- [ ] [ACAO_ADICIONAL]

## 7. Post-Incident

- [ ] Documentar root cause do vazamento
- [ ] Implementar controles preventivos (pre-commit hooks, secret scanning)
- [ ] Atualizar politica de gerenciamento de secrets
- [ ] Treinar equipe sobre manuseio seguro de credenciais
- [ ] Elaborar postmortem
- [ ] Atualizar este runbook

## 8. Ferramentas de Apoio

| Ferramenta | Uso | Acesso |
|------------|-----|--------|
| [SECRET_SCANNER] | Deteccao de secrets em codigo | [URL_OU_INSTRUCAO] |
| [VAULT / SECRET_MANAGER] | Armazenamento seguro de secrets | [URL_OU_INSTRUCAO] |
| [DARK_WEB_MONITOR] | Monitoramento de vazamentos | [URL_OU_INSTRUCAO] |
| [SIEM] | Analise de logs de acesso | [URL_OU_INSTRUCAO] |

## 9. Contatos de Escalacao

| Nivel | Contato | Canal |
|-------|---------|-------|
| L1 — SOC | [NOME] | [CANAL] |
| L2 — IR Team | [NOME] | [CANAL] |
| L3 — CISO | [NOME] | [CANAL] |
| Cloud Team | [NOME] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
