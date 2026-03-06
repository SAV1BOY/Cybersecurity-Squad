# MITRE ATT&CK — Adversarial Tactics, Techniques, and Common Knowledge

## Overview

O MITRE ATT&CK e uma base de conhecimento globalmente acessivel de taticas e tecnicas adversarias baseadas em observacoes do mundo real. Mantido pela MITRE Corporation, o framework documenta o comportamento de adversarios ao longo do ciclo de vida de um ataque, organizado em matrizes para Enterprise, Mobile e ICS. E amplamente utilizado para gap analysis de deteccao, emulacao de adversarios, assessment de ferramentas de seguranca e comunicacao de ameacas de forma estruturada.

## Core Concepts

### Estrutura Hierarquica

- **Tactics** — Representam o objetivo do adversario durante um ataque (o "porque"). Sao as colunas da matriz ATT&CK.
- **Techniques** — Descrevem como o adversario atinge um objetivo tatico (o "como"). Cada tecnica pertence a uma ou mais taticas.
- **Sub-techniques** — Variacoes especificas de uma tecnica que detalham implementacoes particulares.
- **Procedures** — Instancias concretas de como um grupo ou malware especifico utiliza uma tecnica.

### As 14 Taticas (Enterprise)

| ID | Tatica | Objetivo |
|----|--------|----------|
| TA0043 | Reconnaissance | Coletar informacoes para planejar operacoes futuras |
| TA0042 | Resource Development | Estabelecer recursos para suportar operacoes |
| TA0001 | Initial Access | Obter acesso inicial ao ambiente alvo |
| TA0002 | Execution | Executar codigo malicioso no sistema alvo |
| TA0003 | Persistence | Manter presenca no ambiente apos reinicializacoes |
| TA0004 | Privilege Escalation | Obter permissoes de nivel mais elevado |
| TA0005 | Defense Evasion | Evitar deteccao por controles de seguranca |
| TA0006 | Credential Access | Roubar credenciais de acesso |
| TA0007 | Discovery | Mapear o ambiente e recursos disponiveis |
| TA0008 | Lateral Movement | Mover-se entre sistemas no ambiente |
| TA0009 | Collection | Coletar dados de interesse do adversario |
| TA0011 | Command and Control | Estabelecer comunicacao com sistemas comprometidos |
| TA0010 | Exfiltration | Extrair dados do ambiente alvo |
| TA0040 | Impact | Manipular, interromper ou destruir sistemas e dados |

### Elementos Complementares

- **Groups** — Conjuntos de atividades de intrusao nomeados e rastreados (APT29, Lazarus Group, FIN7).
- **Software** — Ferramentas e malware catalogados com tecnicas associadas (Cobalt Strike, Mimikatz).
- **Mitigations** — Controles de seguranca mapeados para cada tecnica que reduzem risco de exploracao.
- **Data Sources** — Fontes de dados necessarias para detectar cada tecnica (process creation, network traffic).

## Practical Application

### Uso para Detection Engineering

1. Mapear fontes de dados disponiveis no ambiente (EDR, SIEM, network sensors).
2. Identificar tecnicas relevantes ao threat landscape da organizacao usando CTI.
3. Criar regras de deteccao especificas por tecnica com data sources mapeados.
4. Priorizar cobertura de deteccao por tecnicas mais utilizadas por grupos relevantes.
5. Testar eficacia das deteccoes com emulacao de adversarios usando Atomic Red Team.
6. Documentar cobertura em heatmap da matriz ATT&CK e identificar gaps criticos.

### Uso para Threat Intelligence

- Mapear relatórios de CTI para tecnicas ATT&CK para padronizar linguagem.
- Rastrear evolucao de TTPs de grupos adversarios relevantes ao setor.
- Correlacionar indicadores de comprometimento (IoCs) com tecnicas para contextualizacao.
- Alimentar threat briefings executivos com visualizacoes baseadas na matriz ATT&CK.

### Uso para Red Team e Purple Team

- Definir planos de ataque baseados em TTPs de grupos adversarios especificos.
- Utilizar ATT&CK Navigator para planejar e documentar operacoes de emulacao.
- Comparar cobertura de deteccao antes e apos exercicios de purple team.
- Gerar relatorios de engagement mapeados para tecnicas ATT&CK para facilitar remediacao.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O detection-coverage-matrix e construido diretamente sobre a matriz ATT&CK Enterprise.
- O defense-layer utiliza data sources do ATT&CK para garantir visibilidade em tecnicas prioritarias.
- O offense-layer planeja engagements de red team baseados em TTPs de grupos adversarios relevantes.
- O purple-team-method utiliza ATT&CK como linguagem comum entre equipes ofensivas e defensivas.
- O ir-layer referencia tecnicas ATT&CK em incident reports para padronizar documentacao.
- O mitre-d3fend complementa o ATT&CK com taxonomia de contramedidas defensivas por tecnica.
- O lockheed-martin-kill-chain mapeia-se as taticas ATT&CK para fornecer visao de cadeia de ataque.
- O red-team-maturity-model avalia cobertura de tecnicas ATT&CK como indicador de capacidade ofensiva.
- Metricas de cobertura ATT&CK por tatica sao exibidas no security-kpi-dashboard.
