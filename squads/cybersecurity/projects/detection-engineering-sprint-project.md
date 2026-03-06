# Detection Engineering Sprint Project

Template de projeto para sprints de detection engineering.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Sprint | [Numero/Nome] |
| Duracao | 2 semanas |
| Equipe | [Detection engineers + SOC analysts] |
| Foco | [Tatica MITRE ou threat especifico] |
| Objetivo | [N regras novas, M regras tuned] |

## Sprint Planning

### Inputs para Priorizacao
- [ ] Gaps de cobertura MITRE ATT&CK identificados
- [ ] Threat intelligence recente (ameacas ativas)
- [ ] Findings de red team / purple team
- [ ] False positive backlog para tuning
- [ ] Lessons learned de incidentes recentes

### Sprint Backlog

| Item | Type | MITRE | Priority | Assignee | Status |
|------|------|-------|----------|----------|--------|
| [Regra 1] | New | T1059.001 | P1 | @eng-1 | To Do |
| [Regra 2] | New | T1021.002 | P1 | @eng-2 | To Do |
| [Regra 3] | Tune | T1110.001 | P2 | @eng-1 | To Do |
| [Test case 1] | Validate | T1003 | P2 | @eng-2 | To Do |

## Workflow por Regra

### Criacao de Nova Regra
1. [ ] Hipotese de deteccao documentada
2. [ ] Data sources necessarios confirmados disponiveis
3. [ ] Query/logica desenvolvida
4. [ ] Unit tests escritos
5. [ ] Teste com dados reais em ambiente de staging
6. [ ] Code review por peer
7. [ ] Deploy para producao
8. [ ] Documentacao atualizada no detection-rules-registry

### Tuning de Regra Existente
1. [ ] Analise de false positives recentes
2. [ ] Identificacao de pattern de FPs
3. [ ] Ajuste de logica/threshold/exclusions
4. [ ] Validacao de que true positives nao sao perdidos
5. [ ] Deploy e monitoramento por 1 semana

## Sprint Review

- Regras entregues vs. planejadas
- Cobertura MITRE ATT&CK atualizada
- Reducao de false positive rate
- Feedback do SOC sobre qualidade dos alertas

## Retrospectiva

- O que funcionou bem neste sprint
- O que pode melhorar
- Impedimentos encontrados
- Action items para proximo sprint
