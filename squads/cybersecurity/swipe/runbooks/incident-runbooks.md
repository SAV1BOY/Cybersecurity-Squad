# Incident Runbooks

Colecao de runbooks para resposta a incidentes com steps claros e acionaveis.

## Estrutura Padrao de Runbook

1. **Trigger** - Condicao que ativa o runbook
2. **Severity Assessment** - Como classificar a severidade
3. **Immediate Actions** - Primeiros 15 minutos
4. **Investigation Steps** - Coleta de evidencias e analise
5. **Containment** - Acoes de isolamento
6. **Eradication** - Remocao da ameaca
7. **Recovery** - Restauracao de servicos
8. **Post-Incident** - Documentacao e postmortem

## Runbook: Ransomware Detection

**Trigger:** Alerta de file encryption em massa ou ransom note detectada

**Immediate Actions (primeiros 15 min):**
- Isolar host(s) afetados da rede (desabilitar porta no switch)
- Notificar Incident Commander e CISO
- Preservar memoria com `volatility` antes de desligar
- Verificar backup integrity imediatamente

**Investigation:**
- Identificar patient zero via EDR timeline
- Mapear lateral movement com logs de autenticacao
- Verificar exfiltration via netflow/proxy logs
- Coletar IOCs (hashes, IPs, domains) para threat intel

## Tipos de Runbook Essenciais

- Phishing confirmado com credential compromise
- Malware detection em endpoint corporativo
- Data exfiltration suspeita
- Unauthorized access a sistemas criticos
- DDoS em servicos de producao
- Supply chain compromise
