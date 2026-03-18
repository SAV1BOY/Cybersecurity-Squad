# Task: Triage & Severity

## Objetivo
Realizar triagem inicial de alertas e incidentes de seguranca, classificando severidade e determinando se requer ativacao completa do processo de incident response.

## Agents
- **chris-sanders** (lead) — Executa triagem tecnica
- **omar-santos** (support) — Valida contexto de infraestrutura
- **cyber-chief** (support) — Decide sobre ativacao de IR

## Inputs
- Alerta ou notificacao de incidente
- Logs e telemetria relacionados ao evento
- Playbooks de triage existentes
- Contexto de ativos afetados (asset registry)

## Steps
1. Receber e registrar alerta/notificacao de incidente
2. Coletar informacoes iniciais (timestamp, source, affected assets)
3. Correlacionar alerta com outros eventos no SIEM
4. Determinar se o evento e verdadeiro positivo ou falso positivo
5. Classificar severidade usando framework definido (P1-P4)
6. Avaliar blast radius e ativos potencialmente afetados
7. Decidir se ativa processo completo de incident response
8. Notificar stakeholders conforme escalation matrix
9. Documentar decisao de triage com justificativa
10. Registrar no `incident-registry`

## Output
- Registro de incidente com classificacao de severidade
- Decisao de ativacao de IR documentada
- Notificacoes enviadas conforme escalation matrix
- Registro no `incident-registry`

## Quality Gates
- [ ] Alerta registrado com timestamp e source
- [ ] Correlacao com outros eventos realizada
- [ ] Severidade classificada com justificativa
- [ ] Blast radius avaliado e documentado
- [ ] Decisao de ativacao documentada
- [ ] Stakeholders notificados conforme escalation matrix
- [ ] Checklist `incident-triage-quality` atendido
- [ ] Checklist `ir-triage-and-severity` validado

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | nist-800-61-incident-response, ir-layer |
| Checklists | incident-triage-quality, incident-response/ir-triage-and-severity |
| Templates | briefs/incident-intake-template |
| Registry | data/registries/incident-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: alert/detection trigger
- **Delivers to**: containment-actions
