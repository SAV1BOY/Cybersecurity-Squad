# Task: Findings Review

## Objetivo
Revisar todos os findings de seguranca antes da entrega, validando qualidade tecnica, classificacao de severidade, evidencias e acionabilidade das recomendacoes.

## Agents
- **cyber-chief** (lead) — Coordena revisao e valida alinhamento
- **peter-kim** (reviewer) — Valida qualidade tecnica Red Team
- **jim-manico** (reviewer) — Valida qualidade tecnica AppSec

## Inputs
- Findings registrados no `findings-registry`
- Evidencias associadas a cada finding
- Risk Scoring Model e Finding Structure Standard
- Templates de report

## Steps
1. Verificar que cada finding segue o Finding Structure Standard
2. Validar que evidencias sao reproduziveis e hasheadas (SHA-256)
3. Revisar classificacao de severidade pelo Risk Scoring Model
4. Confirmar que impacto esta descrito em termos de negocio
5. Verificar que recomendacoes sao acionaveis e especificas
6. Eliminar duplicatas e consolidar findings relacionados
7. Validar que attack paths estao documentados (nao apenas vulns)
8. Verificar que nenhum dado sensivel real aparece nos findings
9. Aprovar ou devolver findings para correcao
10. Registrar decisao de review no `findings-registry`

## Output
- Findings revisados e aprovados para entrega
- Lista de findings devolvidos para correcao com feedback
- Registro de review no `findings-registry`

## Quality Gates
- [ ] Cada finding segue o Finding Structure Standard
- [ ] Evidencias reproduziveis e hasheadas (SHA-256)
- [ ] Severidade classificada pelo Risk Scoring Model
- [ ] Impacto descrito em termos de negocio
- [ ] Recomendacoes acionaveis e especificas
- [ ] Nenhum dado sensivel real nos findings
- [ ] Checklist `security-report-quality` 100% atendido
- [ ] Checklist `evidence-chain-quality` validado
