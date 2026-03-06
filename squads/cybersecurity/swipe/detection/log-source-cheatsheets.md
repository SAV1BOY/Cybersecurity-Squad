# Log Source Cheatsheets

Referencia rapida de log sources essenciais e campos relevantes para deteccao.

## Windows Event Logs

| Event ID | Descricao | Uso em Deteccao |
|----------|-----------|-----------------|
| 4624 | Successful Logon | Baseline de autenticacao, impossible travel |
| 4625 | Failed Logon | Brute force, password spraying |
| 4672 | Special Privileges Assigned | Privilege escalation monitoring |
| 4688 | Process Creation | Command line auditing (requer GPO) |
| 4720 | User Account Created | Unauthorized account creation |
| 7045 | Service Installed | Persistence via services |

## Linux Audit Logs

- `/var/log/auth.log` - SSH attempts, sudo usage, su commands
- `/var/log/syslog` - System events, service starts/stops
- `auditd` com regras para execve, file access, network connections
- `journalctl` para systemd service events

## Cloud Logs (AWS)

| Log Source | Eventos-Chave |
|-----------|---------------|
| CloudTrail | API calls, console logins, IAM changes |
| VPC Flow Logs | Network traffic metadata, exfiltration detection |
| GuardDuty | Threat findings pre-processados |
| S3 Access Logs | Data access patterns, public access attempts |

## Network Logs

- **Firewall:** Blocked connections, geo-anomalies, port scans
- **DNS:** Domain queries para DGA detection, tunneling
- **Proxy/WAF:** HTTP requests, SQL injection attempts, XSS patterns
- **NetFlow:** Volume anomalies, beaconing patterns

## Dicas de Ingestao

- Normalizar campos com schema padrao (ECS, OCSF)
- Definir retention policy por criticidade do log source
- Monitorar log source health (gaps de ingestao = blind spots)
