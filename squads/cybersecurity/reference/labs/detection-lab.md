# Detection Lab - Ambiente de Engenharia de Deteccao

## Objetivo
Ambiente dedicado para desenvolvimento, teste e validacao de regras de deteccao,
threat hunting hypotheses e playbooks de resposta.

## Arquitetura do Detection Lab

### Componentes Core
- **SIEM**: Elastic Security ou Splunk (dev license)
- **Log Collector**: Filebeat, Winlogbeat, Sysmon
- **Network Monitor**: Zeek + Suricata
- **Endpoint Agent**: Wazuh ou Elastic Agent
- **Threat Intel**: MISP (Malware Information Sharing Platform)

### Geradores de Telemetria
- Windows Domain (DC + Workstations com Sysmon)
- Linux servers com auditd configurado
- Web application stack (Apache/Nginx + app)
- Network traffic generators

### Attack Simulation
- Atomic Red Team (testes atomicos por tecnica ATT&CK)
- MITRE Caldera (adversary emulation automatizada)
- Infection Monkey (breach and attack simulation)
- Manual attack execution com ferramentas do squad

## Workflow de Detection Engineering

### 1. Hypothesis
- Identificar tecnica ATT&CK a detectar
- Pesquisar data sources necessarios
- Definir logica de deteccao esperada

### 2. Data Validation
- Verificar se logs necessarios estao sendo coletados
- Validar campos e formatos de dados
- Garantir cobertura de telemetria

### 3. Rule Development
- Escrever regra em formato Sigma
- Converter para linguagem do SIEM target
- Documentar logica e rationale

### 4. Testing
- Executar tecnica com Atomic Red Team
- Verificar se regra dispara corretamente
- Testar contra dados normais (false positive check)

### 5. Tuning
- Ajustar para reduzir false positives
- Adicionar exclusoes documentadas
- Validar que true positives nao sao perdidos

### 6. Deployment
- Promover regra para producao
- Monitorar performance e eficacia
- Iterar baseado em feedback

## Metricas do Detection Lab
- Cobertura ATT&CK (% de tecnicas com deteccao)
- False positive rate por regra
- Mean time to detect (MTTD) por cenario
- Numero de regras em producao vs em desenvolvimento

## Ferramentas Complementares
- ATT&CK Navigator para visualizar cobertura
- DeTT&CT para mapear data sources
- Sigma CLI para conversao de regras
- Git para versionamento de regras

## Notas do Squad
O Detection Lab deve ser tratado como ambiente de desenvolvimento critico.
Manter paridade com producao em termos de log sources e configuracoes.
