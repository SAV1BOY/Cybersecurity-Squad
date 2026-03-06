# Task: Incident Communication

## Objetivo
Gerenciar comunicacao interna e externa durante e apos o incidente, garantindo transparencia, compliance regulatorio e preservacao da reputacao.

## Agents
- **marcus-carey** (lead) — Gerencia comunicacao de incidente
- **cyber-chief** (support) — Alinha com governanca e compliance

## Inputs
- Status do incidente e severidade classificada
- Escalation matrix e lista de stakeholders
- Requisitos regulatorios de notificacao (LGPD, GDPR)
- Templates de comunicacao de incidente

## Steps
1. Determinar audiencias de comunicacao (interna, reguladores, afetados)
2. Avaliar obrigacoes regulatorias de notificacao e prazos
3. Redigir comunicacao interna com status e acoes em andamento
4. Preparar comunicacao para reguladores (se aplicavel)
5. Redigir notificacao para partes afetadas (se dados expostos)
6. Revisar comunicacao com legal antes de envio externo
7. Estabelecer cadencia de updates durante o incidente
8. Coordenar com PR/marketing para comunicacao publica (se necessario)
9. Documentar todas as comunicacoes enviadas com timestamps
10. Registrar no `incident-registry`

## Output
- Comunicacoes internas enviadas e documentadas
- Notificacoes regulatorias (se aplicavel) com confirmacao
- Notificacoes a partes afetadas (se aplicavel)
- Log de comunicacoes com timestamps

## Quality Gates
- [ ] Obrigacoes regulatorias de notificacao avaliadas
- [ ] Prazos regulatorios respeitados
- [ ] Comunicacoes revisadas por legal antes de envio externo
- [ ] Cadencia de updates mantida durante o incidente
- [ ] Todas as comunicacoes documentadas com timestamps
- [ ] Checklist `ir-communication-escalation` atendido
- [ ] Checklist `carey-communication-under-pressure` validado
