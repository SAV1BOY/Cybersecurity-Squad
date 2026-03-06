# Active Directory Attack & Defense Lab

## Objetivo
Ambiente dedicado para pratica de ataques e defesas em ambientes Active
Directory, cobrindo desde enumeration ate domain dominance e deteccao.

## Arquitetura do AD Lab

### Domain Controllers
- **DC01**: Windows Server 2022 (Primary DC)
- **DC02**: Windows Server 2019 (Secondary DC)
- **Forest**: corp.lab.local
- **Child Domain**: dev.corp.lab.local (optional)

### Member Servers
- **SRV-FILE**: file server com shares
- **SRV-SQL**: SQL Server com databases
- **SRV-WEB**: IIS com aplicacoes web
- **SRV-EXCHANGE**: Exchange Server (optional)

### Workstations
- **WS01-WS05**: Windows 10/11 joined ao dominio
- **Usuarios**: 50+ usuarios com diferentes privilegios
- **GPOs**: politicas variadas simulando ambiente real

### Misconfiguration Intencional
- Kerberoastable service accounts
- AS-REP roastable users
- Unconstrained delegation em servidores
- SPN configurations vulneraveis
- Senhas em Group Policy Preferences
- AdminCount em usuarios desnecessarios

## Attack Path Exercises

### Reconnaissance
- BloodHound/SharpHound collection
- PowerView enumeration
- LDAP queries manuais
- DNS enumeration

### Credential Access
- Kerberoasting (Rubeus, Impacket)
- AS-REP Roasting
- NTLM relay attacks (Responder + ntlmrelayx)
- Password spraying
- DCSync (Mimikatz, secretsdump)

### Lateral Movement
- Pass-the-Hash (PtH)
- Pass-the-Ticket (PtT)
- Overpass-the-Hash
- WMI/PSRemoting/SMB lateral movement
- DCOM-based lateral movement

### Privilege Escalation
- Token impersonation
- GPO abuse
- ACL/DACL abuse
- Certificate abuse (AD CS - ESC1-ESC8)
- Constrained/Unconstrained delegation abuse

### Domain Dominance
- Golden Ticket
- Silver Ticket
- Diamond Ticket
- Skeleton Key
- AdminSDHolder persistence

## Defensive Measures para Praticar
- Sysmon deployment e tuning
- Windows Event Log monitoring
- BloodHound para defensive assessment
- Tiered administration model
- LAPS deployment
- Credential Guard
- Protected Users group

## Ferramentas
- **Ofensivo**: BloodHound, Rubeus, Mimikatz, Impacket, CrackMapExec
- **Defensivo**: Sysmon, Elastic Security, PingCastle, Purple Knight

## Notas do Squad
AD security e uma das areas mais demandadas no mercado brasileiro. Manter
o lab atualizado com novas tecnicas de ataque e defesa.
