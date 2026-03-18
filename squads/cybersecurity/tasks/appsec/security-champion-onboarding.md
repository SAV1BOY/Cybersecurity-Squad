# Task: Security Champion Onboarding

## Objetivo
Integrar e capacitar Security Champions dentro das equipes de desenvolvimento, criando uma rede descentralizada de defensores de seguranca no SDLC.

## Agents
- **jim-manico** (lead) — Define programa e conteudo tecnico
- **marcus-carey** (support) — Aborda cultura de seguranca e engajamento

## Inputs
- Lista de equipes de desenvolvimento sem Security Champion
- Programa de Security Champion existente (se houver)
- Materiais de treinamento de seguranca disponiveis
- Metricas atuais de security champion coverage

## Steps
1. Identificar equipes sem Security Champion e priorizar
2. Definir perfil e responsabilidades do Security Champion
3. Selecionar candidatos com interesse e aptidao em seguranca
4. Desenvolver programa de onboarding com trilha de conhecimento
5. Criar materiais de referencia rapida (cheat sheets, playbooks)
6. Estabelecer canal de comunicacao entre Champions e security squad
7. Definir metricas de sucesso do programa (cobertura, engajamento)
8. Conduzir sessao inaugural de onboarding com novos Champions
9. Estabelecer cadencia de syncs recorrentes com Champions
10. Registrar decisoes no `decisions-log`

## Output
- Programa de Security Champion documentado
- Lista de Security Champions ativos por equipe
- Materiais de onboarding e referencia rapida
- Metricas de cobertura de Security Champions

## Quality Gates
- [ ] Perfil e responsabilidades do Champion claramente definidos
- [ ] Trilha de conhecimento estruturada e progressiva
- [ ] Materiais de referencia rapida criados e acessiveis
- [ ] Canal de comunicacao com security squad estabelecido
- [ ] Metricas de sucesso definidas e rastreadas
- [ ] Checklist `carey-security-culture-audit` validado

## Routing & Escalation
- **frameworks**: security-champion-program
- **checklists**: carey/carey-security-culture-audit
- **templates**: reports/security-posture-report-template
- **registry**: data/registries/decisions-log
- **receives_from**: cyber-chief/marcus-carey initiative
- **delivers_to**: dev squad
