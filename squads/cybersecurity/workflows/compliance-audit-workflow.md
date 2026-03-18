# Compliance Audit Workflow

Processo para preparar, executar e responder a auditorias de compliance de seguranca.

## Objetivo

Garantir que a organizacao esteja preparada para auditorias internas e externas, com evidencias organizadas, gaps identificados e planos de remediacao em andamento.

## Inputs

- Framework de compliance aplicavel (SOC 2, ISO 27001, PCI DSS, LGPD)
- Resultados da ultima auditoria e findings pendentes
- Inventario de controles implementados
- Calendario de auditorias planejadas

## Stages

### 1. Scope Definition

- Responsavel: **cyber-chief**
- Definir escopo da auditoria com base no framework
- Identificar sistemas, processos e equipes envolvidos
- Confirmar periodo de avaliacao e timeline

### 2. Evidence Collection

- Responsavel: **omar-santos**
- Mapear cada controle aos artefatos de evidencia necessarios
- Coletar evidencias de logs, configuracoes, politicas e procedimentos
- Organizar evidencias por controle em repositorio estruturado

### 3. Gap Assessment

- Responsavel: **cyber-chief**
- Revisar cada controle contra os requisitos do framework
- Ponto de decisao: **Controle atende ao requisito?**
  - Sim -> documentar evidencia e marcar como compliant
  - Nao -> documentar gap e iniciar plano de remediacao

### 4. Remediation Planning

- Responsavel: **cyber-chief**
- Priorizar gaps por risco e impacto na auditoria
- Atribuir owners e definir prazos de correcao
- Ponto de decisao: **Remediacao possivel antes da auditoria?**
  - Sim -> executar correcao
  - Nao -> preparar plano de acao com timeline realista

### 5. Internal Review

- Responsavel: **cyber-chief**
- Simular auditoria interna usando mesmos criterios
- Identificar fragilidades na documentacao ou evidencias
- Recomendar ajustes antes da auditoria formal

### 6. Audit Execution

- Responsavel: **cyber-chief**
- Coordenar com auditores externos durante a execucao
- Fornecer evidencias e esclarecimentos conforme solicitado
- Documentar todas as questoes levantadas pelos auditores

### 7. Finding Response

- Responsavel: **cyber-chief**
- Revisar findings do auditor e concordar ou contestar
- Desenvolver plano de acao corretiva para cada finding
- Definir owners e prazos para cada acao

### 8. Continuous Monitoring

- Responsavel: **cyber-chief**
- Implementar monitoramento continuo dos controles
- Gerar evidencias automatizadas sempre que possivel
- Preparar para proxima auditoria de forma incremental

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Gap critico encontrado | Controle ausente para requisito obrigatorio | Remediar com prioridade maxima |
| Evidencia insuficiente | Controle existe mas sem documentacao | Gerar evidencia retroativa se possivel |
| Novo requisito regulatorio | Framework atualizado com novos controles | Avaliar impacto e planejar implementacao |
| Finding contestavel | Discordancia com auditor | Preparar justificativa tecnica documentada |

## Outputs

- Relatorio de readiness pre-auditoria
- Repositorio de evidencias organizado por controle
- Plano de acao corretiva para findings
- Dashboard de compliance status por framework

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
