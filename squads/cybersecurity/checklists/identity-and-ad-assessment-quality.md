# Identity & AD Assessment Quality Gate

Checklist de qualidade para avaliacao de Active Directory e Identity.

## Enumeracao e Reconhecimento
- [ ] Domain structure mapeada (forests, trusts, child domains)
- [ ] Domain Controllers identificados e versionados
- [ ] Functional level do domain verificado
- [ ] Group Policy Objects (GPOs) enumerados
- [ ] Organizational Units (OUs) structure documentada
- [ ] BloodHound/SharpHound collection executada e analisada

## Privilege Analysis
- [ ] Domain Admins enumerados e justificados
- [ ] Enterprise Admins e Schema Admins auditados
- [ ] Nested group memberships analisadas para privilege escalation
- [ ] Service accounts com excessive privileges identificados
- [ ] Kerberoastable accounts identificados e avaliados
- [ ] AS-REP roastable accounts identificados
- [ ] Delegation configurations (constrained, unconstrained) auditadas
- [ ] AdminSDHolder e SDProp abuse paths verificados

## Authentication Security
- [ ] Password policy verificada (complexity, length, history, lockout)
- [ ] NTLM usage avaliado e restricoes recomendadas
- [ ] Kerberos configuration auditada (encryption types, ticket lifetime)
- [ ] LAPS deployment verificado para local admin passwords
- [ ] Credential caching policy revisada
- [ ] MFA enforcement para acesso privilegiado verificado

## Attack Path Analysis
- [ ] Shortest path to Domain Admin mapeado
- [ ] ACL-based attack paths identificados (WriteDACL, GenericAll)
- [ ] Certificate Services (ADCS) abuse paths testados
- [ ] GPO abuse paths verificados
- [ ] Trust relationship abuse paths analisados
- [ ] DCSync rights auditados

## Hardening e Configuration
- [ ] LDAP signing e channel binding verificados
- [ ] SMB signing enforced em Domain Controllers
- [ ] Protected Users group utilizado para privileged accounts
- [ ] Tiered admin model avaliado (Tier 0, 1, 2)
- [ ] Print Spooler desabilitado em DCs
- [ ] Legacy protocols desabilitados (NTLMv1, LM hash storage)

## Documentacao
- [ ] Attack paths documentados com impacto e remediation
- [ ] Findings priorizados por criticidade e facilidade de exploracao
- [ ] BloodHound graphs exportados como evidencia
- [ ] Recommendations alinhadas com Microsoft tiering model
