# Threat Hunt Quality Gate

Checklist de qualidade para operacoes de threat hunting.

## Planejamento da Hunt
- [ ] Hipotese de hunting documentada e especifica
- [ ] MITRE ATT&CK technique alvo identificada
- [ ] Intelligence source que motivou a hunt documentada
- [ ] Data sources necessarias identificadas e acessiveis
- [ ] Timeframe da hunt definido (periodo de dados a analisar)
- [ ] Ferramentas e queries preparadas antecipadamente
- [ ] Baseline de atividade normal compreendido

## Execucao
- [ ] Queries executadas contra dados historicos e em tempo real
- [ ] Multiple data sources correlacionadas (endpoint, network, auth)
- [ ] Anomalias estatisticas investigadas (frequency, volume, timing)
- [ ] Stacking e grouping aplicados para identificar outliers
- [ ] Long tail analysis realizada para comportamentos raros
- [ ] Known-good whitelisting aplicado para reduzir ruido
- [ ] Pivot entre indicadores realizado (IP -> domain -> hash -> user)

## Analise de Resultados
- [ ] Cada anomalia investigada ate conclusao (benign ou malicious)
- [ ] False positives documentados para tuning futuro
- [ ] True positives escalados como incidents imediatamente
- [ ] IOCs extraidos e compartilhados com equipe de deteccao
- [ ] TTP patterns documentados para deteccao futura
- [ ] Scope do comprometimento avaliado (se encontrado)

## Conversao para Deteccao
- [ ] Findings convertidos em detection rules (Sigma/SIEM)
- [ ] Novos IOCs adicionados a threat intelligence platform
- [ ] Playbooks atualizados com novos cenarios encontrados
- [ ] Gaps de visibilidade identificados e reportados
- [ ] Data source improvements recomendados

## Documentacao e Metricas
- [ ] Hunt report completo com hipotese, metodo e resultados
- [ ] Tempo investido na hunt registrado
- [ ] Cobertura da hunt mapeada ao ATT&CK Navigator
- [ ] Lessons learned documentadas
- [ ] Hunt backlog atualizado com proximas hipoteses
- [ ] Resultados apresentados para a equipe de SOC
- [ ] Metricas de hunting atualizadas (hunts/month, findings/hunt)
