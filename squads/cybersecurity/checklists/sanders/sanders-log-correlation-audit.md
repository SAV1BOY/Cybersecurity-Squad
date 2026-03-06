# Sanders - Log Correlation Audit

Checklist para auditoria de correlacao de logs de seguranca.

## Inventario de Log Sources
- [ ] Todas as log sources ativas catalogadas
- [ ] Log format de cada source documentado (syslog, JSON, CEF, LEEF)
- [ ] Log volume por source medido (EPS - Events Per Second)
- [ ] Log retention period por source verificado
- [ ] Log collection method documentado (agent, syslog, API, file)
- [ ] Gaps de cobertura identificados (systems sem logging)
- [ ] Log source health monitoring implementado

## Normalizacao e Parsing
- [ ] Parsers configurados para cada log source
- [ ] Field mapping normalizado para schema comum
- [ ] Timestamp parsing correto e em UTC
- [ ] Source IP e destination IP extraidos corretamente
- [ ] Username/identity fields normalizados entre sources
- [ ] Hostname resolution funcional e consistente
- [ ] Custom parsers testados com sample data

## Regras de Correlacao
- [ ] Correlation rules catalogadas com objetivo de cada uma
- [ ] Rules mapeadas a use cases de seguranca (brute force, lateral movement)
- [ ] Multi-source correlation implementada (firewall + auth + endpoint)
- [ ] Time-based correlation com janelas adequadas
- [ ] Threshold-based rules calibradas para o ambiente
- [ ] Statistical baseline rules configuradas (anomaly detection)
- [ ] Kill chain correlation rules implementadas (multi-stage attacks)

## Eficacia das Correlacoes
- [ ] True positive rate medido por correlation rule
- [ ] False positive rate medido e aceitavel (< 20%)
- [ ] Mean time to detect (MTTD) calculado por cenario
- [ ] Rules sem triggers nos ultimos 90 dias revisadas
- [ ] Rules com excessive false positives tuned ou desabilitadas
- [ ] Coverage matrix ATT&CK vs correlation rules atualizada
- [ ] Red team/purple team results validam correlation effectiveness

## Enrichment e Contexto
- [ ] Asset inventory integrado para enriquecimento
- [ ] Threat intelligence feeds integrados
- [ ] GeoIP enrichment configurado
- [ ] User identity enrichment funcional (HR data, role)
- [ ] Vulnerability data integrada para contexto
- [ ] Risk scoring dinAmico implementado

## Operacao e Manutencao
- [ ] Correlation rule lifecycle management definido
- [ ] Tuning schedule estabelecido (monthly/quarterly review)
- [ ] New log source onboarding process documentado
- [ ] SIEM performance monitored (search latency, indexing lag)
- [ ] Correlation rule versioning implementado
- [ ] Documentation atualizada para cada rule change
- [ ] Report de audit entregue com findings e recommendations
