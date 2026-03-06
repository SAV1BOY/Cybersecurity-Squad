# IR Runbook — Phishing

> Runbook de resposta a incidentes de phishing.
> Siga os passos sequencialmente. Documente todas as acoes e horarios.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Phishing (Email / SMS / Voice)
- **Severidade Padrao Inicial:** [MEDIUM]
- **Owner:** [NOME_DO_RESPONSAVEL_PELO_RUNBOOK]
- **Ultima Revisao:** [DATA_ULTIMA_REVISAO]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Fontes de Deteccao

- Report de usuario via [CANAL_DE_REPORT]
- Alerta do email gateway: [FERRAMENTA_EMAIL_GATEWAY]
- Alerta de SIEM: [REGRA_SIEM_ESPECIFICA]
- Threat intelligence feed
- [FONTE_ADICIONAL]

### 2.2 Indicadores de Phishing

- [ ] Remetente suspeito ou spoofed
- [ ] URL maliciosa ou encurtada
- [ ] Anexo suspeito
- [ ] Urgencia incomum na mensagem
- [ ] Solicitacao de credenciais ou dados sensiveis
- [ ] Headers de email anomalos

## 3. Triage (Triagem)

### 3.1 Analise Inicial

- [ ] Verificar headers do email (SPF, DKIM, DMARC)
- [ ] Analisar URLs com [FERRAMENTA_URL_ANALYSIS]
- [ ] Analisar anexos em sandbox: [FERRAMENTA_SANDBOX]
- [ ] Verificar reputacao do sender domain em [FERRAMENTA_REPUTACAO]
- [ ] Determinar quantos usuarios receberam o email

### 3.2 Classificacao

- **Tipo:** [CREDENTIAL_HARVESTING / MALWARE_DELIVERY / BEC / SPEAR_PHISHING]
- **Alvo:** [INDIVIDUAL / DEPARTAMENTO / ORGANIZACAO_TODA]
- **Severidade Ajustada:** [CRITICAL / HIGH / MEDIUM / LOW]

## 4. Containment (Contencao)

### 4.1 Acoes Imediatas

- [ ] Bloquear sender domain no email gateway
- [ ] Bloquear URLs maliciosas no proxy/firewall
- [ ] Remover email de todas as caixas (purge): `[COMANDO_OU_PROCEDIMENTO_DE_PURGE]`
- [ ] Bloquear hash de anexo malicioso no endpoint protection
- [ ] Adicionar IOCs ao blocklist: [PLATAFORMA_DE_BLOCKLIST]

### 4.2 Se Credenciais Foram Comprometidas

- [ ] Forcar reset de senha dos usuarios afetados
- [ ] Revogar sessoes ativas
- [ ] Verificar logins suspeitos no IdP: [FERRAMENTA_IDP]
- [ ] Habilitar MFA se nao estiver ativo
- [ ] Escalar conforme ir-credential-leak-runbook

### 4.3 Se Malware Foi Executado

- [ ] Isolar endpoint(s) afetado(s)
- [ ] Escalar conforme ir-malware-infection-runbook

## 5. Eradication (Erradicacao)

- [ ] Confirmar remocao completa dos emails maliciosos
- [ ] Verificar que IOCs estao bloqueados em todos os controles
- [ ] Validar que nenhum persistence mechanism foi instalado
- [ ] Atualizar regras de deteccao do email gateway
- [ ] [ACAO_ADICIONAL_DE_ERRADICACAO]

## 6. Recovery (Recuperacao)

- [ ] Restaurar acesso de usuarios apos reset de credenciais
- [ ] Monitorar contas afetadas por [PERIODO_DE_MONITORAMENTO]
- [ ] Confirmar que servicos estao operando normalmente
- [ ] [ACAO_ADICIONAL_DE_RECUPERACAO]

## 7. Post-Incident

- [ ] Coletar e preservar evidencias
- [ ] Documentar timeline completa
- [ ] Elaborar postmortem
- [ ] Atualizar IOCs na threat intelligence platform
- [ ] Enviar security awareness sobre a campanha
- [ ] Atualizar este runbook se necessario

## 8. IOCs Coletados

| Tipo | Valor | Contexto |
|------|-------|----------|
| [EMAIL / DOMAIN / URL / HASH / IP] | [VALOR_DO_IOC] | [CONTEXTO] |

## 9. Contatos de Escalacao

| Nivel | Contato | Canal |
|-------|---------|-------|
| L1 — SOC Analyst | [NOME_CONTATO] | [CANAL] |
| L2 — IR Lead | [NOME_CONTATO] | [CANAL] |
| L3 — CISO | [NOME_CONTATO] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
