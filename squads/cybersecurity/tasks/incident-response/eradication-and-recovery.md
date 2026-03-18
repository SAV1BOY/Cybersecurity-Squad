# Task: Eradication & Recovery

## Objetivo
Erradicar a causa raiz do incidente e restaurar sistemas afetados a um estado operacional seguro, validando a ausencia de persistencia adversaria.

## Agents
- **omar-santos** (lead) — Coordena erradicacao e recovery
- **chris-sanders** (support) — Valida completude da erradicacao

## Inputs
- Resultados da investigacao e analise de causa raiz
- Lista de ativos comprometidos
- IOCs (Indicators of Compromise) identificados
- Backups e imagens de recovery disponiveis

## Steps
1. Identificar todos os vetores de acesso utilizados pelo adversario
2. Mapear mecanismos de persistencia instalados
3. Desenvolver plano de erradicacao por ativo afetado
4. Remover malware, backdoors e mecanismos de persistencia
5. Revogar credenciais comprometidas e forcar password reset
6. Aplicar patches e hardening para fechar vetores de acesso
7. Restaurar sistemas a partir de backups limpos (se necessario)
8. Validar ausencia de IOCs apos erradicacao
9. Monitorar sistemas restaurados intensivamente por 72h
10. Registrar acoes no `incident-registry`

## Output
- Plano de erradicacao executado com confirmacao
- Sistemas restaurados e validados
- IOCs cleared em todos os ativos afetados
- Log de monitoramento pos-recovery

## Quality Gates
- [ ] Todos os vetores de acesso identificados e fechados
- [ ] Mecanismos de persistencia removidos e validados
- [ ] Credenciais comprometidas revogadas
- [ ] Patches aplicados para fechar vetores explorados
- [ ] IOCs ausentes apos erradicacao (scan de validacao)
- [ ] Monitoramento intensivo ativo pos-recovery
- [ ] Checklist `ir-eradication-recovery` 100% atendido

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | nist-800-61-incident-response, ir-layer |
| Checklists | incident-response/ir-eradication-recovery |
| Templates | reports/postmortem-template |
| Registry | data/registries/incident-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: containment-actions
- **Delivers to**: evidence-collection
