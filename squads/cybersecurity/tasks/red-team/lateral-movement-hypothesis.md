# Task: Lateral Movement Hypothesis

## Objetivo
Identificar e documentar caminhos de movimentacao lateral possiveis a partir de acessos obtidos, mapeando como um atacante poderia expandir seu foothold na rede.

## Agents
- **rogue** (lead) — Simula adversary lateral movement
- **peter-kim** (support) — Valida attack paths e prioriza

## Inputs
- Acessos obtidos na fase de exploitation
- Network map e segmentacao
- Identity e privilege mapping
- MITRE ATT&CK Lateral Movement techniques

## Steps
1. Mapear credenciais e tokens obtidos durante exploitation
2. Identificar sistemas alcancaveis a partir do foothold atual
3. Enumerar protocolos de lateral movement disponiveis (PtH, RDP, WMI, SSH)
4. Testar pivoting entre segmentos de rede (se autorizado)
5. Identificar shared credentials e credential reuse
6. Mapear trust relationships entre dominios e forests
7. Documentar cada lateral movement path como hipotese
8. Avaliar viabilidade e impacto de cada path
9. Mapear contra MITRE ATT&CK Lateral Movement tactics
10. Registrar findings no `findings-registry`

## Output
- Mapa de lateral movement paths possiveis
- Hipoteses documentadas com viabilidade e impacto
- Mapeamento ATT&CK Lateral Movement por path
- Recomendacoes de segmentacao e controle

## Quality Gates
- [ ] Lateral movement limitado ao autorizado no ROE
- [ ] Paths documentados como hipoteses com evidencia
- [ ] Credenciais obtidas tratadas com seguranca (nao expostas)
- [ ] Pivoting entre segmentos apenas se autorizado
- [ ] Mapeamento ATT&CK completo para cada path
- [ ] Checklist `redteam-attack-chain-review` atendido
- [ ] Checklist `kim-network-pivoting-audit` validado

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | lateral-movement-methodology, mitre-att-ck |
| Checklists | red-team/redteam-attack-chain-review, kim/kim-network-pivoting-audit |
| Templates | reports/finding-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: safe-exploitation-simulation
- **Delivers to**: report-findings
