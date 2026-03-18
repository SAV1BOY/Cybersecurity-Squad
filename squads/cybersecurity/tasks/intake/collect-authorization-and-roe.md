# Task: Collect Authorization & ROE

## Objetivo
Coletar e formalizar toda a documentacao de autorizacao e Rules of Engagement antes de iniciar qualquer atividade de seguranca ofensiva ou assessment.

## Agents
- **cyber-chief** (lead) — Orquestra o processo de coleta e validacao

## Inputs
- Solicitacao de engagement (cliente interno ou externo)
- Informacoes de contato dos stakeholders
- Escopo preliminar do projeto

## Steps
1. Identificar todos os stakeholders e decision-makers do engagement
2. Definir o tipo de assessment (pentest, red team, review, audit)
3. Redigir o documento de ROE com base no template `briefs/pentest-roe-template`
4. Especificar boundaries: IPs, dominios, aplicacoes in-scope e out-of-scope
5. Definir testing windows e restricoes de horario
6. Documentar stop-work conditions e emergency contacts
7. Obter assinatura formal de written authorization
8. Registrar NDA e clausulas de liability
9. Armazenar documentos no repositorio seguro com versionamento
10. Registrar decisao no `decisions-log`

## Output
- Documento de ROE assinado e versionado
- Written authorization formal
- NDA executado
- Registro no `decisions-log` com metadata do engagement

## Quality Gates
- [ ] Written authorization assinada por todas as partes autorizadas
- [ ] Scope boundaries claramente definidos (in-scope e out-of-scope)
- [ ] Testing windows e restricoes documentadas
- [ ] Emergency contacts e escalation path definidos
- [ ] Stop-work conditions explicitas
- [ ] NDA executado antes de qualquer compartilhamento de informacao
- [ ] Documento versionado e armazenado em repositorio seguro
- [ ] Checklist `scope-and-roe-quality` 100% atendido

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | ptes-penetration-testing |
| Checklists | scope-and-roe-quality |
| Templates | briefs/pentest-roe-template, briefs/security-assessment-brief |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: external request
- **Delivers to**: define-success-criteria
