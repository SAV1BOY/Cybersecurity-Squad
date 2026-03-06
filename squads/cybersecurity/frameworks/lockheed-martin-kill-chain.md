# Lockheed Martin Cyber Kill Chain

## Overview

A Cyber Kill Chain e um modelo desenvolvido pela Lockheed Martin em 2011 que descreve as fases sequenciais de um ataque cibernetico direcionado. Baseado no conceito militar de kill chain, o modelo identifica sete fases que um adversario deve completar para atingir seu objetivo. O principal valor do framework esta na premissa de que interromper qualquer fase da cadeia impede o sucesso do ataque completo, permitindo que defensores priorizem investimentos em controles que quebram a cadeia o mais cedo possivel.

## Core Concepts

### As 7 Fases

#### 1. Reconnaissance

O adversario pesquisa e identifica alvos potenciais. Coleta informacoes publicas sobre a organizacao, funcionarios, tecnologias e vulnerabilidades. Inclui OSINT, scanning de infraestrutura publica e engenharia social passiva.

**Indicadores defensivos:** Queries incomuns em DNS, scanning de portas, acesso a paginas de erro e crawling de websites corporativos.

#### 2. Weaponization

O adversario cria o payload malicioso combinando um exploit com um backdoor. Tipicamente envolve a criacao de documentos armados (PDF, Office), scripts maliciosos ou binarios customizados. Esta fase ocorre inteiramente no ambiente do atacante.

**Indicadores defensivos:** Limitados nesta fase pois a atividade ocorre fora do perimetro da vitima. Threat intelligence sobre ferramentas e TTPs de adversarios relevantes e o principal mecanismo.

#### 3. Delivery

O adversario transmite o payload para o ambiente alvo. Vetores comuns incluem email com anexo malicioso (spear phishing), websites comprometidos (watering hole) e midias removiveis (USB drop).

**Indicadores defensivos:** Emails com anexos suspeitos, URLs maliciosas, downloads de fontes nao confiaveis e conexoes USB nao autorizadas.

#### 4. Exploitation

O payload explora uma vulnerabilidade no sistema alvo para executar codigo. Pode explorar vulnerabilidades de software (CVEs), configuracoes inseguras ou o fator humano (usuario habilitando macros).

**Indicadores defensivos:** Crash de aplicacoes, comportamento anomalo de processos, tentativas de exploracao detectadas por IDS/IPS e alertas de EDR.

#### 5. Installation

O adversario instala um backdoor ou implante persistente no sistema comprometido. Utiliza mecanismos de persistencia como scheduled tasks, registry keys, services e rootkits.

**Indicadores defensivos:** Novos arquivos em diretorios de sistema, modificacoes em chaves de registro de autorun, novos servicos e tarefas agendadas.

#### 6. Command and Control (C2)

O implante estabelece comunicacao com a infraestrutura de comando e controle do adversario. Utiliza protocolos comuns como HTTP/HTTPS, DNS e cloud services para evadir deteccao.

**Indicadores defensivos:** Beaconing periodico, comunicacao com dominios recentemente registrados, tunelamento DNS e trafego anomalo para cloud services.

#### 7. Actions on Objectives

O adversario executa seus objetivos finais: exfiltracao de dados, destruicao de informacoes, ransomware, espionagem ou sabotagem. Esta e a unica fase onde o impacto ao negocio se materializa.

**Indicadores defensivos:** Transferencias de dados incomuns, acesso a dados sensiveis fora do padrao, criptografia de arquivos em massa e movimentacao lateral.

## Practical Application

### Defesa em Cada Fase

| Fase | Controle Primario | Acao Defensiva |
|------|-------------------|----------------|
| Reconnaissance | Reducao de superficie | Minimizar exposicao de informacoes publicas |
| Weaponization | Threat Intelligence | Monitorar TTPs de adversarios relevantes |
| Delivery | Email/Web Security | Filtrar anexos maliciosos e URLs suspeitas |
| Exploitation | Patch Management | Manter sistemas atualizados e hardened |
| Installation | Endpoint Protection | EDR com deteccao de persistence mechanisms |
| C2 | Network Monitoring | Deteccao de beaconing e C2 traffic |
| Actions | Data Protection | DLP, segmentacao de rede e monitoring |

### Estrategia de Intelligence-Driven Defense

1. Mapear adversarios relevantes e suas TTPs preferidas por fase da kill chain.
2. Identificar controles existentes e gaps de deteccao em cada fase.
3. Priorizar investimentos nas fases mais a esquerda (earlier in the chain) para maximize disrupcao.
4. Criar indicadores de deteccao especificos para cada fase baseados em threat intelligence.
5. Medir eficacia dos controles por fase com exercicios de red team e purple team.
6. Iterar e fortalecer controles conforme adversarios adaptam suas taticas.

### Limitacoes do Modelo

- Foco em ataques direcionados externos, nao cobrindo bem insider threats.
- Visao linear que nao captura bem ataques multi-vetor simultaneos.
- Limitado para ataques que nao seguem sequencia tradicional (supply chain, cloud-native).
- Complementado pelo MITRE ATT&CK que oferece granularidade superior por fase.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O defense-layer organiza controles de deteccao mapeados as sete fases da kill chain.
- O offense-layer planeja engagements de red team cobrindo todas as fases para validar defesas.
- O detection-coverage-matrix cruza fases da kill chain com tecnicas ATT&CK para cobertura completa.
- O ir-layer utiliza a kill chain para classificar em qual fase um incidente foi detectado.
- O mitre-att-ck fornece granularidade tecnica dentro de cada fase da kill chain.
- O purple-team-method testa controles fase a fase em ciclos iterativos de melhoria.
- O security-kpi-dashboard exibe a fase media de deteccao como metrica de eficacia defensiva.
- O diamond-model complementa a kill chain com analise contextual de cada intrusao.
