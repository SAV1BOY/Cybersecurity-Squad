# Task: Asset Scoping

## Objetivo
Identificar, catalogar e validar todos os ativos dentro do escopo do engagement, criando um inventario preciso para direcionar atividades subsequentes.

## Agents
- **cyber-chief** (lead) — Coordena o processo de scoping
- **cartographer** (executor) — Mapeia e cataloga ativos

## Inputs
- Documento de ROE com scope boundaries
- Informacoes fornecidas pelo cliente (IP ranges, dominios, aplicacoes)
- Asset inventory existente (se disponivel)

## Steps
1. Coletar IP ranges, CIDR blocks e dominios fornecidos pelo cliente
2. Validar ownership dos ativos listados (WHOIS, DNS, certificados)
3. Identificar subdominios e ativos associados dentro do scope
4. Catalogar aplicacoes web, APIs e servicos expostos
5. Mapear ambientes (production, staging, development)
6. Identificar third-party systems e shared infrastructure
7. Documentar ativos explicitamente out-of-scope
8. Classificar ativos por criticidade e sensibilidade
9. Preencher o `asset-inventory-tracker` com dados coletados
10. Registrar inventario no `asset-registry`

## Output
- Asset inventory completo e classificado
- Mapa de ambientes (prod/staging/dev)
- Lista de third-party e shared infrastructure
- Registro no `asset-registry`

## Quality Gates
- [ ] Todos os ativos in-scope identificados e validados
- [ ] Ownership confirmado para cada ativo
- [ ] Ambientes claramente diferenciados (prod vs staging vs dev)
- [ ] Third-party systems listados com autorizacao separada
- [ ] Classificacao de criticidade atribuida a cada ativo
- [ ] Out-of-scope items explicitamente documentados
- [ ] Checklist `asset-inventory-quality` 100% atendido

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | discovery-layer |
| Checklists | asset-inventory-quality |
| Templates | trackers/asset-inventory-tracker |
| Registry | data/registries/asset-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: setup-comms-and-escalation
- **Delivers to**: risk-context-gathering
