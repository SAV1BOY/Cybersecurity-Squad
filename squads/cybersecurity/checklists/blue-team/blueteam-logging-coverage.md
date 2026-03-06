# Blue Team - Logging Coverage

Checklist para avaliacao de cobertura de logging.

## Endpoint Logging
- [ ] Windows Security Event Log habilitado em todos os endpoints
- [ ] PowerShell Script Block Logging habilitado
- [ ] PowerShell Module Logging habilitado
- [ ] Sysmon deployado com configuracao adequada
- [ ] Process creation logging (Event ID 4688) com command line
- [ ] Linux auditd configurado em servidores Linux
- [ ] macOS Unified Logging configurado (se aplicavel)
- [ ] EDR telemetry fluindo para SIEM

## Network Logging
- [ ] Firewall logs (allow e deny) coletados
- [ ] Proxy/web filter logs com full URL coletados
- [ ] DNS query logs coletados (recursive resolver)
- [ ] IDS/IPS alert logs coletados
- [ ] NetFlow/IPFIX data coletado
- [ ] VPN connection logs coletados
- [ ] DHCP lease logs coletados
- [ ] Load balancer/WAF logs coletados

## Identity e Authentication
- [ ] Active Directory authentication logs coletados
- [ ] Failed logon attempts registrados (Event ID 4625)
- [ ] Privileged account usage logado (Event ID 4672)
- [ ] Group membership changes logados
- [ ] Password change/reset events logados
- [ ] MFA logs coletados
- [ ] SSO/Federation logs coletados
- [ ] Service account activity logada

## Cloud Logging
- [ ] AWS CloudTrail habilitado em todas as regions
- [ ] Azure Activity Log e Azure AD Sign-in Logs coletados
- [ ] GCP Cloud Audit Logs habilitados
- [ ] O365/M365 Unified Audit Log habilitado
- [ ] Cloud storage access logs habilitados
- [ ] Cloud networking flow logs habilitados
- [ ] SaaS application audit logs coletados

## Application Logging
- [ ] Web application access logs coletados
- [ ] Application error logs coletados
- [ ] Database audit logs habilitados para DBs criticos
- [ ] API gateway logs coletados
- [ ] Container/Kubernetes audit logs coletados
- [ ] CI/CD pipeline logs coletados

## Validacao e Manutencao
- [ ] Log collection health dashboard operacional
- [ ] Alertas para log source failures configurados
- [ ] Log retention adequada (90 dias hot, 1 ano cold minimo)
- [ ] Log integrity protegida (immutable storage, WORM)
- [ ] Log normalization e parsing validados no SIEM
- [ ] Coverage gaps documentados com remediation plan
- [ ] Logging coverage revisada trimestralmente
