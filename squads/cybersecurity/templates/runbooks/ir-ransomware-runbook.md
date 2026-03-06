# IR Runbook — Ransomware

> Runbook de resposta a incidentes de ransomware.
> Tempo e decisivo. Siga os passos imediatamente e escale para o Incident Commander.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Ransomware
- **Severidade Padrao Inicial:** CRITICAL
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Indicadores de Ransomware

- [ ] Arquivos com extensoes incomuns ou criptografados
- [ ] Nota de resgate (ransom note) encontrada
- [ ] Volume anormal de operacoes de escrita em filesystem
- [ ] Alerta de EDR/AV sobre processo de criptografia
- [ ] Servicos ou sistemas indisponiveis sem explicacao
- [ ] Shadow copies deletadas

### 2.2 Fontes de Alerta

- EDR: [FERRAMENTA_EDR]
- SIEM rule: [REGRA_ESPECIFICA]
- Monitoramento de filesystem: [FERRAMENTA]
- Report de usuario
- [FONTE_ADICIONAL]

## 3. Acoes Imediatas (Primeiros 15 Minutos)

> ATENCAO: NAO desligue os sistemas — isso pode destruir evidencias em memoria.

- [ ] Notificar Incident Commander: [NOME_IC]
- [ ] Isolar sistemas afetados da rede (desconectar cabo / desabilitar WiFi)
- [ ] NAO reiniciar os sistemas
- [ ] Identificar e isolar o paciente zero (se possivel)
- [ ] Desabilitar compartilhamentos de rede (SMB/NFS)
- [ ] Bloquear comunicacao com C2 conhecidos no firewall
- [ ] Preservar logs e evidencias volateis

## 4. Containment (Contencao)

### 4.1 Network Containment

- [ ] Segmentar rede para evitar propagacao lateral
- [ ] Bloquear portas SMB (445/139) entre segmentos
- [ ] Desabilitar RDP em endpoints nao essenciais
- [ ] Bloquear IOCs no firewall/proxy: [LISTA_DE_IOCS]
- [ ] Revisar e restringir regras de firewall temporariamente

### 4.2 Identity Containment

- [ ] Resetar senhas de contas administrativas comprometidas
- [ ] Desabilitar contas de servico suspeitas
- [ ] Revogar tokens e sessoes ativas
- [ ] Resetar KRBTGT se domain controller comprometido (2x com intervalo)
- [ ] [ACAO_ADICIONAL_IDENTITY]

### 4.3 Endpoint Containment

- [ ] Isolar endpoints via EDR: [PROCEDIMENTO_EDR]
- [ ] Bloquear hash do ransomware no EDR/AV
- [ ] Desabilitar execucao de scripts (PowerShell, WMI) temporariamente
- [ ] [ACAO_ADICIONAL_ENDPOINT]

## 5. Investigation (Investigacao)

- [ ] Identificar variante do ransomware: [FERRAMENTA_ID_RANSOMWARE]
- [ ] Determinar vetor de entrada inicial
- [ ] Mapear sistemas afetados (scope do impacto)
- [ ] Verificar se houve exfiltracao de dados (double extortion)
- [ ] Analisar logs de autenticacao para movimentacao lateral
- [ ] Coletar amostras para analise em sandbox

## 6. Eradication (Erradicacao)

- [ ] Remover artefatos maliciosos de todos os sistemas
- [ ] Eliminar mecanismos de persistence
- [ ] Corrigir vulnerabilidade/vetor de entrada utilizado
- [ ] Verificar integridade do Active Directory
- [ ] Validar que backup nao foi comprometido
- [ ] [ACAO_ADICIONAL]

## 7. Recovery (Recuperacao)

- [ ] Validar integridade dos backups
- [ ] Priorizar restauracao por criticidade de negocio
- [ ] Restaurar sistemas a partir de backups limpos
- [ ] Aplicar patches de seguranca antes de reconectar
- [ ] Monitorar intensivamente por [PERIODO]
- [ ] Reconectar sistemas gradualmente a rede

## 8. Decisao sobre Pagamento de Resgate

> Esta decisao envolve: CISO, Juridico, CEO e, se aplicavel, autoridades.

- Pagamento NAO e recomendado por padrao
- Se considerado, consultar: [CONTATO_NEGOCIADOR_OU_CONSULTOR]
- Registrar decisao formalmente com justificativa

## 9. Comunicacao e Escalacao

| Quando | Quem Notificar | Canal |
|--------|----------------|-------|
| Imediato | Incident Commander | [CANAL] |
| Primeiros 30 min | CISO / CTO | [CANAL] |
| Primeiras 2h | Juridico / DPO | [CANAL] |
| Conforme necessario | Autoridades (ANPD, policia) | [CANAL] |
| Conforme necessario | Clientes afetados | [CANAL] |

## 10. Post-Incident

- [ ] Postmortem completo
- [ ] Atualizar threat intelligence com IOCs
- [ ] Revisar e melhorar controles de backup
- [ ] Realizar exercicio de table-top com licoes aprendidas
- [ ] Atualizar este runbook

---

*Template versao 1.0 — Cybersecurity Squad*
