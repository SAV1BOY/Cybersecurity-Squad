# Privilege Escalation Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para identificacao e exploracao de vetores de escalacao de privilegios
em sistemas Linux e Windows. Cobre tecnicas de kernel, servicos, permissoes e tokens.
Aplicavel somente em ambientes com autorizacao formal para testes ofensivos.

## Requisitos de Autorizacao
- Escopo aprovado incluindo sistemas-alvo especificos
- Permissao explicita para execucao de exploits de escalacao
- Ambiente isolado ou janela de manutencao acordada
- Contato de emergencia para rollback imediato
- Documentacao de estado inicial dos sistemas antes dos testes

## Etapas da Metodologia — Linux

### 1. Enumeracao Inicial
- Verificacao de kernel version e distribuicao (uname -a)
- Listagem de SUID/SGID binaries e analise de exploitability
- Revisao de sudo permissions (sudo -l) e misconfigurations
- Identificacao de cron jobs com permissoes inseguras

### 2. Kernel Exploits
- Correlacao de kernel version com CVEs conhecidos
- Validacao de exploit applicability no ambiente-alvo
- Execucao controlada com monitoramento de estabilidade do sistema

### 3. SUID/Sudo Abuse
- Exploracao de binarios SUID com funcionalidades de shell escape
- Abuso de sudo rules permissivas (ex: wildcards, NOPASSWD)
- Exploracao de PATH hijacking em scripts executados como root

### 4. Service Exploitation
- Identificacao de servicos rodando como root com configuracoes fracas
- Writable service files e unit files (systemd)
- Abuso de capabilities atribuidas incorretamente

## Etapas da Metodologia — Windows

### 5. Service Misconfiguration
- Unquoted service paths com diretorios graváveis
- Weak service permissions (modifiable service binaries)
- DLL hijacking em aplicacoes privilegiadas

### 6. Token Impersonation
- SeImpersonatePrivilege e SeAssignPrimaryTokenPrivilege abuse
- Potato family attacks (JuicyPotato, PrintSpoofer, GodPotato)
- Token manipulation via process injection

### 7. Registry e Scheduled Tasks
- AlwaysInstallElevated policy exploitation
- Modifiable scheduled tasks com execucao privilegiada
- Stored credentials em registry keys

### 8. UAC Bypass
- Tecnicas de bypass para User Account Control
- Auto-elevation abusando trusted binaries
- Environment variable injection em processos elevados

## Ferramentas de Referencia
- LinPEAS, WinPEAS, Linux Exploit Suggester, BeRoot, PowerUp, SharpUp
- GTFOBins (referencia SUID/sudo), LOLBAS (Living Off The Land Binaries)

## Contrapartida de Deteccao (Blue Team)
- Monitoramento de processos filhos anomalos de servicos privilegiados
- Alerta para criacao de novos servicos ou scheduled tasks
- Deteccao de SUID bit changes e modificacoes em /etc/sudoers
- Auditoria de Event ID 4672 (special privileges assigned) no Windows
- Baseline de processos normais para identificar anomalias

## Integracao com Outros Frameworks
- Recebe de: credential-attack-methodology.md (acesso inicial)
- Alimenta: lateral-movement-methodology.md (privilegios obtidos)
- Alimenta: persistence-analysis-methodology.md (manutencao de acesso)
- Correlaciona com: container-security-methodology.md (container escape)
