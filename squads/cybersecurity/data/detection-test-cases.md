# Detection Test Cases

Casos de teste para validacao de regras de deteccao e capacidades do SOC.

## Schema dos Casos de Teste

| Test ID | Detection Rule | MITRE Technique | Test Method | Expected Alert | Pass Criteria |
|---------|---------------|-----------------|-------------|----------------|---------------|
| TC-001 | Brute Force Detection | T1110.001 | 10 failed logins em 60s | ALERT-BF-001 | Alerta gerado em < 5 min |
| TC-002 | Suspicious PowerShell | T1059.001 | Encoded command execution | ALERT-PS-001 | Alerta com command line capturado |
| TC-003 | Lateral Movement SMB | T1021.002 | PsExec remote execution | ALERT-LM-001 | Source e destination IPs no alerta |
| TC-004 | DNS Tunneling | T1048.001 | Iodine tunnel simulation | ALERT-EX-001 | Domain e volume de queries registrados |
| TC-005 | Privilege Escalation | T1068 | Potato exploit simulation | ALERT-PE-001 | Process chain capturado |

## Casos de Teste por Categoria

### Initial Access
- TC-010: Phishing link click com download de payload
- TC-011: Drive-by download via browser exploit
- TC-012: Valid account login de geolocalizacao anomala

### Execution
- TC-020: PowerShell com base64 encoded command
- TC-021: WMI remote execution
- TC-022: Scheduled task creation suspeita

### Persistence
- TC-030: Registry run key modification
- TC-031: New service creation com binary path suspeito
- TC-032: Startup folder modification

### Credential Access
- TC-040: LSASS memory dump via procdump
- TC-041: Kerberoasting (SPN request anomalo)
- TC-042: Credential file access (SAM, NTDS.dit)

## Ferramentas para Teste

- **Atomic Red Team**: Testes atomicos mapeados ao MITRE ATT&CK
- **Caldera**: Simulacao de adversario automatizada
- **Stratus Red Team**: Testes especificos para cloud
- **Custom Scripts**: Scripts internos para cenarios especificos

## Processo de Validacao

1. Executar test case em ambiente controlado
2. Verificar se alerta foi gerado no SIEM/EDR
3. Validar conteudo do alerta (campos esperados)
4. Medir tempo entre execucao e deteccao
5. Documentar resultado e gaps identificados
