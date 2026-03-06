# Diamond Model of Intrusion Analysis

## Overview

O Diamond Model e um framework de analise de intrusoes desenvolvido por Sergio Caltagirone, Andrew Pendergast e Christopher Betz em 2013. O modelo estabelece que todo evento de intrusao pode ser descrito por quatro vertices interconectados formando um diamante: Adversary, Infrastructure, Capability e Victim. Cada intrusao gera um evento atomico que conecta esses vertices, permitindo analise estruturada e pivoting investigativo entre elementos de ameacas ciberneticas.

## Core Concepts

### Os Quatro Vertices

#### 1. Adversary

O ator ou grupo de ameaca responsavel pela intrusao:

- **Adversary Operator** — Individuo que conduz diretamente as acoes tecnicas do ataque.
- **Adversary Customer** — Entidade que se beneficia dos resultados da intrusao (pode ser diferente do operador).
- Adversarios sao caracterizados por motivacao, capacidade tecnica, recursos e atribuicao geopolitica.
- Rastreamento de adversarios permite correlacionar campanhas e prever comportamentos futuros.

#### 2. Infrastructure

Recursos tecnicos utilizados pelo adversario para conduzir o ataque:

- **Type 1 Infrastructure** — Infraestrutura proprietaria do adversario (servidores C2, dominios registrados).
- **Type 2 Infrastructure** — Infraestrutura comprometida de terceiros utilizada como proxy ou pivoting.
- Inclui dominios, enderecos IP, certificados SSL, contas de email e servicos cloud.
- A infraestrutura e frequentemente o vertice mais observavel e rastreavel.

#### 3. Capability

Ferramentas e tecnicas empregadas pelo adversario:

- **Capability Capacity** — O que a ferramenta ou tecnica pode fazer (explorar vulnerabilidade, exfiltrar dados).
- **Adversary Arsenal** — Conjunto completo de capacidades disponiveis ao adversario.
- Inclui malware, exploits, scripts, ferramentas comerciais e tecnicas manuais.
- Capacidades sao mapeadas para tecnicas ATT&CK para padronizacao.

#### 4. Victim

O alvo da intrusao:

- **Victim Persona** — Caracteristicas da organizacao ou individuo alvo (setor, porte, papel).
- **Victim Asset** — Recurso tecnico especifico comprometido (servidor, endpoint, conta de usuario).
- A compreensao do vertice Victim permite antecipar quais organizacoes semelhantes podem ser alvos futuros.

### Meta-Features

Cada evento do Diamond Model possui meta-features que enriquecem a analise:

| Meta-Feature | Descricao |
|--------------|-----------|
| Timestamp | Data e hora do evento de intrusao |
| Phase | Fase do ataque (mapeada para kill chain ou ATT&CK) |
| Result | Sucesso ou falha da acao adversaria |
| Direction | Direcao do evento (inbound, outbound, bidirectional) |
| Methodology | Categoria geral do ataque (phishing, exploitation, brute force) |
| Resources | Recursos gastos pelo adversario (tempo, dinheiro, conhecimento) |

### Activity Threads e Activity Groups

- **Activity Thread** — Sequencia temporal de eventos do Diamond Model que formam uma cadeia de intrusao completa. Cada thread conecta multiplos diamantes em ordem cronologica.
- **Activity Group** — Agrupamento de activity threads que compartilham vertices em comum, permitindo clustering de campanhas e atribuicao de adversarios.

## Practical Application

### Pivoting Investigativo

O poder do Diamond Model esta na capacidade de pivoting entre vertices:

1. **Victim para Infrastructure** — Analisar logs da vitima para identificar IPs e dominios do atacante.
2. **Infrastructure para Adversary** — Consultar WHOIS, passive DNS e threat intel para atribuir infraestrutura.
3. **Infrastructure para Capability** — Analisar malware ou payloads hospedados na infraestrutura identificada.
4. **Capability para Adversary** — Correlacionar ferramentas com grupos conhecidos via signatures e TTPs.
5. **Adversary para Victim** — Identificar outras vitimas potenciais baseado no perfil do adversario.
6. **Capability para Infrastructure** — Mapear C2 servers e download sites associados ao malware.

### Processo de Analise

1. Documentar o evento atomico com os quatro vertices e meta-features.
2. Realizar pivoting a partir do vertice com mais informacao disponivel.
3. Enriquecer vertices usando threat intelligence feeds e bases de dados.
4. Construir o activity thread conectando eventos cronologicamente.
5. Agrupar threads em activity groups para identificar campanhas.
6. Compartilhar indicadores e contexto com a comunidade de CTI.

### Integracao com Outros Modelos

- **Kill Chain** — Cada fase da kill chain pode conter multiplos eventos do Diamond Model.
- **ATT&CK** — Tecnicas ATT&CK enriquecem o vertice Capability com detalhamento tatico.
- **STIX/TAXII** — O formato STIX modela nativamente os vertices do Diamond Model para compartilhamento.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O ir-layer utiliza o Diamond Model para estruturar investigacoes de incidentes com pivoting sistematico.
- O defense-layer alimenta indicadores derivados de pivoting para regras de deteccao no SIEM.
- O offense-layer simula adversarios reais baseando-se em vertices documentados de activity groups.
- O detection-coverage-matrix mapeia deteccoes por capability para garantir visibilidade em ferramentas adversarias.
- O mitre-att-ck complementa o vertice Capability com taxonomia padronizada de tecnicas.
- O lockheed-martin-kill-chain complementa o Diamond Model com visao sequencial de cada activity thread.
- Indicadores de comprometimento derivados de analises Diamond sao compartilhados via threat intel feeds.
- O security-kpi-dashboard rastreia metricas de pivoting como indicador de maturidade de CTI.
