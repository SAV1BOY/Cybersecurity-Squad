# Task: Containment Actions

## Objetivo
Executar acoes de contencao para limitar o impacto do incidente, impedindo a propagacao da ameaca enquanto preserva evidencias para investigacao.

## Agents
- **omar-santos** (lead) — Coordena acoes de contencao
- **chris-sanders** (support) — Garante preservacao de evidencias
- **cyber-chief** (support) — Autoriza acoes de alto impacto

## Inputs
- Registro de incidente com severidade classificada
- Ativos afetados identificados na triagem
- Playbooks de contencao existentes
- Escalation matrix e autorizacoes

## Steps
1. Avaliar opcoes de contencao (short-term e long-term)
2. Obter autorizacao para acoes de contencao de alto impacto
3. Executar contencao short-term (isolamento de rede, block de IP/hash)
4. Preservar evidencias ANTES de qualquer acao destrutiva
5. Documentar cada acao de contencao com timestamp
6. Verificar eficacia da contencao (ameaca contida?)
7. Implementar contencao long-term se necessario
8. Monitorar ativos contidos para reinfeccao ou bypass
9. Comunicar status de contencao aos stakeholders
10. Registrar acoes no `incident-registry`

## Output
- Log de acoes de contencao com timestamps
- Confirmacao de eficacia da contencao
- Evidencias preservadas antes de acoes destrutivas
- Comunicacao de status aos stakeholders

## Quality Gates
- [ ] Evidencias preservadas ANTES de acoes de contencao
- [ ] Cada acao documentada com timestamp e responsavel
- [ ] Autorizacao obtida para acoes de alto impacto
- [ ] Eficacia da contencao verificada
- [ ] Stakeholders comunicados sobre status
- [ ] Checklist `ir-containment-checklist` atendido
- [ ] Checklist `sanders-evidence-integrity` validado
