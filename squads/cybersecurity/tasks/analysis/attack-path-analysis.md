# Task: Attack Path Analysis

## Objetivo
Analisar e priorizar attack paths identificados durante assessments, mapeando caminhos de comprometimento completos do initial access ao objetivo final do adversario.

## Agents
- **peter-kim** (lead) — Analisa e prioriza attack paths
- **rogue** (support) — Contribui com perspectiva adversaria
- **cartographer** (support) — Fornece dados de mapeamento

## Inputs
- Findings de Red Team e vulnerability assessments
- Identity e privilege mapping
- Network segmentation map
- MITRE ATT&CK matrix

## Steps
1. Consolidar todos os findings que compoem attack paths
2. Mapear caminhos completos do initial access ao objective
3. Identificar choke points onde controles podem interromper o path
4. Classificar attack paths por probabilidade e impacto
5. Mapear cada path contra MITRE ATT&CK kill chain
6. Identificar paths que byppassam controles existentes
7. Avaliar blast radius de cada path se explorado
8. Priorizar paths por risco ao negocio
9. Documentar recomendacoes de mitigacao por choke point
10. Registrar no `findings-registry`

## Output
- Mapa de attack paths priorizados por risco
- Choke points identificados com recomendacoes de controle
- Mapeamento ATT&CK por attack path
- Recomendacoes de mitigacao estrategica

## Quality Gates
- [ ] Attack paths mapeados end-to-end (initial access ao objetivo)
- [ ] Choke points identificados em cada path
- [ ] Paths classificados por probabilidade e impacto
- [ ] Mapeamento ATT&CK completo por path
- [ ] Recomendacoes focam em choke points de maior valor
- [ ] Checklist `kim-attack-path-prioritization` atendido
- [ ] Checklist `redteam-attack-chain-review` validado
