# Tabletop Exercise Workflow

Processo para planejar, conduzir e documentar exercicios de simulacao de incidentes de seguranca.

## Objetivo

Testar a capacidade de resposta da organizacao a cenarios de incidentes de seguranca em um ambiente controlado de discussao, identificando gaps em processos, comunicacao e decisao.

## Inputs

- Cenario de incidente baseado em ameacas reais ao setor
- Lista de participantes e seus papeis no exercicio
- Playbooks de resposta a incidentes atuais
- Escalation matrix e plano de comunicacao

## Stages

### 1. Exercise Design

- Responsavel: **chris-sanders + cyber-chief**
- Selecionar cenario relevante (ransomware, data breach, insider threat, supply chain)
- Desenvolver injects (eventos que avancam o cenario) com timeline
- Preparar materiais: briefing deck, injects cards, evaluation forms

### 2. Participant Selection

- Responsavel: **chris-sanders + cyber-chief**
- Identificar participantes de todas as areas relevantes (IT, security, legal, comms, management)
- Enviar convites com briefing pre-exercicio
- Ponto de decisao: **Todos os papeis criticos confirmados?**
  - Sim -> prosseguir
  - Nao -> ajustar cenario ou reagendar

### 3. Pre-Brief

- Responsavel: **chris-sanders + cyber-chief**
- Apresentar regras do exercicio e objetivos de aprendizado
- Esclarecer que e um ambiente blameless de aprendizado
- Confirmar que participantes entendem seus papeis

### 4. Exercise Execution

- Responsavel: **marcus-carey**
- Apresentar cenario inicial aos participantes
- Injetar eventos conforme timeline planejado
- Guiar discussao com perguntas provocativas
- Documentar decisoes tomadas e justificativas

### 5. Hot Wash

- Responsavel: **marcus-carey**
- Imediatamente apos o exercicio, coletar impressoes iniciais
- Perguntar aos participantes: o que funcionou, o que nao funcionou
- Identificar surpresas e pontos de confusao

### 6. Analysis

- Responsavel: **chris-sanders + cyber-chief**
- Analisar decisoes tomadas contra os playbooks existentes
- Identificar gaps em processos, comunicacao e tooling
- Classificar findings por criticidade e facilidade de correcao

### 7. After Action Report

- Responsavel: **chris-sanders + cyber-chief**
- Compilar relatorio com cenario, decisoes, findings e recomendacoes
- Incluir action items com owners e prazos
- Distribuir para todos os participantes e management

### 8. Improvement Tracking

- Responsavel: **cyber-chief**
- Rastrear implementacao dos action items
- Verificar que playbooks foram atualizados conforme necessario
- Planejar proximo exercicio para testar melhorias

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Participante ausente | Papel critico sem representante | Designar substituto ou ajustar cenario |
| Cenario muito facil | Participantes resolvem sem dificuldade | Injetar complicacoes adicionais |
| Discussao desviou | Participantes saem do escopo | Facilitador redireciona com inject |
| Gap critico revelado | Processo essencial inexistente | Priorizar como action item P1 |

## Outputs

- After action report com findings e recomendacoes
- Lista de action items com owners e prazos
- Playbooks atualizados (apos implementacao dos fixes)
- Metricas de participacao e gaps identificados

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
