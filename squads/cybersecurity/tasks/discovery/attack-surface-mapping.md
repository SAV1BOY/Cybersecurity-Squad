# Task: Attack Surface Mapping

## Objetivo
Mapear a superficie de ataque completa dos ativos in-scope, identificando todos os pontos de entrada potenciais que um atacante poderia explorar.

## Agents
- **cartographer** (lead) — Mapeia superficie de ataque
- **busterer** (executor) — Enumera endpoints e servicos
- **dirber** (executor) — Enumera diretórios e paths web
- **peter-kim** (reviewer) — Valida completude do mapeamento

## Inputs
- Asset inventory atualizado (asset-discovery)
- ROE com scope boundaries
- Threat model preliminar (se disponivel)

## Steps
1. Enumerar todos os endpoints HTTP/HTTPS com crawling e brute-force
2. Mapear APIs expostas (REST, GraphQL, SOAP, gRPC)
3. Identificar entry points de autenticacao e formularios
4. Catalogar servicos de rede expostos (SSH, RDP, FTP, SMB, DB)
5. Mapear DNS records (A, CNAME, MX, TXT, SRV, DMARC, SPF)
6. Identificar cloud entry points (management consoles, APIs)
7. Documentar componentes de terceiros e integrações expostas
8. Classificar entry points por nivel de exposicao e risco
9. Mapear findings contra MITRE ATT&CK Initial Access techniques
10. Gerar relatorio tecnico com mapa de superficie

## Output
- Mapa de attack surface completo por ativo
- Lista de entry points classificados por risco
- Mapeamento MITRE ATT&CK de tecnicas de Initial Access
- Registro no `findings-registry`

## Quality Gates
- [ ] Todos os ativos in-scope cobertos pelo mapeamento
- [ ] APIs e endpoints web enumerados e catalogados
- [ ] Servicos de rede mapeados com versoes identificadas
- [ ] Entry points classificados por nivel de exposicao
- [ ] Mapeamento contra MITRE ATT&CK realizado
- [ ] Checklist `attack-surface-mapping-quality` atendido
- [ ] Checklist `kim-recon-checklist` validado

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | discovery-layer, mitre-att-ck |
| Checklists | attack-surface-mapping-quality, kim/kim-recon-checklist |
| Templates | reports/technical-report-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: asset-discovery
- **Delivers to**: red-team/appsec/cloudsec tasks
