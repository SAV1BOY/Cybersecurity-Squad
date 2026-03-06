# Incident Triage Quality Gate

Checklist de qualidade para triagem de incidentes de seguranca.

## Deteccao Inicial
- [ ] Alerta recebido e registrado com timestamp
- [ ] Fonte do alerta identificada (SIEM, EDR, IDS, user report)
- [ ] Alert fidelity verificada (true positive vs false positive)
- [ ] Ticket de incidente criado no sistema de tracking
- [ ] Incident handler designado e notificado
- [ ] Comunicacao inicial com stakeholders realizada

## Classificacao
- [ ] Tipo de incidente categorizado (malware, phishing, data breach, DDoS)
- [ ] Severity level atribuido (P1-Critical, P2-High, P3-Medium, P4-Low)
- [ ] Business impact avaliado (sistemas afetados, dados expostos)
- [ ] Numero de usuarios/sistemas impactados estimado
- [ ] Regulatory notification requirements verificados (LGPD, GDPR)
- [ ] SLA de resposta identificado para o severity level

## Coleta Inicial de Dados
- [ ] IOCs (Indicators of Compromise) extraidos do alerta
- [ ] Logs relevantes coletados e preservados (firewall, proxy, DNS, auth)
- [ ] Affected systems identificados e listados
- [ ] Timeline preliminar construida com eventos conhecidos
- [ ] Network connections suspeitas identificadas
- [ ] User accounts envolvidas identificadas

## Analise Inicial
- [ ] IOCs correlacionados com threat intelligence feeds
- [ ] Scope do comprometimento estimado (lateral movement?)
- [ ] Attack vector provavel identificado
- [ ] Kill chain stage determinado
- [ ] Related alerts dos ultimos 30 dias revisados
- [ ] Known malware family identificada (se aplicavel)

## Decisao de Escalation
- [ ] Criticidade confirmada apos analise inicial
- [ ] Escalation decision documentada com justificativa
- [ ] Incident response team notificado (se escalado)
- [ ] Management chain notificado conforme severity
- [ ] External parties notificadas se necessario (CERT, law enforcement)

## Documentacao
- [ ] Triage notes completas no ticket de incidente
- [ ] Decisao de true/false positive documentada
- [ ] Handoff notes preparados para proximo analista
- [ ] Evidence preservada para possivel forensics
- [ ] Tempo de triage registrado para metricas
