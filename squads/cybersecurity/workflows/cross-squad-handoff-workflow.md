# Cross-Squad Handoff Workflow

Processo para transferir trabalho, findings ou responsabilidades entre squads de forma estruturada.

## Objetivo

Garantir que informacoes criticas nao se percam durante transicoes entre equipes, mantendo contexto, rastreabilidade e continuidade de responsabilidade.

## Inputs

- Artefato ou finding a ser transferido
- Identificacao do squad de destino
- Contexto completo do trabalho realizado
- SLA ou urgencia da transferencia

## Stages

### 1. Handoff Preparation

- Responsavel: **cyber-chief** (squad de origem)
- Compilar toda documentacao relevante do trabalho realizado
- Estruturar handoff package com contexto, findings e next steps
- Identificar o ponto de contato no squad de destino

### 2. Context Documentation

- Responsavel: **cartographer**
- Documentar o que foi feito, por que e o que falta fazer
- Incluir decisoes tomadas e justificativas
- Listar dependencias e riscos conhecidos
- Anexar evidencias e artefatos relevantes

### 3. Handoff Meeting

- Responsavel: **cyber-chief**
- Agendar sessao de handoff com ambos os squads
- Apresentar o handoff package ao squad de destino
- Ponto de decisao: **Squad de destino aceita o handoff?**
  - Sim -> formalizar transferencia de responsabilidade
  - Nao -> resolver objecoes e re-apresentar

### 4. Acceptance e Assignment

- Responsavel: **cyber-chief** (squad de destino)
- Revisar completude do handoff package
- Atribuir owner no squad de destino
- Confirmar entendimento do escopo e expectativas

### 5. Transition Period

- Responsavel: **cartographer** e **cartographer**
- Manter canal de comunicacao aberto por periodo definido
- Originating agent disponivel para esclarecer duvidas
- Ponto de decisao: **Receiving agent autonomo?**
  - Sim -> encerrar periodo de transicao
  - Nao -> estender suporte

### 6. Confirmation e Closeout

- Responsavel: **cyber-chief**
- Confirmar que o squad de destino assumiu a responsabilidade
- Atualizar tracking systems com novo owner
- Registrar handoff no log de transferencias

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Handoff rejeitado | Squad destino nao tem capacidade | Escalar para management para resolver |
| Informacao incompleta | Package sem contexto suficiente | Devolver para complementacao |
| Urgencia alta | Finding critico precisa de acao imediata | Fazer handoff emergencial com briefing verbal |
| Responsabilidade compartilhada | Trabalho requer ambos os squads | Definir RACI claro e manter colaboracao |

## Outputs

- Handoff package documentado e aceito
- Tracking atualizado com novos owners
- Log de transferencia registrado
- Confirmacao formal de aceitacao pelo squad destino

## Handoff Package Template

O handoff package deve conter no minimo:
- Resumo executivo do contexto
- Lista de findings ou items transferidos
- Trabalho ja realizado e pendente
- Decisoes tomadas e justificativas
- Contatos para esclarecimentos
- Prazo ou SLA associado

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
