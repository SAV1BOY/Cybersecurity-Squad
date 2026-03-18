# Task: Threat Hunting Sprint

## Objetivo
Conduzir sprints de threat hunting proativas, buscando indicadores de comprometimento e atividade adversaria que regras automaticas de deteccao podem nao captar.

## Agents
- **chris-sanders** (lead) — Lidera hunting e analise
- **rogue** (support) — Fornece perspectiva adversaria
- **shannon-runner** (executor) — Executa anomaly detection

## Inputs
- Threat intelligence atualizada
- MITRE ATT&CK techniques prioritarias
- Logs e telemetria disponiveis
- Hipoteses de hunting baseadas em threat landscape

## Steps
1. Formular hipoteses de hunting baseadas em threat intelligence
2. Identificar data sources necessarios para cada hipotese
3. Desenvolver queries de hunting (KQL, SPL, Lucene)
4. Executar queries contra dados de telemetria
5. Analisar resultados com foco em anomalias e outliers
6. Investigar indicadores suspeitos com deep-dive analysis
7. Documentar findings positivos com evidencia
8. Converter findings em regras de deteccao permanentes
9. Documentar hipoteses negativas para knowledge base
10. Registrar findings no `findings-registry`

## Output
- Relatorio de threat hunting com hipoteses e resultados
- Findings positivos documentados com evidencia
- Novas regras de deteccao derivadas do hunting
- Knowledge base atualizada com hipoteses testadas

## Quality Gates
- [ ] Hipoteses de hunting baseadas em threat intelligence
- [ ] Queries de hunting documentadas e reproduziveis
- [ ] Findings positivos investigados com deep-dive
- [ ] Findings convertidos em regras de deteccao permanentes
- [ ] Hipoteses negativas documentadas na knowledge base
- [ ] Checklist `threat-hunt-quality` atendido
- [ ] Checklist `sanders-packet-analysis` validado

## Routing & Escalation
- **frameworks**: mitre-att-ck, diamond-model
- **checklists**: threat-hunt-quality, sanders/sanders-packet-analysis
- **templates**: reports/technical-report-template
- **registry**: data/registries/findings-registry
- **receives_from**: threat-landscape-analysis
- **delivers_to**: detection-rule-development (new rules)
