# Task: Recon & Enumeration

## Objetivo
Executar reconhecimento e enumeracao detalhada dos ativos in-scope, coletando informacoes que alimentarao as fases subsequentes de vulnerability assessment e exploitation.

## Agents
- **peter-kim** (lead) — Direciona estrategia de recon
- **busterer** (executor) — Brute-force de endpoints e servicos
- **dirber** (executor) — Enumeracao de diretorios web
- **cartographer** (support) — Complementa mapeamento

## Inputs
- Asset inventory e attack surface map
- ROE com scope boundaries aprovados
- Informacoes publicas sobre o alvo (OSINT baseline)

## Steps
1. Executar passive recon: OSINT, Google dorks, Shodan, certificate transparency
2. Enumerar DNS: subdominios, zone transfers, brute-force
3. Realizar port scanning detalhado (full TCP + top UDP)
4. Fingerprint de servicos e versoes em portas abertas
5. Enumerar diretorios web e virtual hosts
6. Identificar tecnologias e frameworks em uso (web stack)
7. Coletar informacoes de autenticacao (login pages, default creds)
8. Mapear relacoes entre servicos e dependencias
9. Documentar todos os findings com evidencia (screenshots, outputs)
10. Registrar no `findings-registry`

## Output
- Relatorio de recon com todos os dados coletados
- Lista de servicos, versoes e tecnologias por ativo
- Mapa de relacoes e dependencias
- Evidencias com hash SHA-256

## Quality Gates
- [ ] Recon limitado ao scope autorizado (ROE)
- [ ] Passive recon executado antes de active recon
- [ ] Full port scan realizado nos ativos criticos
- [ ] Servicos e versoes fingerprinted com precisao
- [ ] Evidencias documentadas com hash SHA-256
- [ ] Checklist `kim-recon-checklist` 100% atendido
- [ ] Checklist `redteam-safe-testing-rules` validado

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | offense-layer, ptes-penetration-testing |
| Checklists | kim/kim-recon-checklist, red-team/redteam-safe-testing-rules |
| Templates | reports/finding-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: discovery phase
- **Delivers to**: vuln-validation
