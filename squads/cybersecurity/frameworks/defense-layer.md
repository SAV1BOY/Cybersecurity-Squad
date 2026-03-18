# Defense Layer — Framework Operacional

> Camada defensiva: visibilidade, deteccao, resposta e melhoria continua.

## Objetivo

A Defense Layer garante que a organizacao consegue ver, detectar e responder a ameacas em tempo real. Nao basta ter ferramentas — e preciso visibilidade completa, deteccoes de qualidade, e processos de resposta testados. O objetivo e reduzir MTTD (Mean Time to Detect) e MTTR (Mean Time to Respond) continuamente.

## Principios

1. **Visibilidade antes de deteccao** — Sem logs, nao ha deteccao
2. **Deteccao como codigo** — Regras versionadas, testadas, revisadas
3. **Qualidade > quantidade** — 10 regras boas > 1000 com falsos positivos
4. **Context enrichment** — Alerta sem contexto e ruido
5. **Assume breach** — Sempre operar como se ja houvesse um invasor
6. **Melhoria continua** — Cada incidente e exercicio melhora a defesa
7. **Purple loop** — Red Team findings viram deteccoes novas

## Pilares da Defesa

### 1. Visibilidade (Logging & Telemetry)
```
Fontes obrigatorias:
- Authentication logs (IdP, AD, cloud IAM)
- Network flow logs (VPC flow, firewall)
- Endpoint telemetry (EDR, sysmon, auditd)
- Application logs (auth events, errors, access)
- Cloud audit trails (CloudTrail, Activity Log)
- Email gateway logs
- DNS query logs
- Web proxy/WAF logs
```

**Matriz de visibilidade**: Para cada tecnica ATT&CK relevante, mapear:
- Fonte de log necessaria
- Se a fonte esta configurada
- Se os logs estao sendo coletados
- Se ha regra de deteccao

### 2. Deteccao (Detection Engineering)
```
Ciclo de vida de uma regra:
1. Hipotese (qual tecnica/comportamento detectar?)
2. Data source (qual log fornece o sinal?)
3. Logic (qual query/correlacao identifica o evento?)
4. Threshold (qual limiar reduz falsos positivos?)
5. Context (quais enrichments adicionam valor?)
6. Validation (testar com simulacao real)
7. Deploy (colocar em producao)
8. Tuning (ajustar com feedback operacional)
```

### 3. Triage (Alert Triage)
```
Processo de triage:
1. Receber alerta
2. Contexto rapido: quem, o que, quando, onde
3. Classificar: TP / FP / Benign TP
4. Se TP: escalar conforme severidade
5. Se FP: documentar e tunar regra
6. Tempo maximo para triage inicial: 15 min
```

### 4. Resposta (Incident Response)
- Coberta pela IR Layer (framework separado)
- Defense Layer garante readiness: playbooks, contatos, ferramentas

### 5. Threat Hunting
```
Sprint de hunting:
1. Formular hipotese baseada em intel/gap
2. Identificar datasets relevantes
3. Construir queries
4. Analisar resultados
5. Documentar findings (positivos e negativos)
6. Converter findings em deteccoes permanentes
```

## Metricas da Defense Layer

| Metrica | Descricao | Target |
|---------|-----------|--------|
| MTTD | Tempo medio de deteccao | < 24h |
| MTTR | Tempo medio de resposta | < 4h (critico) |
| Detection Coverage | % ATT&CK com regra ativa | > 70% |
| FP Rate | % alertas falso positivo | < 10% |
| Alert-to-Triage Time | Tempo ate primeiro triage | < 15 min |
| Hunting Conversion Rate | % hunts que viram deteccao | > 30% |

## Agentes Envolvidos

| Agente | Papel na Defense Layer |
|--------|----------------------|
| Chris Sanders | Analise de pacotes, timeline, correlacao, hunting |
| Omar Santos | SOC ops, hardening, baselines, alert triage |
| Shannon Runner | Anomaly detection, entropy analysis, pattern discovery |
| Command Generator | Scripts de coleta e automacao de resposta |
| Cyber Chief | Priorizacao, metricas, governance |

## MITRE ATT&CK Integration

A Defense Layer usa ATT&CK como lingua franca:
- **Mapeamento**: Cada regra de deteccao e mapeada para tecnica(s) ATT&CK
- **Cobertura**: Dashboard de cobertura por tatica (Initial Access -> Exfiltration)
- **Gaps**: Identificar taticas/tecnicas sem deteccao
- **Purple Team**: Red testa tecnica X -> Blue verifica se detectou -> Gap? -> Nova regra

## Outputs

- Detection coverage matrix (ATT&CK mapping)
- Regras de deteccao validadas
- Playbooks de resposta
- Hunting reports
- SOC operations dashboard (KPIs)

## Quality Gates

- `detection-engineering-quality.md`
- `blue-team/blueteam-detection-coverage.md`
- `blue-team/blueteam-tuning-checklist.md`
- `blue-team/blueteam-monitoring-slo.md`

## Used By

### Tasks (config.yaml routing)
- logging-and-visibility-gap-audit
- detection-rule-development
- soc-operations-improvement
- cloud-logging-setup

### Agents
- chris-sanders
- omar-santos
- shannon-runner

### Related Checklists
- detection-engineering-quality
- blue-team/blueteam-detection-coverage

### Cross-References
- Config routing: `config.yaml`
- Quality gate system: `docs/quality-gate-system.md`
