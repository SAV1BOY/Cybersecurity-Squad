# Bug Bounty Triage Workflow

Processo para receber, avaliar e responder a reports de um programa de bug bounty.

## Objetivo

Processar submissoes de bug bounty de forma eficiente e justa, garantindo que vulnerabilidades validas sejam corrigidas rapidamente e pesquisadores recebam reconhecimento adequado.

## Inputs

- Submissao do pesquisador via plataforma de bug bounty
- Politica do programa (escopo, severidade, recompensas)
- Historico de reports anteriores para dedup
- SLA de resposta definido no programa

## Stages

### 1. Initial Triage

- Responsavel: **omar-santos**
- Verificar se o report esta dentro do escopo do programa
- Ponto de decisao: **Report dentro do escopo?**
  - Sim -> prosseguir com analise
  - Nao -> responder ao pesquisador com justificativa e fechar
- Verificar duplicatas contra reports anteriores

### 2. Validation

- Responsavel: **georgia-weidman**
- Reproduzir a vulnerabilidade em ambiente controlado
- Ponto de decisao: **Vulnerabilidade confirmada?**
  - Sim -> classificar severidade
  - Nao -> solicitar mais informacoes ou marcar como not reproducible

### 3. Severity Assessment

- Responsavel: **georgia-weidman**
- Calcular CVSS score baseado no impacto real
- Determinar valor da recompensa conforme tabela do programa
- Verificar se afeta dados de usuarios ou sistemas criticos

### 4. Developer Notification

- Responsavel: **omar-santos**
- Criar ticket interno para o time responsavel pelo fix
- Incluir detalhes tecnicos, severidade e SLA de correcao
- Acompanhar progresso e cobrar se necessario

### 5. Fix Development

- Responsavel: **System Owner**
- Desenvolver e testar correcao para a vulnerabilidade
- Seguir processo padrao de code review e deploy
- Notificar equipe de seguranca quando fix estiver em producao

### 6. Fix Verification

- Responsavel: **georgia-weidman**
- Verificar que o fix corrige a vulnerabilidade reportada
- Testar para regressoes e bypasses
- Ponto de decisao: **Fix efetivo?**
  - Sim -> prosseguir para pagamento
  - Nao -> devolver para re-fix

### 7. Reward e Disclosure

- Responsavel: **cyber-chief**
- Processar pagamento da recompensa ao pesquisador
- Coordenar disclosure timeline com pesquisador
- Publicar advisory se aplicavel

### 8. Lessons Learned

- Responsavel: **jim-manico**
- Analisar root cause da vulnerabilidade
- Verificar se o mesmo pattern existe em outros sistemas
- Atualizar secure coding guidelines se necessario

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Report duplicado | Finding ja reportado anteriormente | Notificar pesquisador e fechar |
| Vulnerabilidade critica | CVSS >= 9.0 | Ativar processo de emergencia |
| Pesquisador agindo de ma-fe | Exfiltracao de dados ou extorsao | Envolver equipe juridica |
| Disputa de severidade | Pesquisador discorda da classificacao | Revisar com segundo analista |

## Outputs

- Report processado com decisao documentada
- Ticket de remediacao rastreado ate closure
- Pagamento processado ao pesquisador
- Metricas do programa (reports recebidos, MTTR, gastos)

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
