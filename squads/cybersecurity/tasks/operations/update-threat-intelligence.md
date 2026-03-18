# Task: Update Threat Intelligence

## Objetivo
Atualizar a base de threat intelligence do squad com novos IOCs, TTPs, threat actor profiles e tendencias, mantendo a defesa informada e proativa.

## Agents
- **rogue** (lead) — Atualiza TTPs e threat actor profiles
- **shannon-runner** (executor) — Processa e correlaciona indicadores

## Inputs
- Threat intelligence feeds (OSINT e comerciais)
- MITRE ATT&CK updates
- ISACs e comunidades do setor
- Incidentes publicos relevantes

## Steps
1. Coletar updates de threat intelligence feeds configurados
2. Processar novos IOCs (hashes, IPs, dominios, URLs)
3. Atualizar threat actor profiles com novas TTPs observadas
4. Correlacionar novos IOCs com ativos do ambiente
5. Atualizar mapeamento MITRE ATT&CK com novas tecnicas
6. Verificar se deteccoes existentes cobrem novas TTPs
7. Criar alerta para TTPs relevantes sem deteccao
8. Disseminar intelligence relevante para equipes operacionais
9. Arquivar intelligence expirada ou irrelevante
10. Registrar atualizacoes no `findings-registry`

## Output
- Base de threat intelligence atualizada
- Novos IOCs processados e correlacionados
- Threat actor profiles atualizados
- Alertas para TTPs sem cobertura de deteccao

## Quality Gates
- [ ] Fontes de intelligence multiplas e confiáveis consultadas
- [ ] IOCs processados e correlacionados com ambiente
- [ ] Threat actor profiles atualizados com TTPs recentes
- [ ] Gaps de deteccao para novas TTPs identificados
- [ ] Intelligence disseminada para equipes operacionais

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | mitre-att-ck, mitre-atlas |
| Checklists | threat-hunt-quality |
| Templates | reports/technical-report-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Receives from**: daily/weekly cadence
- **Delivers to**: threat-hunting-sprint
