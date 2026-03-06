# Red Team - Attack Chain Review

Checklist para revisao de cadeia de ataque em engagements de red team.

## Mapeamento da Attack Chain
- [ ] Kill chain completa documentada (initial access to objective)
- [ ] Cada fase da kill chain com timestamps inicio/fim
- [ ] MITRE ATT&CK techniques mapeadas para cada etapa
- [ ] Ferramentas utilizadas em cada fase documentadas
- [ ] Dificuldade de cada etapa avaliada (trivial, moderate, hard)
- [ ] Tempo investido em cada fase registrado
- [ ] Pontos de decisao e pivots documentados

## Initial Access Review
- [ ] Vector de initial access documentado com detalhes
- [ ] Alternativas de initial access tentadas e resultados
- [ ] Tempo para initial access registrado
- [ ] Deteccao durante initial access avaliada
- [ ] Lessons learned sobre initial access documentadas

## Execution e Persistence Review
- [ ] Execution methods revisados para stealth e reliability
- [ ] Persistence mechanisms avaliados para survivability
- [ ] Detection surface de persistence avaliada
- [ ] Backup persistence methods implementados
- [ ] Timing de persistence implantation revisado

## Lateral Movement Review
- [ ] Cada hop documentado com justificativa
- [ ] Credential usage tracked (which creds, where, when)
- [ ] Most efficient path identificado vs path taken
- [ ] Detection opportunities em cada hop avaliadas
- [ ] Network segmentation effectiveness avaliada em cada hop
- [ ] Alternative paths identificados e documentados

## Objective Achievement Review
- [ ] Objectives atingidos listados com evidence
- [ ] Objectives nao atingidos com explicacao
- [ ] Crown jewels accessed documentados
- [ ] Business impact demonstrado para cada objective
- [ ] Time to objective calculado

## Detection e Response Analysis
- [ ] Pontos onde red team foi detectado identificados
- [ ] Blue team response actions documentadas
- [ ] Evasion techniques que funcionaram catalogadas
- [ ] Evasion techniques que falharam documentadas
- [ ] MTTD (Mean Time to Detect) por fase calculado
- [ ] Gaps de deteccao identificados para blue team

## Improvement Opportunities
- [ ] Attack chain optimizations identificadas
- [ ] Tool improvements necessarios documentados
- [ ] TTP refinements para proximos engagements
- [ ] Client-specific defenses que bloquearam ataques documentadas
- [ ] Recommendations para o cliente baseadas na attack chain
- [ ] Report de attack chain review completo e entregue
