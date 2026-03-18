# Task: Cross-Squad Sync

## Objetivo
Sincronizar atividades e handoffs entre o Cybersecurity Squad e outros squads (Dev, Infra, Compliance), garantindo que findings e requisitos fluam adequadamente.

## Agents
- **cyber-chief** (lead) — Coordena integracao cross-squad
- **marcus-carey** (support) — Facilita comunicacao e alinhamento cultural

## Inputs
- Findings pendentes de handoff para outros squads
- Requisitos de seguranca para Dev e Infra
- Status de remediacao de findings entregues
- Roadmap de outros squads

## Steps
1. Consolidar findings pendentes de handoff por squad destino
2. Priorizar findings por impacto e urgencia
3. Preparar briefing com contexto tecnico e de negocio
4. Conduzir sync meeting com cada squad parceiro
5. Alinhar timelines de remediacao com capacidade dos squads
6. Verificar status de findings anteriormente entregues
7. Identificar dependencias e bloqueios entre squads
8. Definir acoes e follow-ups com deadlines
9. Documentar acordos e compromissos
10. Registrar no `decisions-log`

## Output
- Ata de sync meetings com acordos
- Status de handoffs atualizados
- Dependencias e bloqueios mapeados
- Registro no `decisions-log`

## Quality Gates
- [ ] Todos os findings pendentes de handoff revisados
- [ ] Sync realizado com squads relevantes
- [ ] Timelines de remediacao alinhados
- [ ] Status de findings anteriores atualizado
- [ ] Dependencias e bloqueios identificados e endereçados

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | carey/carey-communication-under-pressure |
| Templates | communications/incident-notification-template |
| Registry | data/registries/decisions-log, data/handoffs/handoff-tracking |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: weekly/monthly cadence
- **Delivers to**: partner squads
