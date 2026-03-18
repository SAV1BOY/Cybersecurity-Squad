# Task: Policy Review

## Objetivo
Revisar politicas de seguranca da organizacao, garantindo alinhamento com best practices, compliance regulatorio e aplicabilidade pratica.

## Agents
- **cyber-chief** (lead) — Revisa alinhamento estrategico de politicas
- **marcus-carey** (reviewer) — Valida aplicabilidade cultural e pratica

## Inputs
- Politicas de seguranca existentes
- Requisitos regulatorios aplicaveis
- Frameworks de referencia (NIST CSF, ISO 27001, CIS)
- Feedback de equipes sobre aplicabilidade

## Steps
1. Inventariar politicas de seguranca existentes e versoes
2. Verificar alinhamento com requisitos regulatorios (LGPD, PCI, SOC2)
3. Mapear politicas contra frameworks de referencia
4. Identificar gaps entre politicas e praticas reais
5. Avaliar clareza e aplicabilidade pratica de cada politica
6. Verificar que politicas estao atualizadas (review date)
7. Identificar politicas conflitantes ou redundantes
8. Documentar recomendacoes de atualizacao com prioridade
9. Aprovar ou recomendar atualizacoes
10. Registrar decisoes no `decisions-log`

## Output
- Relatorio de review de politicas com gaps e recomendacoes
- Lista de politicas para atualizacao priorizadas
- Registro de decisoes no `decisions-log`

## Quality Gates
- [ ] Todas as politicas inventariadas e versionadas
- [ ] Alinhamento regulatorio verificado
- [ ] Gaps entre politica e pratica identificados
- [ ] Politicas desatualizadas sinalizadas
- [ ] Recomendacoes de atualizacao priorizadas
- [ ] Checklist `compliance-audit-quality` atendido

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | compliance-audit-quality |
| Templates | reports/security-posture-report-template |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: quarterly cadence / new policy request
- **Delivers to**: stakeholder approval
