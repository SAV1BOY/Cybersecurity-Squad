# Red Team - Operator Notes Standard

Checklist para padronizacao de anotacoes de operadores de red team.

## Formato de Notas
- [ ] Timestamp (UTC) registrado para cada acao
- [ ] Operator callsign/name identificado em cada entrada
- [ ] Target system identificado (hostname, IP)
- [ ] Acao executada descrita claramente
- [ ] Resultado da acao registrado (success, fail, partial)
- [ ] Tool utilizado e versao documentados
- [ ] Command line exato registrado (copy/paste ready)

## Conteudo por Fase
- [ ] Recon notes com sources e findings organizados
- [ ] Initial access method documentado em detalhe
- [ ] Privilege escalation path documentado step-by-step
- [ ] Lateral movement cada hop registrado (source -> dest, method)
- [ ] Credential access method e credentials obtidos (encrypted)
- [ ] Persistence mechanisms instalados (location, type, trigger)
- [ ] Collection e exfiltration activities registradas
- [ ] Objective completion evidence documentada

## Infraestrutura do Operador
- [ ] C2 server e channel details documentados
- [ ] Redirector chain documentada
- [ ] Domains e IPs utilizados catalogados
- [ ] Payloads deployados com hash e filename
- [ ] Callback configurations registradas
- [ ] Infrastructure changes logged com timestamp

## OPSEC Notes
- [ ] Detection avoidance techniques utilizadas documentadas
- [ ] Blue team detections observadas registradas
- [ ] EDR/AV encounters e bypasses documentados
- [ ] Network monitoring evasion techniques anotadas
- [ ] Operational mistakes e suas consequencias registradas
- [ ] Cover stories utilizadas em social engineering documentadas

## Evidence Linking
- [ ] Cada nota linkada a screenshot ou log output
- [ ] Evidence files nomeados com convencao padrao
- [ ] Cross-references entre notas de diferentes operadores
- [ ] MITRE ATT&CK technique ID associado a cada acao
- [ ] Finding ID atribuido para items que serao reportados

## Qualidade e Review
- [ ] Notas revisadas diariamente para completude
- [ ] Outro operador pode reproduzir acoes a partir das notas
- [ ] Notas armazenadas em sistema seguro com access control
- [ ] Backup de notas realizado diariamente
- [ ] Notas exportadas para report generation ao final
- [ ] Operator notes revisadas em debrief session
- [ ] Template padrao de notas utilizado por todos os operadores
