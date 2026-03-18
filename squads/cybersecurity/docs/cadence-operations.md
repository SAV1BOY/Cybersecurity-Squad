# Cadence Operations — Cybersecurity Squad

> Calendario operacional do Cybersecurity Squad com atividades diarias, semanais, mensais, trimestrais e anuais.
> Define responsaveis, participantes, outputs esperados e registries atualizados em cada cadencia.

## 1. Visao Geral

O squad opera com cadencias regulares para garantir que atividades recorrentes nao sejam negligenciadas. Cada cadencia tem owner definido, participantes obrigatorios e registries que devem ser atualizados. A configuracao de referencia esta em [`config.yaml`](../config.yaml) secao `cadence`.

---

## 2. Cadencia Diaria

Atividades executadas **todo dia util** para manter visibilidade operacional em tempo real.

| Atividade | Owner | Participantes | Descricao | Registry Atualizado |
|-----------|-------|---------------|-----------|---------------------|
| Alert triage and severity classification | [`chris-sanders`](../agents/chris-sanders.md) | Blue Team | Triagem de todos os alertas recebidos nas ultimas 24h. Classificacao por severidade usando [`incident-triage-quality`](../checklists/incident-triage-quality.md). Falsos positivos descartados com justificativa. | [`incident-registry`](../data/registries/incident-registry.md) |
| Active incident status check | [`omar-santos`](../agents/omar-santos.md) | IR Team | Atualizacao de status de todos os incidentes ativos. Verificacao de containment effectiveness. Escalacao se SLA estiver em risco. | [`incident-registry`](../data/registries/incident-registry.md) |

**Criterio de saida**: todos os alertas triados, todos os incidentes ativos com status atualizado.

---

## 3. Cadencia Semanal

Atividades executadas **uma vez por semana** para revisao tatica e ajuste de prioridades.

| Atividade | Owner | Participantes | Descricao | Registry Atualizado |
|-----------|-------|---------------|-----------|---------------------|
| Vulnerability backlog review | [`cyber-chief`](../agents/cyber-chief.md) | [`peter-kim`](../agents/peter-kim.md) | Revisao do backlog de vulnerabilidades. Priorizacao por risk score. Verificacao de SLA compliance. Vulns criticas sem owner recebem atribuicao. | [`findings-registry`](../data/registries/findings-registry.md) |
| Detection effectiveness review | [`chris-sanders`](../agents/chris-sanders.md) | [`shannon-runner`](../agents/shannon-runner.md) | Analise de efetividade das detection rules da semana. False positive rate, detection gaps identificados. Novos rules propostos para gaps. | [`detection-rules-registry`](../data/registries/detection-rules-registry.md) |
| Cross-squad request queue review | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md) | Revisao de todas as solicitacoes pendentes de/para outros squads. Handoffs atrasados sao escalados. Novas solicitacoes recebem context packet e deadline. | [`decisions-log`](../data/registries/decisions-log.md) |

**Criterio de saida**: backlog priorizado, detection gaps documentados, queue cross-squad zerada ou com SLA definido.

---

## 4. Cadencia Mensal

Atividades executadas **uma vez por mes** para analise de tendencias e ajuste de estrategia tatica.

| Atividade | Owner | Participantes | Descricao | Registry Atualizado |
|-----------|-------|---------------|-----------|---------------------|
| Security metrics dashboard review | [`cyber-chief`](../agents/cyber-chief.md) | Domain leads | Revisao dos KPIs definidos em `config.yaml > kpis`: MTTD, MTTR, vuln SLA compliance, detection coverage, false positive rate. Tendencias identificadas e action items criados. | [`data/metrics/`](../data/metrics/) |
| Maturity score update | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md) | Atualizacao do score de maturidade do squad usando [`red-team-maturity-model`](../frameworks/red-team-maturity-model.md) e [`security-kpi-dashboard`](../frameworks/security-kpi-dashboard.md). Comparacao com mes anterior. | [`data/scorecards/`](../data/scorecards/) |
| Improvement backlog grooming | [`cyber-chief`](../agents/cyber-chief.md) | Domain leads | Revisao de todos os itens de melhoria acumulados (de rework loops, postmortems, detection gaps). Priorizacao e atribuicao de owners. Itens obsoletos arquivados. | [`data/metrics/`](../data/metrics/) |

**Criterio de saida**: dashboard atualizado, maturity score publicado, improvement backlog limpo e priorizado.

---

## 5. Cadencia Trimestral

Atividades executadas **a cada 3 meses** para validacao estrategica e exercicios praticos.

