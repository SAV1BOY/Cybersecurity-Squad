# SIEM e SOAR Tooling

## Visao Geral
Ferramentas de Security Information and Event Management (SIEM) e Security
Orchestration, Automation and Response (SOAR) utilizadas pelo squad para
deteccao, investigacao e resposta automatizada.

## SIEM Platforms

### Splunk
- **Tipo**: SIEM enterprise lider de mercado
- **SPL**: Search Processing Language para queries
- **Apps**: Splunk Enterprise Security (ES) para security
- **Uso no Squad**: analise de logs, deteccao, dashboards
- **Dica**: dominar SPL e essencial para analistas

### Elastic Security (ELK Stack)
- **Tipo**: SIEM open-source baseado no Elasticsearch
- **Componentes**: Elasticsearch, Logstash, Kibana, Beats
- **Detection Rules**: regras pre-built alinhadas com ATT&CK
- **Uso no Squad**: SIEM de lab, ambientes com orcamento limitado
- **Diferencial**: custo-beneficio e flexibilidade

### Microsoft Sentinel
- **Tipo**: cloud-native SIEM (Azure)
- **KQL**: Kusto Query Language
- **Integracao**: nativa com ecossistema Microsoft
- **Uso no Squad**: ambientes Microsoft-centric
- **Diferencial**: integracao com Defender suite

### Google Chronicle / SecOps
- **Tipo**: cloud-native security operations platform
- **YARA-L**: linguagem de deteccao propria
- **Uso no Squad**: ambientes Google Cloud
- **Diferencial**: capacidade de retencao e busca

## SOAR Platforms

### XSOAR (Palo Alto)
- **Tipo**: SOAR enterprise
- **Uso**: automacao de playbooks, case management
- **Integracoes**: centenas de integracoes pre-built

### Shuffle
- **Tipo**: SOAR open-source
- **Uso**: automacao de workflows de seguranca
- **Interface**: visual workflow builder
- **Diferencial**: gratuito e auto-hospedado

### TheHive + Cortex
- **Tipo**: incident response platform + analysis engine
- **Uso**: case management e automacao de analise
- **Cortex**: analyzers e responders automatizados
- **Diferencial**: open-source, integracao com MISP

## Detection as Code

### Sigma Rules
- **Tipo**: formato generico para regras de deteccao
- **Uso**: escrever regras portaveis entre SIEMs
- **Conversao**: sigma-cli converte para SPL, KQL, Lucene
- **Repositorio**: SigmaHQ no GitHub

### Detection Engineering Pipeline
1. Escrever regras em Sigma format
2. Testar com Atomic Red Team
3. Converter para SIEM target
4. Deploy via CI/CD
5. Monitorar false positive rate
6. Iterar e refinar

## Log Sources Essenciais
- Windows Event Logs (Security, Sysmon, PowerShell)
- Linux audit logs (auditd, syslog)
- Network logs (firewall, DNS, proxy)
- Cloud logs (CloudTrail, Activity Log)
- Application logs (web servers, databases)
- Authentication logs (AD, SSO, MFA)

## Notas do Squad
Investir em detection engineering como disciplina. Regras de deteccao devem
ser versionadas, testadas e mantidas como codigo.
