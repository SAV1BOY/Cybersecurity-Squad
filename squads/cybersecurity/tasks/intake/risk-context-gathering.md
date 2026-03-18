# Task: Risk Context Gathering

## Objetivo
Coletar e documentar o contexto de risco do negocio para informar a priorizacao de atividades de seguranca e a classificacao de findings.

## Agents
- **cyber-chief** (lead) — Coordena coleta de contexto de risco

## Inputs
- Informacoes de negocio do cliente
- Regulamentacoes aplicaveis (LGPD, PCI-DSS, SOC2, HIPAA)
- Historico de incidentes anteriores (se disponivel)
- Threat intelligence relevante ao setor

## Steps
1. Identificar vertical de negocio e regulamentacoes aplicaveis
2. Mapear crown jewels (dados e sistemas mais criticos)
3. Coletar historico de incidentes e vulnerabilidades anteriores
4. Identificar threat actors relevantes ao setor (APTs, cybercrime)
5. Documentar risk appetite e risk tolerance da organizacao
6. Mapear controles de seguranca existentes
7. Identificar gaps conhecidos e iniciativas de seguranca em andamento
8. Quantificar impacto potencial usando FAIR ou modelo equivalente
9. Preencher o `security-assessment-brief` com contexto de risco
10. Registrar informacoes no `risk-register`

## Output
- Documento de risk context com crown jewels mapeados
- Lista de regulamentacoes e compliance requirements
- Threat actor profile relevante ao setor
- Registro no `risk-register`

## Quality Gates
- [ ] Crown jewels identificados e priorizados
- [ ] Regulamentacoes aplicaveis listadas e mapeadas
- [ ] Risk appetite e tolerance documentados
- [ ] Threat actors relevantes identificados com base em threat intelligence
- [ ] Controles existentes mapeados contra gaps conhecidos
- [ ] Impacto potencial quantificado ou estimado
- [ ] Checklist `scope-and-roe-quality` validado para contexto de risco

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | fair-risk-quantification, governance-layer |
| Checklists | scope-and-roe-quality |
| Templates | briefs/security-assessment-brief |
| Registry | data/registries/risk-register |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: asset-scoping
- **Delivers to**: discovery tasks
