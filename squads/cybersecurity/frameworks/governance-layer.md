# Governance Layer — Framework Operacional

> Camada de governanca: risco, compliance util, cadencia, metricas e melhoria continua.

## Objetivo

A Governance Layer garante que o programa de seguranca e gerenciado como um sistema: com metricas, cadencias, decisoes baseadas em dados e melhoria continua. Nao e burocracia — e o "sistema operacional" que faz todas as outras camadas funcionarem de forma coordenada.

## Principios

1. **Metricas > opinioes** — Decisoes baseadas em dados, nao em feeling
2. **Compliance util > compliance theater** — Evidencia real, nao checkbox
3. **Risco quantificado > risco qualitativo** — Mover de High/Medium/Low para valores
4. **Cadencia e disciplina** — Reviews regulares, nao ad-hoc
5. **Transparencia com lideranca** — Risco comunicado de forma clara e acionavel
6. **Prioridade por impacto de negocio** — Seguranca serve o negocio

## Componentes

### 1. Risk Management
- **Risk register**: Registro centralizado de riscos (aceitos, mitigados, abertos)
- **Risk scoring**: FAIR para quantificacao, risk matrix para comunicacao
- **Risk appetite**: Definido pela lideranca, respeitado pelo squad
- **Risk reviews**: Trimestral com lideranca, mensal internamente
- **Exception management**: Excecoes documentadas com prazo e justificativa

### 2. Compliance Management
- **Control mapping**: Mapear controles para multiplos frameworks (NIST, CIS, ISO, PCI)
- **Evidence automation**: Coletar evidencia automaticamente onde possivel
- **Gap tracking**: Dashboard de gaps e plano de remediacao
- **Audit readiness**: Evidencia sempre pronta, nao "corrida antes do auditor"

### 3. Security Metrics & KPIs
```
Metricas operacionais:
- MTTD (Mean Time to Detect)
- MTTR (Mean Time to Respond)
- MTTR-emediation (Mean Time to Remediate vulns)
- Vuln SLA compliance (% corrigidas no prazo)
- Detection coverage (% ATT&CK)
- False positive rate
- Security maturity score
- Critical vuln backlog

Metricas estrategicas:
- Risk posture trend (melhorando/piorando)
- Security investment ROI
- Incident frequency and impact trend
- Compliance posture
- Security culture score
```

### 4. Cadencia Operacional

| Frequencia | Atividade |
|------------|-----------|
| Diaria | Alert triage, incident response |
| Semanal | Vuln backlog review, detection tuning |
| Quinzenal | Sprint de hunting, purple team mini |
| Mensal | Security metrics review, cross-squad sync |
| Trimestral | Quarterly security review, tabletop exercise |
| Semestral | Maturity assessment, red team engagement |
| Anual | Security program strategy, budget planning |

### 5. Decision Framework
Para cada decisao de seguranca:
1. **Qual o risco?** (impacto x probabilidade)
2. **Qual o custo de mitigar?** (esforco x timeline)
3. **Qual o risco residual?** (apos mitigacao)
4. **Quem decide?** (risk owner, nao security team)
5. **Documentar** (decisions-log.md)

### 6. Cross-Squad Coordination
- **Dev Squad**: Findings -> backlog, SDLC gates, security requirements
- **Infra Squad**: Hardening, monitoring, guardrails
- **Compliance Squad**: Evidence, control mappings, risk register
- **Product Squad**: Threat models, security requirements, risk trade-offs

## Reporting

### Para Lideranca Executiva (Board)
- Risk posture resumido (semaforo + tendencia)
- Top 5 riscos com plano de acao
- Incidentes significativos
- Investimento vs. resultado
- Comparacao com benchmarks do setor

### Para Lideranca Tecnica
- KPIs detalhados
- Vuln backlog aging
- Detection coverage gaps
- Incident trends
- Maturity score by domain

### Para o Squad
- Sprint metrics
- Individual KPIs
- Improvement actions
- Recognition

## Agentes Envolvidos

| Agente | Papel na Governance Layer |
|--------|--------------------------|
| Cyber Chief | Estrategia, priorizacao, decisoes, reporting executivo |
| Marcus Carey | Cultura, cadencia, comunicacao, lessons learned |
| Omar Santos | Metricas operacionais, SOC KPIs |
| Chris Sanders | Metricas de deteccao, hunting effectiveness |

## Outputs

- Quarterly security report
- Risk register atualizado
- Security KPI dashboard
- Compliance evidence packages
- Decision log
- Maturity assessment

## Quality Gates

- `compliance-audit-quality.md`
- `security-report-quality.md`

## Used By

### Tasks (config.yaml routing)
- define-success-criteria
- setup-comms-and-escalation
- sdlc-security-gates-setup
- cloud-guardrails-setup
- policy-review
- security-posture-analysis
- maturity-assessment
- roi-security-investment-analysis
- quarterly-security-review
- cross-squad-sync
- maintain-checklists-and-standards
- security-policy-review
- compliance-gap-analysis

### Agents
- cyber-chief
- marcus-carey

### Related Checklists
- compliance-audit-quality

### Cross-References
- Config routing: `config.yaml`
- Quality gate system: `docs/quality-gate-system.md`
