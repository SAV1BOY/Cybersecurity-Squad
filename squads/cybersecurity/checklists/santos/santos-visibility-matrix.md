# Santos - Visibility Matrix

Checklist para avaliacao e manutencao da matriz de visibilidade de seguranca.

## Inventario de Data Sources
- [ ] Endpoint telemetry sources catalogadas (EDR, sysmon, audit logs)
- [ ] Network telemetry sources catalogadas (firewall, NDR, proxy, DNS)
- [ ] Identity telemetry sources catalogadas (AD, IAM, RADIUS)
- [ ] Cloud telemetry sources catalogadas (CloudTrail, Azure Monitor)
- [ ] Application telemetry sources catalogadas (WAF, app logs)
- [ ] Email telemetry sources catalogadas (gateway, O365, GSuite)
- [ ] Physical security telemetry catalogada (badge, camera)

## Mapeamento ATT&CK
- [ ] MITRE ATT&CK matrix utilizada como framework de referencia
- [ ] Cada tactic coberta por pelo menos uma data source
- [ ] Cada technique prioritaria mapeada a data sources disponiveis
- [ ] Coverage gaps por tactic identificados e documentados
- [ ] ATT&CK Navigator heatmap criado com coverage atual
- [ ] Top threats para o setor mapeados e cobertura verificada
- [ ] Sub-techniques criticas verificadas individualmente

## Avaliacao de Qualidade por Source
- [ ] Log completeness verificada (fields necessarios presentes)
- [ ] Log fidelity avaliada (dados confiaveis e precisos)
- [ ] Log latency medida (delay entre evento e disponibilidade)
- [ ] Log retention adequada para investigation needs
- [ ] Log volume monitorado para anomalias (drops, spikes)
- [ ] Parsing accuracy verificada no SIEM
- [ ] Enrichment data disponivel e correto

## Gaps de Visibilidade
- [ ] Blind spots de rede identificados (subnets sem monitoring)
- [ ] Endpoints sem EDR/agent catalogados
- [ ] Cloud accounts sem audit logging identificados
- [ ] Shadow IT sem visibilidade documentado
- [ ] Encrypted traffic sem inspecao catalogado
- [ ] Mobile devices sem telemetry documentados
- [ ] IoT/OT devices sem monitoring identificados

## Plano de Melhoria
- [ ] Gaps priorizados por risco e impacto
- [ ] Data source onboarding plan definido
- [ ] Budget implications documentadas
- [ ] Quick wins identificados (sources faceis de integrar)
- [ ] Timeline para gap closure definida
- [ ] Responsible owner para cada improvement action

## Manutencao e Reporting
- [ ] Visibility matrix revisada trimestralmente
- [ ] Dashboard de coverage operacional atualizado
- [ ] Metricas de visibilidade reportadas ao management
- [ ] New systems automaticamente avaliados para telemetry
- [ ] Decommissioned systems removidos da matrix
- [ ] Visibility improvements rastreados e medidos
- [ ] Matrix compartilhada com detection engineering e threat hunting
