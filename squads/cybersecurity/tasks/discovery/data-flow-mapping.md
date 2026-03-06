# Task: Data Flow Mapping

## Objetivo
Mapear fluxos de dados entre sistemas, identificando onde dados sensiveis trafegam, sao armazenados e processados, para informar threat modeling e compliance.

## Agents
- **cartographer** (lead) — Mapeia fluxos de dados
- **jim-manico** (support) — Valida aspectos de AppSec nos fluxos

## Inputs
- Asset inventory e arquitetura de sistemas
- Classificacao de dados da organizacao
- Threat model preliminar
- Requisitos regulatorios (LGPD, PCI-DSS)

## Steps
1. Identificar tipos de dados sensiveis processados (PII, PCI, PHI, secrets)
2. Mapear origens e destinos de cada tipo de dado
3. Documentar protocolos de transporte e criptografia em transito
4. Identificar pontos de armazenamento e criptografia at rest
5. Mapear integrações com terceiros que recebem ou enviam dados
6. Identificar data flows que cruzam trust boundaries
7. Avaliar controles de acesso em cada ponto do fluxo
8. Detectar data leakage paths potenciais
9. Documentar diagramas de data flow (DFD)
10. Registrar no `asset-registry`

## Output
- Diagramas de data flow (DFD) por sistema
- Mapa de dados sensiveis com classificacao e localizacao
- Lista de data leakage paths potenciais
- Gap analysis de controles por trust boundary

## Quality Gates
- [ ] Todos os tipos de dados sensiveis identificados e classificados
- [ ] Fluxos de dados mapeados com origens e destinos
- [ ] Criptografia em transito e at rest documentada
- [ ] Integracoes com terceiros mapeadas com controles
- [ ] Trust boundaries claramente definidos nos DFDs
- [ ] Data leakage paths identificados e documentados
- [ ] Checklist `threat-model-quality` validado
