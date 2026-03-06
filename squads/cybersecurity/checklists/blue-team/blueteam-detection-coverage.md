# Blue Team - Detection Coverage

Checklist para avaliacao de cobertura de deteccao.

## Framework de Cobertura
- [ ] MITRE ATT&CK matrix utilizado como framework de referencia
- [ ] Detection rules mapeadas a ATT&CK techniques
- [ ] ATT&CK Navigator heatmap gerado com cobertura atual
- [ ] Tactics com menor cobertura identificadas como gaps
- [ ] Top threats para o setor priorizadas na cobertura
- [ ] Coverage score calculado (techniques covered / total relevant)

## Detection por Tactic
- [ ] Initial Access: phishing, exploit public apps, valid accounts
- [ ] Execution: PowerShell, script interpreters, scheduled tasks
- [ ] Persistence: registry run keys, scheduled tasks, services
- [ ] Privilege Escalation: token manipulation, exploits, UAC bypass
- [ ] Defense Evasion: obfuscation, disabling tools, process injection
- [ ] Credential Access: credential dumping, brute force, kerberoasting
- [ ] Discovery: network scanning, account enumeration, system info
- [ ] Lateral Movement: RDP, SMB, WMI, PsExec
- [ ] Collection: data from local system, email collection
- [ ] Exfiltration: over C2 channel, to cloud, over web service
- [ ] Command and Control: beaconing, DNS tunneling, HTTPS C2

## Tipos de Detection
- [ ] Signature-based rules implementadas (IOCs, hashes, IPs)
- [ ] Behavior-based rules implementadas (anomaly, pattern)
- [ ] Statistical baseline detections configuradas
- [ ] ML/AI-based detections habilitadas (se disponivel)
- [ ] Threat hunting queries disponíveis para gaps de automation
- [ ] Correlation rules para multi-stage attacks implementadas

## Validacao de Deteccoes
- [ ] Atomic Red Team tests executados para cada detection rule
- [ ] True positive rate medido e documentado por rule
- [ ] False positive rate medido e dentro de limites aceitaveis
- [ ] Detection rules testadas apos cada SIEM update
- [ ] Purple team exercises validam detection effectiveness
- [ ] Time to detect medido para cada categoria de deteccao

## Gap Analysis
- [ ] ATT&CK techniques sem deteccao listadas
- [ ] Gap por data source insuficiente vs gap por falta de regra
- [ ] Priorizacao de gaps por threat likelihood e impact
- [ ] Remediation plan para fechar gaps prioritarios
- [ ] Budget e resource needs para gap closure estimados

## Lifecycle Management
- [ ] Detection rule creation process documentado
- [ ] Detection rule review cadence definida (quarterly)
- [ ] Deprecated rules arquivadas com justificativa
- [ ] New technique coverage adicionada apos threat intel updates
- [ ] Detection coverage report gerado e compartilhado mensalmente
- [ ] Continuous improvement metrics rastreadas
