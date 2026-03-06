# Purple Team Method — Continuous Red+Blue Collaboration

## Overview

O Purple Team Method e uma abordagem colaborativa que integra as capacidades ofensivas (Red Team) e defensivas (Blue Team) em um ciclo continuo de teste e melhoria. Diferente de red team engagements tradicionais onde resultados sao entregues no final, o purple teaming cria um loop de feedback em tempo real onde ataques sao executados, deteccoes sao validadas e gaps sao corrigidos de forma iterativa. O objetivo nao e vencer o outro time, mas elevar continuamente a postura de seguranca da organizacao.

## Core Concepts

### Fundamentos

#### Red Team

Equipe ofensiva que simula adversarios reais utilizando TTPs documentadas:

- Emula comportamento de threat actors relevantes ao setor da organizacao.
- Executa tecnicas de forma controlada e documentada com evidencias.
- Fornece perspectiva ofensiva sobre fraquezas em controles de deteccao.
- Utiliza frameworks como MITRE ATT&CK para padronizar tecnicas executadas.

#### Blue Team

Equipe defensiva responsavel por detectar, analisar e responder a ameacas:

- Opera ferramentas de seguranca (SIEM, EDR, NDR, SOAR) para deteccao e resposta.
- Cria e mantém regras de deteccao e playbooks de resposta.
- Analisa alertas e realiza triagem de eventos de seguranca.
- Conduz investigacoes forenses e resposta a incidentes.

#### Purple Team

Funcao integradora que facilita a colaboracao entre Red e Blue:

- Coordena sessoes de teste com objetivos claros e metricas definidas.
- Documenta resultados de cada tecnica testada incluindo deteccao e visibilidade.
- Facilita transferencia de conhecimento entre equipes ofensivas e defensivas.
- Prioriza melhorias de deteccao baseado em gaps identificados durante exercicios.

### Ciclo Purple Team

O ciclo e composto por cinco fases iterativas:

1. **Plan** — Selecionar tecnicas ATT&CK a serem testadas baseado em threat intelligence e gaps de cobertura.
2. **Execute** — Red team executa a tecnica de forma controlada no ambiente de producao ou lab.
3. **Detect** — Blue team verifica se a tecnica foi detectada por controles existentes e em que tempo.
4. **Measure** — Documentar resultado (detected/not detected), data sources utilizados e tempo de deteccao.
5. **Improve** — Criar ou ajustar regras de deteccao para tecnicas nao detectadas e retestar.

### Categorias de Resultado

| Resultado | Descricao | Acao |
|-----------|-----------|------|
| Detected and Alerted | Tecnica gerou alerta acionavel no SIEM/EDR | Documentar e validar playbook |
| Logged but Not Alerted | Dados existem nos logs mas nenhuma regra detectou | Criar regra de deteccao |
| Not Logged | Nenhum dado da tecnica foi capturado | Habilitar data source necessario |
| Blocked | Controle preventivo impediu a execucao da tecnica | Documentar e testar bypass |

## Practical Application

### Planejamento de Exercicio Purple Team

1. Selecionar threat actor relevante usando threat intelligence do setor.
2. Mapear TTPs do threat actor selecionado na matriz ATT&CK.
3. Priorizar tecnicas baseado em probabilidade de uso e impacto potencial.
4. Definir escopo do exercicio (tecnicas, sistemas, duracao e restricoes).
5. Preparar infraestrutura de teste e ferramentas necessarias.
6. Comunicar janela de exercicio para equipes operacionais relevantes.

### Estrutura de Uma Sessao

- **Duracao**: 2-4 horas por sessao focada.
- **Tecnicas por sessao**: 3-5 tecnicas ATT&CK.
- **Participantes**: Red team operator, Blue team analyst, Purple team coordinator.
- **Documentacao**: Resultados registrados em tempo real por tecnica testada.

### Template de Documentacao por Tecnica

```
Tecnica ATT&CK: [ID e Nome]
Data Source Requerido: [ex: Process Creation, Network Flow]
Ferramenta Utilizada: [ex: Atomic Red Team, manual]
Resultado: [Detected/Logged/Not Logged/Blocked]
Alerta Gerado: [Nome da regra ou N/A]
Tempo de Deteccao: [em minutos]
Gap Identificado: [descricao do gap se aplicavel]
Acao de Melhoria: [nova regra, novo data source, tuning]
Responsavel: [analista ou engenheiro]
Prazo: [data para implementacao]
```

### Cadencia Recomendada

- **Sessoes Purple Team**: Quinzenal ou mensal, 3-5 tecnicas por sessao.
- **Reteste de Melhorias**: 2 semanas apos implementacao de nova deteccao.
- **Review de Cobertura**: Trimestral, avaliando evolucao do heatmap ATT&CK.
- **Report Executivo**: Trimestral, com metricas de cobertura e melhoria.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O offense-layer fornece operadores Red Team para executar tecnicas durante sessoes.
- O defense-layer fornece analistas Blue Team e e responsavel por implementar melhorias de deteccao.
- O detection-coverage-matrix e atualizado apos cada sessao com resultados de cobertura por tecnica.
- O mitre-att-ck fornece a taxonomia padronizada utilizada para planejar e documentar sessoes.
- O mitre-d3fend mapeia contramedidas defensivas relevantes para cada tecnica testada.
- O lockheed-martin-kill-chain fornece visao sequencial para garantir cobertura em todas as fases.
- O ir-layer valida playbooks de resposta durante exercicios com cenarios de deteccao real.
- O red-team-maturity-model avalia a sofisticacao das simulacoes executadas pelo Red Team.
- O security-kpi-dashboard exibe metricas de cobertura ATT&CK e taxa de deteccao por sessao.
- Melhorias implementadas sao rastreadas no backlog do squad com referencia a tecnica ATT&CK.
