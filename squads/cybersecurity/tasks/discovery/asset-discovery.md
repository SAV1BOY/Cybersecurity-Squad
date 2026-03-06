# Task: Asset Discovery

## Objetivo
Descobrir ativos digitais dentro do escopo autorizado que podem nao estar documentados no inventario, incluindo shadow IT, servicos esquecidos e infraestrutura exposta.

## Agents
- **cartographer** (lead) — Executa discovery e mapeamento
- **cyber-chief** (support) — Valida escopo e prioriza

## Inputs
- Asset inventory do intake (asset-scoping)
- ROE com scope boundaries aprovados
- IP ranges e dominios autorizados

## Steps
1. Executar passive DNS enumeration nos dominios autorizados
2. Consultar certificate transparency logs para subdominios
3. Realizar port scanning nos ranges autorizados (top 1000 inicialmente)
4. Identificar servicos e versoes expostas via service fingerprinting
5. Descobrir aplicacoes web e APIs nao documentadas
6. Mapear cloud assets (S3 buckets, Azure blobs, GCP storage)
7. Comparar ativos descobertos com inventario existente
8. Classificar novos ativos por risco de exposicao
9. Atualizar o `asset-inventory-tracker` com descobertas
10. Registrar no `asset-registry`

## Output
- Lista de ativos descobertos nao documentados (shadow IT)
- Inventario atualizado com servicos e versoes
- Mapa de exposicao por ativo
- Registro atualizado no `asset-registry`

## Quality Gates
- [ ] Discovery limitado ao scope autorizado no ROE
- [ ] Todos os ativos descobertos validados quanto a ownership
- [ ] Shadow IT identificado e reportado aos stakeholders
- [ ] Servicos e versoes fingerprinted com precisao
- [ ] Cloud assets verificados (buckets, blobs, storage)
- [ ] Inventario atualizado com delta entre esperado e descoberto
- [ ] Checklist `asset-inventory-quality` 100% atendido
