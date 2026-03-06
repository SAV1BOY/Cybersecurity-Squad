# IR Runbook — Suspicious Login

> Runbook de resposta a alertas de login suspeito ou acesso nao autorizado.
> Inclui impossible travel, brute force e login de localizacao anomala.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Suspicious Login / Unauthorized Access
- **Severidade Padrao Inicial:** MEDIUM
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Tipos de Alerta

- [ ] Impossible travel (login de geolocalizacoes distantes em curto periodo)
- [ ] Login de pais ou regiao incomum
- [ ] Multiplas falhas de autenticacao (brute force)
- [ ] Login fora do horario padrao
- [ ] Login de IP em threat intelligence blocklist
- [ ] Login de dispositivo nao reconhecido
- [ ] Password spray detectado
- [ ] [TIPO_ADICIONAL]

### 2.2 Fontes de Alerta

- IdP / SSO: [FERRAMENTA_IDP]
- SIEM: [REGRA_SIEM]
- UEBA: [FERRAMENTA_UEBA]
- Cloud provider alerts: [AWS_GUARDDUTY / AZURE_SENTINEL / GCP_SCC]
- [FONTE_ADICIONAL]

## 3. Triage (Triagem)

### 3.1 Analise Inicial

- [ ] Identificar conta afetada: [USERNAME / EMAIL]
- [ ] Verificar se o login foi bem-sucedido
- [ ] Verificar IP de origem e geolocalizacao
- [ ] Verificar user agent e dispositivo
- [ ] Consultar usuario para confirmar se o acesso e legitimo
- [ ] Verificar se o usuario utiliza VPN pessoal ou viagem

### 3.2 Contextualizacao

- [ ] Historico de logins recentes do usuario
- [ ] Horario padrao de atividade do usuario
- [ ] Dispositivos conhecidos do usuario
- [ ] Verificar se ha outros alertas correlacionados
- [ ] Verificar se mais contas estao com alertas similares (campanha)

### 3.3 Classificacao

| Cenario | Acao |
|---------|------|
| Login legitimo confirmado pelo usuario | Fechar como false positive |
| Brute force sem sucesso | Monitorar e bloquear IP |
| Login bem-sucedido nao reconhecido | Escalar como HIGH |
| Multiplas contas comprometidas | Escalar como CRITICAL |

## 4. Containment (Contencao)

### 4.1 Se Login Nao Autorizado Confirmado

- [ ] Forcar reset de senha imediato
- [ ] Revogar todas as sessoes ativas
- [ ] Habilitar MFA se nao ativo
- [ ] Bloquear IP de origem no firewall / WAF
- [ ] Desabilitar conta temporariamente (se necessario)
- [ ] Verificar regras de email forwarding criadas
- [ ] Verificar aplicacoes OAuth autorizadas recentemente

### 4.2 Se Brute Force / Password Spray

- [ ] Bloquear IPs de origem: [LISTA_DE_IPS]
- [ ] Implementar lockout temporario nas contas alvo
- [ ] Verificar se alguma conta foi comprometida com sucesso
- [ ] Notificar usuarios para alterar senhas
- [ ] [ACAO_ADICIONAL]

## 5. Investigation (Investigacao)

- [ ] Revisar todas as acoes realizadas apos o login suspeito
- [ ] Verificar acessos a dados sensiveis
- [ ] Verificar mudancas de configuracao na conta
- [ ] Verificar se houve movimentacao lateral
- [ ] Correlacionar com outros alertas no SIEM
- [ ] [INVESTIGACAO_ADICIONAL]

## 6. Recovery (Recuperacao)

- [ ] Restaurar acesso do usuario legitimo com nova senha + MFA
- [ ] Reverter alteracoes maliciosas na conta
- [ ] Monitorar conta por [PERIODO]
- [ ] Confirmar com usuario que acesso esta normalizado

## 7. Post-Incident

- [ ] Documentar findings e timeline
- [ ] Atualizar regras de deteccao se necessario
- [ ] Revisar politica de senhas e MFA
- [ ] Considerar implementacao de UEBA se nao existente
- [ ] Atualizar este runbook

## 8. Contatos de Escalacao

| Nivel | Contato | Canal |
|-------|---------|-------|
| L1 — SOC | [NOME] | [CANAL] |
| L2 — IR Team | [NOME] | [CANAL] |
| Identity Team | [NOME] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
