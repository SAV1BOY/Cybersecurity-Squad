# Task: Maintain Checklists & Standards

## Objetivo
Manter checklists, standards e guidelines de seguranca atualizados, garantindo que refletem best practices atuais e lessons learned recentes.

## Agents
- **cyber-chief** (lead) — Coordena manutencao de checklists e standards

## Inputs
- Checklists e standards existentes
- Lessons learned de engagements recentes
- Atualizacoes de frameworks de referencia (OWASP, NIST, CIS)
- Feedback das equipes sobre aplicabilidade

## Steps
1. Inventariar todos os checklists e standards do squad
2. Verificar data de ultima revisao de cada documento
3. Identificar documentos desatualizados (review overdue)
4. Coletar feedback das equipes sobre gaps e melhorias
5. Incorporar lessons learned de engagements recentes
6. Atualizar checklists com mudancas de frameworks de referencia
7. Remover items obsoletos e adicionar novos conforme evolucao
8. Versionar documentos atualizados com changelog
9. Comunicar atualizacoes relevantes para as equipes
10. Registrar no `decisions-log`

## Output
- Checklists e standards atualizados e versionados
- Changelog de atualizacoes realizadas
- Comunicacao de mudancas relevantes
- Registro no `decisions-log`

## Quality Gates
- [ ] Todos os documentos inventariados com data de ultima revisao
- [ ] Documentos overdue priorizados para atualizacao
- [ ] Lessons learned incorporados nos documentos relevantes
- [ ] Changelog documentado para cada atualizacao
- [ ] Equipes notificadas sobre mudancas relevantes

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
- **Receives from**: improvement-backlog
- **Delivers to**: updated checklists
