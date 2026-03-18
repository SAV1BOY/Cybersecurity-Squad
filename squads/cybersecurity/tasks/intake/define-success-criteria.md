# Task: Define Success Criteria

## Objetivo
Estabelecer criterios claros e mensuraveis de sucesso para o engagement de seguranca, alinhando expectativas entre o squad e os stakeholders.

## Agents
- **cyber-chief** (lead) — Define criterios e alinha com stakeholders

## Inputs
- Documento de ROE aprovado
- Objetivos de negocio do cliente/stakeholder
- Baseline de seguranca atual (se disponivel)

## Steps
1. Reunir com stakeholders para entender objetivos de negocio
2. Traduzir objetivos de negocio em criterios tecnicos mensuraveis
3. Definir KPIs especificos para o engagement (cobertura, SLA, metricas)
4. Estabelecer thresholds de aceite (ex: zero critical sem plano de remediacao)
5. Documentar deliverables esperados e formato de entrega
6. Definir timeline com milestones intermediarios
7. Alinhar severity classification framework (CVSS, custom, risk-based)
8. Registrar criterios no `security-assessment-brief`
9. Obter sign-off dos stakeholders sobre criterios definidos
10. Registrar no `decisions-log`

## Output
- Documento de success criteria assinado
- Lista de KPIs e thresholds do engagement
- Timeline com milestones definidos
- Registro no `decisions-log`

## Quality Gates
- [ ] Criterios sao mensuraveis e objetivos (nao subjetivos)
- [ ] Stakeholders revisaram e aprovaram os criterios
- [ ] Timeline e milestones sao realistas e acordados
- [ ] Severity classification framework definido e aceito
- [ ] Deliverables e formato de entrega documentados
- [ ] Criterios alinhados com o escopo definido no ROE
- [ ] Checklist `scope-and-roe-quality` validado

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | scope-and-roe-quality |
| Templates | briefs/security-assessment-brief |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: collect-authorization-and-roe
- **Delivers to**: setup-comms-and-escalation
