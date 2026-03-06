# Active Directory Attack & Defense

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia integrada de ataque e defesa para ambientes Active Directory. Cobre
enumeracao, abuso de delegacao, exploracoes Kerberos, DCSync e defesas correspondentes.
Perspectiva dual Red Team e Blue Team para avaliacao completa do ambiente AD.

## Requisitos de Autorizacao
- Aprovacao do Domain Admin ou equipe responsavel pelo AD
- Escopo definido: dominios, OUs, florestas autorizadas para teste
- Ambiente de DR ou snapshot disponivel antes de testes destrutivos
- Monitoramento ativo durante execucao dos testes
- Plano de reversao para cada modificacao realizada no AD

## Etapas de Ataque (Red Team)

### 1. Enumeracao de Active Directory
- Coleta de informacoes via LDAP queries (usuarios, grupos, GPOs)
- Mapeamento de relacoes de confianca (trusts) entre dominios
- Identificacao de privileged groups e seus membros
- Analise de ACLs e DACLs para identificar misconfigured permissions

### 2. Abuso de Delegacao
- Unconstrained delegation: comprometimento de hosts com TGT forwarding
- Constrained delegation: abuso de S4U2Self e S4U2Proxy
- Resource-based constrained delegation (RBCD) exploitation
- Identificacao de machine accounts com delegacao configurada

### 3. Kerberos Attacks
- Kerberoasting de service accounts com SPNs definidos
- AS-REP Roasting de contas sem pre-autenticacao
- Golden Ticket: forja de TGT com KRBTGT hash
- Silver Ticket: forja de TGS para servicos especificos
- Diamond Ticket e Sapphire Ticket para evasao de deteccao

### 4. DCSync e Credential Dumping
- DCSync para replicacao de hashes do NTDS.dit
- NTDS.dit extraction via Volume Shadow Copy
- LSASS memory dumping para obtencao de credenciais em cache
- Secretsdump para extracao completa de segredos do dominio

### 5. Trust Exploitation
- SID History injection para escalacao cross-domain
- Abuso de forest trusts com selective authentication
- PAM Trust exploitation em ambientes com Privileged Access Management

## Etapas de Defesa (Blue Team)

### 6. Hardening e Deteccao
- Implementacao de tiered administration model (Tier 0/1/2)
- Protected Users group para contas privilegiadas
- Monitoramento de Event IDs: 4662 (DCSync), 4769 (Kerberoasting)
- LAPS deployment para randomizacao de senhas locais
- Credential Guard para protecao de LSASS

### 7. Monitoramento Avancado
- Deteccao de Golden Ticket via TGT lifetime anomalies
- Alertas para modificacoes em AdminSDHolder e KRBTGT
- Auditoria de delegacao changes e ACL modifications
- BloodHound defensivo para identificacao de attack paths

## Ferramentas de Referencia
- BloodHound/SharpHound, Impacket, Rubeus, Mimikatz, ADRecon
- PingCastle, Purple Knight (avaliacao defensiva de AD)

## Integracao com Outros Frameworks
- Alimenta: credential-attack-methodology.md (Kerberos attacks)
- Alimenta: lateral-movement-methodology.md (delegacao abuse)
- Alimenta: persistence-analysis-methodology.md (GPO persistence)
- Correlaciona com: cloud-identity-attack-defense.md (hybrid identity)
