# Secure SDLC Workflow

Integracao de praticas de seguranca em cada fase do ciclo de desenvolvimento de software.

## Objetivo

Garantir que seguranca seja incorporada desde o design ate o deploy, reduzindo vulnerabilidades em producao e o custo de remediacao tardia.

## Inputs

- Requisitos funcionais do projeto
- Politica de seguranca de desenvolvimento
- Ferramentas de SAST, DAST e SCA configuradas
- Checklists de seguranca por fase

## Stages

### 1. Requirements e Design

- Responsavel: **jim-manico**
- Participar da definicao de requisitos para incluir security requirements
- Conduzir threat modeling do design proposto
- Definir security acceptance criteria para cada feature

### 2. Secure Coding

- Responsavel: **Developer** (com suporte do **jim-manico**)
- Seguir secure coding guidelines da organizacao
- Utilizar bibliotecas e frameworks aprovados
- Evitar patterns inseguros documentados no swipe file

### 3. Static Analysis (SAST)

- Responsavel: **jim-manico**
- Executar SAST no pipeline de CI automaticamente
- Ponto de decisao: **Findings criticos identificados?**
  - Sim -> bloquear merge e notificar developer
  - Nao -> prosseguir para proxima fase

### 4. Software Composition Analysis (SCA)

- Responsavel: **jim-manico**
- Verificar dependencias contra bancos de vulnerabilidades conhecidas
- Identificar licencas incompativeis
- Ponto de decisao: **Dependencia vulneravel?**
  - Sim -> exigir atualizacao ou aprovacao de excecao
  - Nao -> prosseguir

### 5. Code Review

- Responsavel: **jim-manico**
- Revisar mudancas com foco em seguranca
- Validar que findings de SAST e SCA foram tratados
- Aprovar ou solicitar correcoes

### 6. Dynamic Analysis (DAST)

- Responsavel: **jim-manico**
- Executar DAST em ambiente de staging
- Testar para OWASP Top 10 e vulnerabilidades especificas do contexto
- Documentar findings e encaminhar para correcao

### 7. Pre-Production Security Review

- Responsavel: **jim-manico**
- Revisar configuracoes de deploy (secrets management, TLS, headers)
- Validar que todos os findings foram tratados ou aceitos
- Ponto de decisao: **Aprovado para producao?**
  - Sim -> autorizar deploy
  - Nao -> bloquear ate resolucao

### 8. Production Monitoring

- Responsavel: **chris-sanders**
- Configurar alertas de seguranca para a nova aplicacao
- Monitorar primeiros dias em producao para anomalias
- Integrar com vulnerability management para scans continuos

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| SAST bloqueante | Finding de severidade critica | Bloquear pipeline ate correcao |
| Dependencia com CVE critico | SCA encontra vulnerabilidade explorada | Exigir atualizacao imediata |
| Threat model incompleto | Design mudou significativamente | Refazer threat model antes de prosseguir |
| Deploy de emergencia | Hotfix critico em producao | Seguir fast-track com revisao pos-deploy |

## Outputs

- Relatorio de seguranca por release
- Metricas de findings por fase do SDLC
- Threat models atualizados
- Security acceptance criteria validados

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
