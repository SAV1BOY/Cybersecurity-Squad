# Operating Assumptions — Cybersecurity Squad

> Premissas operacionais sob as quais o squad opera.
> Revisadas trimestralmente pelo cyber-chief (ver docs/cadence-operations.md).

## Assumptions

| ID | Assumption | Risco se Falsa | Review Cadence | Ultima Revisao | Status |
|----|-----------|----------------|----------------|----------------|--------|
| ASM-001 | Autorizacao formal (ROE) e obtida antes de qualquer teste | Consequencias legais, violacao de compliance | Cada engagement | — | Ativa |
| ASM-002 | Ambientes de teste sao isolados de producao quando possivel | Dano a sistemas de producao | Cada engagement | — | Ativa |
| ASM-003 | Agentes operam dentro do escopo declarado em seus arquivos | Resultados fora do escopo, risco nao gerenciado | Mensal | — | Ativa |
| ASM-004 | Config.yaml e a fonte de verdade para roteamento de tasks | Roteamento incorreto, agente errado para task | Trimestral | — | Ativa |
| ASM-005 | Quality gates com threshold de 80% sao suficientes para qualidade | Outputs abaixo do padrao passando | Trimestral | — | Ativa |
| ASM-006 | Cross-squad handoffs seguem protocolo padronizado | Perda de contexto, SLA violation | Cada handoff | — | Ativa |
| ASM-007 | Registries e metrics sao atualizados apos cada task completion | Perda de memoria operacional | Semanal | — | Ativa |
| ASM-008 | OPSEC do repositorio e mantido (sem segredos, exploits ou dados reais) | Vazamento, risco legal | Cada commit | — | Ativa |

## Cross-References
- Risk register: `data/registries/risk-register.md`
- Decisions log: `data/registries/decisions-log.md`
- Cadence: `docs/cadence-operations.md` (reviewed quarterly)
