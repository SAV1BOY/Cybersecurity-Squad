# Incident Response Workflow

Processo de resposta a incidentes de seguranca desde a deteccao ate o encerramento e lessons learned.

## Objetivo

Coordenar a resposta a incidentes de seguranca de forma rapida, organizada e documentada, minimizando impacto e garantindo preservacao de evidencias.

## Inputs

- Alerta do SIEM, SOC ou reporte manual
- Playbooks de resposta por tipo de incidente
- Lista de contatos de emergencia e escalation matrix
- Inventario de assets e criticidade

## Stages

### 1. Detection e Triage

- Responsavel: **omar-santos**
- Receber e registrar o alerta no sistema de tracking
- Realizar triage inicial: validar se e um true positive
- Ponto de decisao: **Incidente confirmado?**
  - Sim -> classificar severidade e escalar
  - Nao -> documentar como false positive e fechar

### 2. Classification e Escalation

- Responsavel: **omar-santos**
- Classificar o incidente por tipo (malware, phishing, data breach, unauthorized access)
- Atribuir severidade (P1-P4) com base em impacto e urgencia
- Escalar conforme a escalation matrix

### 3. Containment

- Responsavel: **chris-sanders + cyber-chief**
- Executar acoes de containment imediato (isolamento de host, bloqueio de conta)
- Ponto de decisao: **Containment efetivo?**
  - Sim -> prosseguir para investigacao
  - Nao -> escalar para containment mais agressivo
- Preservar evidencias antes de qualquer acao destrutiva

### 4. Investigation

- Responsavel: **chris-sanders**
- Coletar e preservar evidencias digitais com chain of custody
- Analisar logs, memoria, disco e trafego de rede
- Determinar root cause, timeline e scope do comprometimento

### 5. Eradication

- Responsavel: **chris-sanders + cyber-chief**
- Remover presenca do adversario (malware, backdoors, contas comprometidas)
- Aplicar patches ou configuracoes necessarias
- Validar que o ambiente esta limpo

### 6. Recovery

- Responsavel: **System Owner** (com suporte do **chris-sanders + cyber-chief**)
- Restaurar sistemas ao estado operacional normal
- Monitorar de perto para sinais de re-comprometimento
- Validar integridade dos dados restaurados

### 7. Post-Incident Review

- Responsavel: **chris-sanders + cyber-chief**
- Conduzir blameless postmortem com todos os envolvidos
- Documentar lessons learned e action items
- Atualizar playbooks e detection rules conforme necessario

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Incidente P1 | Impacto critico em producao | Ativar war room e notificar C-level |
| Dados pessoais expostos | Indicios de data breach | Acionar equipe juridica e DPO |
| Adversario ativo | Atacante ainda presente | Priorizar containment sobre investigacao |
| Evidencia juridica | Possivel acao legal | Preservar chain of custody rigorosa |

## Outputs

- Incident report completo com timeline
- Root cause analysis documentado
- Action items de melhoria com owners e prazos
- Metricas de resposta (MTTD, MTTR, MTTC)

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
