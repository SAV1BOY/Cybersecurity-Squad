# Detection Engineering Quality Gate

Checklist de qualidade para engenharia de deteccao.

## Design da Deteccao
- [ ] Use case documentado com threat scenario especifico
- [ ] MITRE ATT&CK technique mapeada para a deteccao
- [ ] Data sources necessarias identificadas e disponiveis
- [ ] Detection logic documentada em pseudocode antes de implementar
- [ ] False positive scenarios antecipados e documentados
- [ ] Bypass scenarios conhecidos documentados
- [ ] Cobertura da deteccao definida (host, network, cloud, app)

## Implementacao
- [ ] Query/rule escrita na linguagem do SIEM (Sigma, KQL, SPL)
- [ ] Sigma rule criada para portabilidade entre SIEMs
- [ ] Rule syntax validada sem erros
- [ ] Performance da query testada (execution time aceitavel)
- [ ] Fields normalizados conforme schema do SIEM
- [ ] Threshold e time window calibrados
- [ ] Correlation com outras deteccoes implementada (se aplicavel)

## Teste e Validacao
- [ ] Deteccao testada com simulacao de ataque real (Atomic Red Team)
- [ ] True positive confirmado em ambiente de teste
- [ ] False positive rate medido em dados de producao (baseline)
- [ ] Edge cases testados (encoding, evasion, variations)
- [ ] Deteccao nao gera alertas em atividade normal (1 semana min)
- [ ] Performance impact no SIEM avaliado

## Operacionalizacao
- [ ] Alert severity e priority configurados
- [ ] Triage playbook/SOP criado para o alerta
- [ ] Alert routing configurado (team, channel, escalation)
- [ ] Enrichment automatico configurado (threat intel, asset info)
- [ ] Response actions documentadas para o analista
- [ ] SOAR automation implementada (se aplicavel)

## Documentacao e Lifecycle
- [ ] Detection catalog atualizado com nova regra
- [ ] Owner da deteccao definido
- [ ] Review cadence estabelecida (tuning quarterly)
- [ ] Metricas de eficacia coletadas (TP rate, MTTR)
- [ ] Version control aplicado para detection rules
- [ ] Retirement criteria definidos para deteccao obsoleta
