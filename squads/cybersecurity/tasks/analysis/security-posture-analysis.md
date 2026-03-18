# Task: Security Posture Analysis

## Objetivo
Analisar a postura de seguranca geral da organizacao, consolidando metricas, findings e trends para fornecer uma visao holistica do estado de seguranca.

## Agents
- **cyber-chief** (lead) — Consolida visao estrategica de postura
- **omar-santos** (support) — Contribui com metricas operacionais
- **marcus-carey** (support) — Contextualiza com cultura e maturidade

## Inputs
- Security KPIs atuais (MTTD, MTTR, vuln backlog)
- Findings registrados de todos os domains
- Detection coverage map
- Maturity assessment anterior (se disponivel)

## Steps
1. Coletar metricas de todos os domains (red, blue, appsec, cloud, IR)
2. Consolidar findings abertos por severidade e aging
3. Analisar detection coverage contra MITRE ATT&CK
4. Avaliar compliance status contra frameworks regulatorios
5. Comparar metricas atuais com baseline e targets
6. Identificar trends positivos e negativos
7. Mapear top risks e areas de maior exposicao
8. Calcular security maturity score agregado
9. Gerar relatorio de postura com recomendacoes estrategicas
10. Registrar no `security-kpis`

## Output
- Relatorio de security posture com visao holistica
- Dashboard de KPIs com trends e comparacoes
- Top risks e recomendacoes estrategicas priorizadas
- Registro no `security-kpis`

## Quality Gates
- [ ] Metricas coletadas de todos os domains de seguranca
- [ ] Findings consolidados por severidade e aging
- [ ] Detection coverage atualizado e analisado
- [ ] Trends identificados com contexto historico
- [ ] Top risks mapeados com recomendacoes acionaveis
- [ ] Checklist `compliance-audit-quality` atendido

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | security-kpi-dashboard, governance-layer |
| Checklists | compliance-audit-quality |
| Templates | reports/security-posture-report-template, reports/quarterly-security-report-template |
| Registry | data/metrics/security-kpis |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: monthly/quarterly cadence
- **Delivers to**: cyber-chief decisions
