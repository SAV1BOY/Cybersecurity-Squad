# Task: Toolchain Maintenance

## Objetivo
Manter o toolchain de seguranca do squad atualizado, funcional e seguro, garantindo que ferramentas estao em versoes estaveis e configuradas adequadamente.

## Agents
- **command-generator** (lead) — Gerencia toolchain tecnico
- **cyber-chief** (support) — Prioriza e autoriza mudancas

## Inputs
- Inventario de ferramentas do squad
- Release notes e changelogs de ferramentas
- Vulnerabilidades conhecidas em ferramentas utilizadas
- Licencas e contratos de ferramentas comerciais

## Steps
1. Inventariar todas as ferramentas do squad com versoes atuais
2. Verificar atualizacoes disponiveis para cada ferramenta
3. Avaliar changelogs para breaking changes e security fixes
4. Planejar atualizacoes com rollback strategy
5. Executar atualizacoes em ambiente de teste primeiro
6. Validar funcionalidade pos-atualizacao
7. Atualizar documentacao de ferramentas e configuracoes
8. Verificar licencas e renovacoes proximas
9. Avaliar novas ferramentas para gaps identificados
10. Registrar no `decisions-log`

## Output
- Inventario de toolchain atualizado com versoes
- Ferramentas atualizadas e validadas
- Documentacao de configuracao atualizada
- Registro de decisoes no `decisions-log`

## Quality Gates
- [ ] Todas as ferramentas inventariadas com versoes
- [ ] Security updates aplicados em ferramentas criticas
- [ ] Atualizacoes testadas antes de deploy em producao
- [ ] Documentacao de configuracao atualizada
- [ ] Licencas e renovacoes verificadas

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | governance-layer |
| Checklists | santos/santos-soc-readiness |
| Templates | reports/remediation-plan-template |
| Registry | data/registries/decisions-log |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: quarterly review
- **Delivers to**: updated toolchain docs
