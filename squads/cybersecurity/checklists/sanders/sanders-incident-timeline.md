# Sanders - Incident Timeline

Checklist para construcao de timeline de incidentes de seguranca.

## Coleta de Fontes de Dados
- [ ] SIEM logs coletados para o periodo do incidente
- [ ] Firewall logs obtidos (allow e deny)
- [ ] Proxy/web filter logs obtidos
- [ ] DNS logs coletados
- [ ] Authentication logs (AD, LDAP, RADIUS) obtidos
- [ ] Endpoint logs (EDR, syslog, Event Log) coletados
- [ ] Email gateway logs obtidos (se phishing envolvido)
- [ ] VPN/remote access logs coletados
- [ ] Application-specific logs obtidos
- [ ] Cloud audit logs coletados (CloudTrail, Activity Log)

## Normalizacao de Dados
- [ ] Timestamps normalizados para fuso horario unico (UTC)
- [ ] Formato de log normalizado para parsing consistente
- [ ] Hostname/IP resolution aplicada para identificacao de assets
- [ ] User identity correlated entre diferentes log sources
- [ ] Duplicatas removidas entre fontes sobrepostas
- [ ] Gaps temporais em logs identificados e documentados

## Construcao da Timeline
- [ ] Evento initial (first known malicious activity) identificado
- [ ] Eventos sequenciados cronologicamente
- [ ] Cada evento com: timestamp, source, actor, action, target, result
- [ ] Causal relationships entre eventos documentadas
- [ ] Lateral movement steps mapeados na timeline
- [ ] Data access/exfiltration events destacados
- [ ] Persistence mechanisms mapped com timestamp de criacao
- [ ] C2 communication patterns correlacionados na timeline

## Analise da Timeline
- [ ] Dwell time calculado (initial compromise to detection)
- [ ] Kill chain phases mapeadas na timeline
- [ ] MITRE ATT&CK techniques associadas a cada fase
- [ ] Gaps na timeline identificados e investigados
- [ ] Eventos anomalos que nao se encaixam no padrao investigados
- [ ] Impact assessment baseado na timeline definido
- [ ] Response actions mapeadas na timeline

## Validacao
- [ ] Timeline revisada por segundo analista
- [ ] Eventos-chave validados com multiple log sources
- [ ] Hipoteses alternativas consideradas e descartadas/confirmadas
- [ ] Timeline consistente com IOCs e threat intelligence
- [ ] Stakeholders revisaram timeline para contexto de negocio

## Documentacao e Apresentacao
- [ ] Timeline visual criada (ferramenta ou diagrama)
- [ ] Executive summary da timeline preparado
- [ ] Timeline exportada em formato estruturado (CSV, JSON)
- [ ] Key findings da timeline destacados no incident report
- [ ] Timeline preservada como evidencia do incidente
- [ ] Lessons learned derivadas da analise temporal
