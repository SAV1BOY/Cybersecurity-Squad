# SOC Buildout Project

Template de projeto para construcao ou maturacao de um Security Operations Center.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Tipo | [Greenfield / Maturation] |
| Modelo | [Internal / Hybrid / MSSP] |
| Cobertura | [8x5 / 12x5 / 24x7] |
| Timeline | [3-6 meses para MVP] |
| Headcount | [Definir por cobertura] |
| Budget | [Ferramentas + pessoas] |

## Fase 1: Foundation (Mes 1-2)

### Pessoas
- [ ] Definicao de roles: SOC Manager, L1/L2/L3 Analysts, Detection Engineer
- [ ] Hiring plan conforme cobertura desejada
- [ ] On-call rotation e escalacao definidos
- [ ] Treinamento inicial planejado

### Tecnologia
- [ ] SIEM selecionado e implementado
- [ ] EDR deployado em endpoints
- [ ] Ticketing system para case management
- [ ] Comunicacao (Slack channels, PagerDuty)

### Processos
- [ ] Alert triage workflow definido
- [ ] Severity classification criteria documentado
- [ ] Escalacao path para cada severidade
- [ ] Handoff procedures entre turnos

## Fase 2: Log Sources e Deteccoes (Mes 2-3)

### Log Sources Prioritarios
| Priority | Source | Tipo |
|----------|--------|------|
| P1 | Authentication logs | Identity |
| P1 | EDR telemetry | Endpoint |
| P1 | Firewall logs | Network |
| P2 | Cloud audit logs | Cloud |
| P2 | Email gateway | Email |
| P2 | WAF logs | Application |
| P3 | DNS logs | Network |
| P3 | Proxy logs | Network |

### Regras de Deteccao Iniciais
- [ ] Top 20 regras para ameacas mais comuns
- [ ] Alertas de alta fidelidade priorizados
- [ ] Tuning inicial baseado em 2 semanas de dados

## Fase 3: Operacionalizacao (Mes 3-4)

- [ ] Playbooks para top 10 cenarios de alerta
- [ ] Metricas operacionais definidas (MTTD, MTTA, MTTR)
- [ ] Dashboard operacional configurado
- [ ] Daily standup e weekly review implementados
- [ ] Processo de quality assurance para cases

## Fase 4: Maturacao (Mes 4-6+)

- [ ] Threat hunting program iniciado
- [ ] SOAR para automacao de tarefas repetitivas
- [ ] Purple team exercises regulares
- [ ] Detection as code workflow
- [ ] Continuous improvement baseado em metricas
