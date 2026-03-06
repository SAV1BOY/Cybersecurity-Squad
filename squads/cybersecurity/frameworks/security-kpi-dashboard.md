# Security KPI Dashboard — Framework Interno

> Metricas que importam para medir a saude do programa de seguranca.

## Principio

"Se voce nao mede, voce nao gerencia." Mas medir errado e pior que nao medir. KPIs devem ser: acionaveis, comparaveis ao longo do tempo, e conectados a decisoes reais.

## KPIs Operacionais

### Deteccao & Resposta
| KPI | Descricao | Target | Medicao |
|-----|-----------|--------|---------|
| MTTD | Mean Time to Detect (da intrusao ate o alerta) | < 24h | Mediana dos incidentes |
| MTTR | Mean Time to Respond (do alerta ate contencao) | < 4h (P1) | Mediana por severidade |
| Alert-to-Triage | Tempo do alerta ate primeiro triage | < 15 min | Mediana |
| FP Rate | % de alertas que sao falsos positivos | < 10% | Mensal |
| Detection Coverage | % tecnicas ATT&CK com deteccao ativa | > 70% | Trimestral |
| Hunting Conversion | % de hunts que geram nova deteccao | > 30% | Por sprint |

### Vulnerability Management
| KPI | Descricao | Target | Medicao |
|-----|-----------|--------|---------|
| Vuln SLA Compliance | % corrigidas dentro do SLA | > 90% | Mensal |
| MTTR-emediation | Tempo medio de correcao | P1: 72h, P2: 14d | Mediana |
| Critical Backlog | Vulns P1 abertas agora | < 5 | Semanal |
| Backlog Aging | Idade media do backlog | < 30 dias | Mensal |
| Retest Rate | % de fixes retestados | > 95% | Mensal |
| Fix Rejection | % de fixes que falharam no reteste | < 15% | Mensal |

### AppSec
| KPI | Descricao | Target | Medicao |
|-----|-----------|--------|---------|
| SSDLC Coverage | % de projetos com security gates | > 80% | Trimestral |
| Code Review Coverage | % de PRs com security review | > 90% (criticos) | Mensal |
| Champion Coverage | % de dev teams com security champion | > 50% | Trimestral |
| Dependency Vulns | Vulns criticas em dependencias | 0 unpatched > 30d | Semanal |

### Incidentes
| KPI | Descricao | Target | Medicao |
|-----|-----------|--------|---------|
| Incident Volume | Numero de incidentes por mes | Trending down | Mensal |
| Severity Distribution | P1/P2/P3/P4 ratio | P1 < 5% | Mensal |
| Postmortem Rate | % de P1/P2 com postmortem | 100% | Mensal |
| Action Completion | % de acoes de postmortem completadas | > 90% | Trimestral |
| Repeat Incidents | % de incidentes com mesma root cause | < 10% | Trimestral |

## KPIs Estrategicos

| KPI | Descricao | Target | Medicao |
|-----|-----------|--------|---------|
| Security Maturity | Score 1-5 por dominio | > 3.5 | Semestral |
| Risk Posture Trend | Melhorando/estavel/piorando | Melhorando | Trimestral |
| Compliance Posture | % controles implementados | > 90% | Trimestral |
| Tabletop Frequency | Exercicios realizados | >= 4/ano | Anual |
| Security Culture Score | Pesquisa de awareness | > 80% | Anual |

## Dashboard Visual

```
[SEMAFORO GERAL]
🟢 Green: Todos os KPIs dentro do target
🟡 Yellow: 1-2 KPIs fora do target, sem risco critico
🔴 Red: KPI critico fora do target ou tendencia negativa

[TRENDING]
↑ Melhorando | → Estavel | ↓ Piorando

[TOP 3 RISCOS]
1. [Risco + owner + prazo]
2. [Risco + owner + prazo]
3. [Risco + owner + prazo]
```

## Cadencia de Reporting

| Frequencia | Audiencia | Conteudo |
|------------|-----------|----------|
| Semanal | Squad | Metricas operacionais detalhadas |
| Mensal | Lideranca tecnica | KPIs + trending + top risks |
| Trimestral | Executivo | Postura + investimento + decisoes |
| Anual | Board | Estrategia + maturidade + benchmarks |

## Anti-Patterns

- **Vanity metrics**: Medir numero de scans e nao numero de fixes
- **Averages lie**: Usar mediana, nao media (outliers distorcem)
- **Measuring activity, not outcome**: Numero de alertas nao e KPI, resolucao e
- **Too many KPIs**: Se tudo e metrica, nada e metrica — focar em < 15