| Atividade | Owner | Participantes | Descricao | Registry Atualizado |
|-----------|-------|---------------|-----------|---------------------|
| Tabletop exercise | [`marcus-carey`](../agents/marcus-carey.md) | [`cyber-chief`](../agents/cyber-chief.md), all domain leads | Exercicio de simulacao de incidente usando [`tabletop-exercise-quality`](../checklists/tabletop-exercise-quality.md). Cenario baseado em ameacas recentes do threat landscape. Gaps de processo documentados. | [`data/registries/lessons-learned-registry`](../data/registries/lessons-learned-registry.md) |
| Risk register full review | [`cyber-chief`](../agents/cyber-chief.md) | All domain leads | Revisao completa do [`risk-register`](../data/registries/risk-register.md). Riscos obsoletos fechados. Novos riscos do trimestre adicionados. Risk scores recalculados com dados atuais. | [`data/registries/risk-register`](../data/registries/risk-register.md) |
| Cross-squad integration health check | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md) | Avaliacao da saude das integracoes com dev, infra e compliance squads. SLA compliance, handoff quality, feedback loop effectiveness. Acoes corretivas para integracoes degradadas. | [`data/registries/decisions-log`](../data/registries/decisions-log.md) |
| KPI target recalibration | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md), domain leads | Revisao dos targets de KPI para o proximo trimestre. Targets ajustados com base no desempenho real e mudancas no threat landscape. Novos KPIs propostos se necessario. | [`data/registries/decisions-log`](../data/registries/decisions-log.md) |

**Criterio de saida**: tabletop executado com lessons learned, risk register atualizado, integracoes avaliadas, KPI targets recalibrados.

---

## 6. Cadencia Anual

Atividades executadas **uma vez por ano** para revisao estrategica e avaliacao de maturidade completa.

| Atividade | Owner | Participantes | Descricao | Registry Atualizado |
|-----------|-------|---------------|-----------|---------------------|
| Security program strategy review | [`cyber-chief`](../agents/cyber-chief.md) | All domain leads, [`marcus-carey`](../agents/marcus-carey.md) | Revisao da estrategia de seguranca do squad para o proximo ano. Alinhamento com objetivos organizacionais. Novos capabilities planejados. Budget e headcount revisados. | [`data/scorecards/`](../data/scorecards/) |
| Red team maturity assessment | [`cyber-chief`](../agents/cyber-chief.md) | [`peter-kim`](../agents/peter-kim.md), [`georgia-weidman`](../agents/georgia-weidman.md) | Avaliacao completa de maturidade do red team usando [`red-team-maturity-model`](../frameworks/red-team-maturity-model.md). Benchmark contra o ano anterior. Roadmap de evolucao atualizado. | [`data/scorecards/`](../data/scorecards/) |
| Full compliance audit cycle | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md), all domain leads | Auditoria completa de compliance usando [`compliance-audit-quality`](../checklists/compliance-audit-quality.md). Mapeamento de controles contra [`nist-800-53`](../frameworks/nist-800-53-controls.md), [`iso-27001`](../frameworks/iso-27001-isms.md), [`cis-controls`](../frameworks/cis-controls-v8.md). Gaps documentados com plano de remediacao. | [`data/scorecards/`](../data/scorecards/) |

**Criterio de saida**: estrategia publicada, maturity assessment concluido, compliance audit com remediation plan.

---

## 7. Calendario Consolidado

```
DIARIO  ──── Alert triage + Incident status
              |
SEMANAL ──── Vuln backlog + Detection review + Cross-squad queue
              |
MENSAL  ──── Metrics dashboard + Maturity score + Improvement grooming
              |
TRIMESTRAL ── Tabletop + Risk register + Integration health + KPI recalib
              |
ANUAL   ──── Strategy review + Red team maturity + Compliance audit
```

Cada cadencia alimenta a proxima: dados diarios informam revisoes semanais, tendencias semanais alimentam analises mensais, metricas mensais embasam decisoes trimestrais, e avaliacoes trimestrais compoem a revisao anual.

---

## Referencias Cruzadas

- [`config.yaml`](../config.yaml) — secao `cadence`, `kpis`
- [`data/metrics/`](../data/metrics/) — security-kpis, vulnerability-metrics, detection-metrics, maturity-score-history
- [`data/registries/`](../data/registries/) — incident-registry, findings-registry, detection-rules-registry, risk-register, decisions-log, lessons-learned-registry
- [`data/scorecards/`](../data/scorecards/) — squad-scorecard
- [`frameworks/security-kpi-dashboard.md`](../frameworks/security-kpi-dashboard.md) — framework de KPIs
- [`frameworks/red-team-maturity-model.md`](../frameworks/red-team-maturity-model.md) — modelo de maturidade
- [`docs/quality-gate-system.md`](./quality-gate-system.md) — quality gates aplicados em reviews de cadencia

---

*Cybersecurity Squad — Cadence Operations v1.0.0*
