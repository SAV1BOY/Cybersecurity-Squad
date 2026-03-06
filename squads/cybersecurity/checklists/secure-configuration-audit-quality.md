# Secure Configuration Audit Quality Gate

Checklist de qualidade para auditoria de configuracao segura.

## Baseline e Referencia
- [ ] CIS Benchmark aplicavel identificado para cada tecnologia
- [ ] Versao do benchmark documentada
- [ ] Scope de sistemas a auditar definido e aprovado
- [ ] Automated scanning tools configurados (CIS-CAT, Lynis, InSpec)
- [ ] Custom policies adicionadas para requisitos internos

## Operating System Hardening
- [ ] Unnecessary services desabilitados
- [ ] Local firewall configurado e ativo
- [ ] Patch level verificado e atualizado
- [ ] User accounts auditados (default, unused, shared)
- [ ] Password policies enforced conforme baseline
- [ ] SSH/RDP hardening verificado (key-based auth, protocol version)
- [ ] File system permissions revisados para sensitive files
- [ ] Audit logging habilitado e configurado

## Network Device Configuration
- [ ] Default credentials alterados em todos os devices
- [ ] Management interfaces restritas a redes de gerencia
- [ ] SNMP community strings alterados ou SNMPv3 enforced
- [ ] Firmware/software version atualizado
- [ ] ACLs revisadas para regras excessivamente permissivas
- [ ] NTP sincronizado com fonte confiavel
- [ ] Unused ports desabilitados

## Database Hardening
- [ ] Default accounts desabilitados ou removidos
- [ ] Encryption at rest habilitada
- [ ] Network listener restrito a interfaces necessarias
- [ ] Audit logging habilitado para operacoes privilegiadas
- [ ] Backup encryption verificada
- [ ] Patch level do database verificado

## Application Server Hardening
- [ ] Default pages e admin consoles removidos ou restritos
- [ ] Directory listing desabilitado
- [ ] Error handling configurado sem information disclosure
- [ ] TLS configuration endurecida (protocols, ciphers)
- [ ] Security headers configurados
- [ ] Log rotation e retention configurados

## Documentacao e Remediation
- [ ] Compliance score calculado por sistema e por controle
- [ ] Deviations justificadas e documentadas como accepted risk
- [ ] Remediation plan priorizado por risco e esforco
- [ ] Evidence de cada verificacao armazenada
- [ ] Report comparativo com auditoria anterior (se existente)
- [ ] Findings apresentados ao time responsavel
