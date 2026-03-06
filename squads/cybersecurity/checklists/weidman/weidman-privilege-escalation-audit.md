# Weidman - Privilege Escalation Audit

Checklist para auditoria de vetores de escalacao de privilegios.

## Linux Privilege Escalation
- [ ] Kernel version verificado para known exploits
- [ ] SUID/SGID binaries enumerados e analisados
- [ ] Writable cron jobs e scripts identificados
- [ ] Sudo misconfigurations verificadas (sudo -l)
- [ ] Capabilities em binarios verificadas (getcap)
- [ ] Writable /etc/passwd ou /etc/shadow verificado
- [ ] PATH hijacking opportunities identificadas
- [ ] NFS shares com no_root_squash verificados
- [ ] Docker group membership verificada
- [ ] Writable systemd service files identificados
- [ ] LD_PRELOAD e LD_LIBRARY_PATH abuse paths testados
- [ ] Wildcard injection em cron scripts verificada

## Windows Privilege Escalation
- [ ] Missing patches verificados (Watson, Sherlock)
- [ ] Unquoted service paths identificados
- [ ] Modifiable service binaries ou configs identificados
- [ ] AlwaysInstallElevated registry key verificado
- [ ] Stored credentials procurados (Credential Manager, registry)
- [ ] Token impersonation opportunities (SeImpersonate, SeAssignPrimaryToken)
- [ ] DLL hijacking paths identificados
- [ ] Modifiable scheduled tasks verificadas
- [ ] Auto-logon credentials extraidos
- [ ] UAC bypass techniques testadas
- [ ] PrintSpoofer/PrintNightmare verificados
- [ ] Group Policy Preferences (GPP) passwords verificados

## Validacao de Escalacao
- [ ] Cada vector de privesc testado com cuidado para estabilidade
- [ ] Escalacao confirmada com whoami/id apos exploit
- [ ] Metodo de escalacao documentado step-by-step
- [ ] Impacto da escalacao no servico avaliado
- [ ] Reversibilidade da escalacao verificada
- [ ] Evidence capturada antes e depois da escalacao

## Analise e Reporting
- [ ] Vectors priorizados por facilidade de exploracao
- [ ] Root cause identificado para cada vector (patch, config, design)
- [ ] Remediation steps especificos por vector
- [ ] Automated tools results validados manualmente
- [ ] False positives removidos dos resultados
- [ ] Report de privilege escalation paths entregue com PoCs
