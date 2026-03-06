# Santos - Alert Triage

Checklist para processo de triagem de alertas no SOC.

## Recepcao do Alerta
- [ ] Alerta recebido e ticket criado automaticamente
- [ ] Timestamp de recepcao registrado
- [ ] Alert source identificada (SIEM, EDR, NDR, email)
- [ ] Alert severity verificada e confirmada
- [ ] SLA timer iniciado conforme severity
- [ ] Analista designado para triagem

## Contextualizacao Inicial
- [ ] Asset envolvido identificado (hostname, IP, owner, criticality)
- [ ] User associado ao evento identificado
- [ ] Localizacao geografica do evento verificada
- [ ] Horario do evento avaliado (business hours vs off-hours)
- [ ] Asset criticality verificada no inventario
- [ ] Alertas anteriores para o mesmo asset/user revisados

## Analise do Alerta
- [ ] Alert logic compreendida (o que a regra detecta)
- [ ] Raw logs subjacentes ao alerta revisados
- [ ] Source e destination IPs analisados (reputation, geo, ownership)
- [ ] Domains/URLs envolvidos verificados em threat intel
- [ ] File hashes verificados em threat intel (VirusTotal, OTX)
- [ ] Network connections correlacionadas com proxy/firewall logs
- [ ] Endpoint activity verificada via EDR console
- [ ] Email logs verificados (se phishing-related)

## Determinacao
- [ ] Classificacao definida: True Positive, False Positive, Benign True Positive
- [ ] Justificativa da classificacao documentada
- [ ] Se True Positive: severity confirmada e escalacao iniciada
- [ ] Se False Positive: tuning request criado para detection team
- [ ] Se Benign True Positive: exception documentada
- [ ] Confidence level da determinacao registrado

## Escalacao (se True Positive)
- [ ] Incident ticket criado com detalhes do alerta
- [ ] L2/L3 analista notificado conforme escalation matrix
- [ ] Initial containment recommendations incluidas
- [ ] All relevant evidence anexada ao ticket
- [ ] Stakeholders notificados conforme severity
- [ ] Timeline inicial documentada

## Documentacao e Fechamento
- [ ] Triage notes completas no ticket
- [ ] Tempo de triage registrado (para MTTD metrics)
- [ ] Classificacao final registrada para reporting
- [ ] Knowledge base atualizada (se novo pattern identificado)
- [ ] Feedback fornecido para detection engineering (se applicable)
- [ ] Ticket fechado com resolucao documentada
- [ ] Handoff notes para proximo turno (se investigacao em andamento)
