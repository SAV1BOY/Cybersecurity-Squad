# Sanders - Reporting for Responders

Checklist para qualidade de reports voltados a equipes de resposta.

## Estrutura do Report para IR
- [ ] Incident summary em formato executivo (quem, o que, quando, impacto)
- [ ] Severity e priority claramente indicados
- [ ] Timeline de eventos resumida na primeira pagina
- [ ] IOCs listados em formato actionable (IP, domain, hash, YARA)
- [ ] Affected systems listados com hostname, IP, owner
- [ ] Current status do incidente claramente indicado

## Detalhamento Tecnico
- [ ] Attack vector identificado e descrito
- [ ] Initial access method documentado com evidencia
- [ ] Lateral movement paths documentados step-by-step
- [ ] Persistence mechanisms identificados com locations
- [ ] Data accessed/exfiltrated documentado com scope
- [ ] Malware/tools utilizados pelo atacante listados com hashes
- [ ] C2 infrastructure documentada (IPs, domains, protocols)

## Actionable Intelligence
- [ ] IOCs formatados para import em security tools (STIX, CSV)
- [ ] YARA rules criadas para deteccao de malware identificado
- [ ] Sigma rules criadas para deteccao de TTPs observadas
- [ ] Blocking recommendations com IOCs especificos
- [ ] Detection rules para monitoramento pos-incidente
- [ ] Hunting queries fornecidas para verificar scope

## Containment e Recovery Guidance
- [ ] Containment actions recomendadas priorizadas
- [ ] Eradication steps detalhados por sistema afetado
- [ ] Recovery sequence recomendada
- [ ] Verification steps para confirmar eradicacao completa
- [ ] Monitoring requirements pos-recovery definidos
- [ ] Rollback procedures documentados

## Comunicacao
- [ ] Report escrito para audiencia tecnica (IR team, SOC)
- [ ] Executive summary separado para management
- [ ] Legal/compliance summary para equipe juridica
- [ ] Notification templates para stakeholders afetados
- [ ] External communication guidance (se necessario)
- [ ] Media statement draft (se incidente publico)

## Lessons Learned
- [ ] Root cause analysis incluida
- [ ] Detection gaps identificados com recommendations
- [ ] Process improvements recomendados
- [ ] Technology gaps identificados
- [ ] Training needs identificados
- [ ] Preventive measures para incidentes similares
- [ ] Report revisado por IR lead antes de distribuicao
- [ ] Report classificado e distribuido conforme need-to-know
