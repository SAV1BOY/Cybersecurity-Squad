# Task: Report Executive Review

## Objetivo
Revisar o executive summary e relatorios de alto nivel, garantindo que a comunicacao com C-level e stakeholders nao-tecnicos seja clara, precisa e acionavel.

## Agents
- **cyber-chief** (lead) — Revisa alinhamento estrategico
- **marcus-carey** (reviewer) — Valida clareza de comunicacao

## Inputs
- Executive summary draft
- Relatorio tecnico completo para referencia
- Metricas e KPIs do engagement
- Templates de executive summary

## Steps
1. Verificar que executive summary tem no maximo 1-2 paginas
2. Validar que linguagem e acessivel para audiencia nao-tecnica
3. Confirmar que risk posture geral esta claramente comunicado
4. Verificar que top findings estao destacados com impacto de negocio
5. Validar que recomendacoes estrategicas sao acionaveis
6. Confirmar que metricas-chave estao presentes e contextualizadas
7. Verificar consistencia entre executive summary e relatorio tecnico
8. Revisar tom e linguagem (informativo, nao alarmista)
9. Aprovar ou devolver para ajustes
10. Registrar decisao no `decisions-log`

## Output
- Executive summary revisado e aprovado
- Feedback para ajustes (se necessario)
- Registro de aprovacao no `decisions-log`

## Quality Gates
- [ ] Executive summary em 1-2 paginas maximo
- [ ] Linguagem acessivel para nao-tecnicos
- [ ] Top findings com impacto de negocio destacados
- [ ] Recomendacoes estrategicas acionaveis
- [ ] Metricas-chave presentes e contextualizadas
- [ ] Consistencia com relatorio tecnico validada
- [ ] Checklist `security-report-quality` atendido

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | security-report-quality |
| Templates | reports/executive-summary-template |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: findings-review
- **Delivers to**: stakeholder delivery
