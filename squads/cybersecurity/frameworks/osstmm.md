# OSSTMM — Open Source Security Testing Methodology Manual

## Overview

O OSSTMM (Open Source Security Testing Methodology Manual) e uma metodologia de teste de seguranca desenvolvida pelo ISECOM (Institute for Security and Open Methodologies). Diferente de frameworks focados em vulnerabilidades, o OSSTMM e orientado a medicao quantitativa da seguranca operacional. O manual define metricas objetivas para avaliar a superficie de ataque real (Attack Surface) e produz um valor numerico chamado rav (Risk Assessment Value) que representa a seguranca efetiva de um ambiente. A versao 3 e a referencia atual.

## Core Concepts

### Canais de Teste

O OSSTMM organiza testes em cinco canais que cobrem toda a superficie de seguranca:

#### 1. Human Security

Teste do fator humano e engenharia social:

- Avaliacao de conscientizacao e treinamento de seguranca.
- Testes de phishing, vishing, pretexting e baiting.
- Verificacao de processos de verificacao de identidade e controle de visitantes.
- Avaliacao de separacao de funcoes e controle de acesso fisico baseado em pessoas.

#### 2. Physical Security

Teste de seguranca fisica do ambiente:

- Avaliacao de perimetros fisicos, barreiras e controles de acesso.
- Teste de sistemas de vigilancia, alarmes e deteccao de intrusao fisica.
- Verificacao de controle de midias removiveis e descarte seguro.
- Avaliacao de protecao ambiental (incendio, inundacao, energia).

#### 3. Wireless Communications

Teste de comunicacoes sem fio:

- Avaliacao de redes WiFi (WPA3, segmentacao, rogue AP detection).
- Teste de Bluetooth, NFC e comunicacoes de curto alcance.
- Verificacao de RFID e controles de acesso sem fio.
- Avaliacao de emanacoes eletromagneticas (TEMPEST considerations).

#### 4. Telecommunications

Teste de infraestrutura de telecomunicacoes:

- Avaliacao de VoIP e sistemas de telefonia.
- Teste de modems, linhas dedicadas e circuitos de comunicacao.
- Verificacao de seguranca de fax e sistemas de messaging.
- Avaliacao de call routing e voicemail security.

#### 5. Data Networks

Teste de redes de dados e sistemas de informacao:

- Avaliacao de infraestrutura de rede (switches, routers, firewalls).
- Teste de servicos de rede e aplicacoes expostas.
- Verificacao de seguranca de DNS, email e web services.
- Avaliacao de segmentacao de rede e controles de acesso logico.

### Metricas OSSTMM

#### Attack Surface

A superficie de ataque e medida quantitativamente considerando tres dimensoes:

- **Visibility** — Alvos visiveis e enumeraveis pelo atacante.
- **Access** — Pontos de entrada acessiveis no ambiente.
- **Trust** — Relacoes de confianca que podem ser exploradas.

#### Operational Security (OpSec) Controls

Controles medidos em cada canal de teste:

| Controle | Tipo | Descricao |
|----------|------|-----------|
| Authentication | Class A | Verificacao de identidade de entidades |
| Indemnification | Class A | Protecao contra perdas e responsabilidades |
| Subjugation | Class A | Controle de acesso e restricao de acoes |
| Continuity | Class B | Manutencao de operacoes durante interrupcoes |
| Resilience | Class B | Capacidade de recuperacao apos incidentes |
| Non-repudiation | Class A | Garantia de rastreabilidade de acoes |
| Confidentiality | Class A | Protecao contra divulgacao nao autorizada |
| Privacy | Class A | Protecao de informacoes pessoais |
| Integrity | Class A | Protecao contra alteracao nao autorizada |
| Alarm | Class B | Notificacao de eventos de seguranca |

#### RAV (Risk Assessment Value)

O rav e calculado pela formula que relaciona controles operacionais com a superficie de ataque:

- Valores acima de 100 indicam excesso de controles (over-secured).
- Valor de 100 indica equilibrio perfeito entre controles e superficie de ataque.
- Valores abaixo de 100 indicam deficit de controles (under-secured).
- O rav permite comparacao objetiva entre diferentes ambientes e periodos.

## Practical Application

### Processo de Teste OSSTMM

1. Definir escopo identificando canais de teste aplicaveis ao ambiente.
2. Enumerar a superficie de ataque por canal (Visibility, Access, Trust).
3. Identificar e classificar controles operacionais existentes por tipo.
4. Executar testes especificos para validar eficacia de cada controle.
5. Calcular o rav para cada canal e para o ambiente como um todo.
6. Comparar rav com avaliacao anterior para medir evolucao.
7. Documentar resultados com recomendacoes priorizadas por impacto no rav.

### Comparacao com Outras Metodologias

| Aspecto | OSSTMM | PTES | NIST 800-115 |
|---------|--------|------|--------------|
| Foco | Metricas quantitativas | Processo de pentest | Guia tecnico geral |
| Cobertura | 5 canais (fisico a digital) | Rede e aplicacoes | Revisao, scan, pentest |
| Output | rav score numerico | Report qualitativo | Report qualitativo |
| Escopo | Seguranca operacional total | Pentest especifico | Assessment geral |

### Vantagens do Approach Quantitativo

- Permite comparacao objetiva entre avaliacoes em diferentes periodos.
- Facilita comunicacao de postura de seguranca para stakeholders nao tecnicos.
- Identifica over-securing que desperdiça recursos sem beneficio proporcional.
- Mede seguranca efetiva em vez de apenas listar vulnerabilidades.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O offense-layer utiliza o OSSTMM como metodologia complementar ao PTES para assessments abrangentes.
- O risk-scoring-model incorpora o conceito de rav para medicao quantitativa de seguranca.
- O defense-layer mapeia controles operacionais conforme taxonomia OSSTMM para gap analysis.
- O security-kpi-dashboard exibe rav scores por canal para comunicacao executiva.
- O ptes-penetration-testing complementa o OSSTMM com detalhamento especifico de exploitation.
- O nist-800-115-technical-testing fornece orientacoes tecnicas adicionais para os canais de teste.
- O evidence-standard define requisitos de documentacao de evidencia compativeis com metricas OSSTMM.
- Assessments OSSTMM sao conduzidos anualmente cobrindo os cinco canais aplicaveis ao ambiente.
- O discovery-layer alimenta a enumeracao de superficie de ataque requerida pelo OSSTMM.
