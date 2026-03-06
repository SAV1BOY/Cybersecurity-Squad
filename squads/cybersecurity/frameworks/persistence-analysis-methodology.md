# Persistence Analysis Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de vetores de persistencia em sistemas operacionais e
ambientes cloud. Foca na identificacao de mecanismos que permitem manter acesso
apos reinicializacao ou remediacao parcial. Uso exclusivo em testes autorizados.

## Requisitos de Autorizacao
- Permissao explicita para implantacao de mecanismos de persistencia de teste
- Acordo sobre remocao completa apos finalizacao dos testes
- Documentacao de cada artefato implantado com localizacao e metodo
- Validacao de que mecanismos nao impactam operacoes de producao
- Checklist de cleanup obrigatorio pos-teste

## Etapas da Metodologia — Windows

### 1. Startup e Registry Persistence
- Analise de Run/RunOnce keys (HKLM e HKCU)
- Verificacao de Startup folders e shell extensions
- Winlogon keys, AppInit_DLLs e Image File Execution Options
- COM object hijacking e DLL search order abuse

### 2. Scheduled Tasks e Services
- Criacao de scheduled tasks com triggers de logon ou tempo
- Registro de servicos com startup type automatico
- WMI event subscriptions para execucao baseada em eventos
- Analise de Group Policy Objects para persistence domain-wide

### 3. Outras Tecnicas Windows
- BITS jobs persistentes para download e execucao
- Office application startup (macros, add-ins, templates)
- Print monitor e port monitor DLL injection
- Active Setup e Accessibility Features abuse

## Etapas da Metodologia — Linux

### 4. Cron e Systemd
- Implantacao em crontab de usuario e sistema (/etc/cron.d)
- Criacao de systemd services e timers customizados
- Manipulacao de init scripts (/etc/init.d, /etc/rc.local)
- XDG autostart entries para ambientes com desktop

### 5. Shell e Profile Persistence
- Modificacao de .bashrc, .profile, .bash_logout
- LD_PRELOAD e shared library injection
- SSH authorized_keys e configuracoes de acesso
- PAM module backdoors para interceptacao de credenciais

## Etapas da Metodologia — Cloud

### 6. Cloud Persistence
- Criacao de IAM users/roles backdoor com credenciais de longo prazo
- Lambda/Cloud Functions com triggers automaticos
- Modificacao de automation runbooks e pipelines
- OAuth app registrations com permissoes excessivas

## Ferramentas de Referencia
- Autoruns (Sysinternals), PersistenceSniper, DVTA, SharPersist
- pspy (Linux process monitoring), Volatility (memory analysis)

## Contrapartida de Deteccao (Blue Team)
- Baseline de scheduled tasks, services e registry keys criticos
- Monitoramento de Event ID 4698 (task created) e 7045 (service installed)
- File integrity monitoring em diretorios de startup e configuracao
- Auditoria periodica de IAM entities e OAuth applications em cloud
- Analise de autoruns diff entre baselines conhecidos

## Integracao com Outros Frameworks
- Recebe de: lateral-movement-methodology.md (acesso a novos hosts)
- Recebe de: privilege-escalation-methodology.md (privilegios para persistir)
- Correlaciona com: active-directory-attack-defense.md (GPO persistence)
- Correlaciona com: cloud-identity-attack-defense.md (cloud persistence)
