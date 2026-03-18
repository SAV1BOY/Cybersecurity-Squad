# Task: Multi-Cloud Security Review

## Objetivo
Avaliar a postura de seguranca em ambientes multi-cloud, identificando inconsistencias de controles, gaps de visibilidade e riscos especificos de cada cloud provider.

## Agents
- **omar-santos** (lead) — Conduz review multi-cloud
- **cartographer** (support) — Mapeia ativos cross-cloud

## Inputs
- Inventario de ativos por cloud provider
- Politicas de seguranca por provider
- IAM configurations cross-cloud
- Container e serverless deployments

## Steps
1. Inventariar workloads por cloud provider (AWS, Azure, GCP)
2. Comparar controles de seguranca entre providers
3. Identificar inconsistencias de politicas e configuracao
4. Auditar identity federation e cross-cloud access
5. Revisar seguranca de containers (EKS, AKS, GKE)
6. Avaliar seguranca de serverless functions (Lambda, Functions, Cloud Functions)
7. Verificar data residency e compliance por regiao
8. Mapear shared responsibility boundaries por provider
9. Documentar gaps e recomendacoes de normalizacao
10. Registrar findings no `findings-registry`

## Output
- Relatorio comparativo de seguranca multi-cloud
- Lista de inconsistencias entre providers
- Findings de container e serverless security
- Recomendacoes de normalizacao cross-cloud

## Quality Gates
- [ ] Todos os cloud providers in-scope cobertos
- [ ] Controles comparados consistentemente entre providers
- [ ] Identity federation e cross-cloud access auditados
- [ ] Container e serverless security avaliados
- [ ] Data residency validado contra requisitos
- [ ] Checklist `cloud-security-assessment-quality` atendido
- [ ] Checklist `cloud-serverless-container-security` validado

## Routing & Escalation
- **frameworks**: cloudsec-layer, cloud-identity-attack-defense
- **checklists**: cloud-security-assessment-quality, cloud/cloud-serverless-container-security
- **templates**: reports/technical-report-template
- **registry**: data/registries/findings-registry
- **receives_from**: discovery phase
- **delivers_to**: findings-review
