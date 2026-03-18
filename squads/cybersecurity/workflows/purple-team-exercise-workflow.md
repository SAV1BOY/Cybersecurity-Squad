# Purple Team Exercise Workflow

Processo colaborativo entre red team e blue team para testar e melhorar capacidades de deteccao e resposta.

## Objetivo

Validar a eficacia dos controles de deteccao e resposta atraves de exercicios colaborativos onde atacantes e defensores trabalham juntos para melhorar a postura de seguranca.

## Inputs

- ATT&CK techniques selecionadas para o exercicio
- Detection rules e playbooks atuais do blue team
- Ferramentas e payloads do red team
- Ambiente de teste ou producao aprovado

## Stages

### 1. Exercise Planning

- Responsavel: **peter-kim + chris-sanders**
- Selecionar scenarios e tecnicas ATT&CK a serem testadas
- Definir regras do exercicio e limites de escopo
- Alinhar objetivos entre red team e blue team
- Agendar janela de execucao com stakeholders

### 2. Pre-Exercise Briefing

- Responsavel: **peter-kim + chris-sanders**
- Apresentar o plano de exercicio para ambas as equipes
- Confirmar que blue team entende os objetivos de aprendizado
- Verificar que tooling de red team esta preparado
- Estabelecer canais de comunicacao durante o exercicio

### 3. Technique Execution

- Responsavel: **rogue**
- Executar a tecnica ATT&CK conforme planejado
- Documentar exatamente o que foi feito com timestamps
- Ponto de decisao: **Execucao bem sucedida?**
  - Sim -> notificar blue team para iniciar deteccao
  - Nao -> ajustar abordagem ou documentar bloqueio por controle preventivo

### 4. Detection Assessment

- Responsavel: **chris-sanders**
- Verificar se alertas foram gerados pela atividade
- Avaliar qualidade e tempo de deteccao
- Ponto de decisao: **Tecnica detectada?**
  - Sim -> avaliar qualidade do alerta e tempo de resposta
  - Nao -> documentar gap de deteccao

### 5. Response Assessment

- Responsavel: **chris-sanders**
- Executar o playbook de resposta correspondente
- Avaliar se as acoes de containment sao eficazes
- Medir tempo total de resposta (MTTD + MTTR)

### 6. Joint Analysis

- Responsavel: **peter-kim + chris-sanders**
- Red team explica detalhes tecnicos da execucao
- Blue team compartilha o que viu (ou nao viu)
- Identificar melhorias em detection rules, logs e playbooks

### 7. Improvement Implementation

- Responsavel: **chris-sanders**
- Criar ou ajustar detection rules para gaps encontrados
- Atualizar playbooks de resposta com novos procedimentos
- Re-testar para validar melhorias

### 8. Report e Closeout

- Responsavel: **peter-kim + chris-sanders**
- Compilar resultados por tecnica testada
- Gerar scorecard de deteccao e resposta
- Documentar action items e owners

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Tecnica causa impacto real | Sistema de producao afetado | Pausar exercicio e remediar |
| Gap critico encontrado | Tecnica de alto risco nao detectada | Priorizar fix como P1 |
| Controle preventivo bloqueou | Red team impedido de executar | Documentar controle eficaz |
| Multiplos gaps na mesma tactic | Falha sistematica em uma tactic | Planejar sprint dedicado |

## Outputs

- Scorecard de deteccao por tecnica ATT&CK
- Lista de gaps com prioridade e owners
- Detection rules novas ou atualizadas
- Playbooks de resposta revisados
- Relatorio executivo do exercicio

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
