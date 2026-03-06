# Task: Postmortem & Actions

## Objetivo
Conduzir analise postmortem do incidente, extraindo lessons learned e definindo acoes corretivas para prevenir recorrencia e melhorar a postura de seguranca.

## Agents
- **marcus-carey** (lead) — Facilita postmortem blameless
- **cyber-chief** (support) — Prioriza acoes corretivas

## Inputs
- Timeline do incidente completa
- Evidencias coletadas e analise de causa raiz
- Acoes de contencao e recovery executadas
- Metricas do incidente (MTTD, MTTR)

## Steps
1. Preparar timeline consolidada do incidente
2. Conduzir sessao de postmortem blameless com todos os envolvidos
3. Identificar causa raiz e fatores contribuintes
4. Documentar o que funcionou bem e o que precisa melhorar
5. Mapear gaps em processos, tecnologia e pessoas
6. Definir acoes corretivas com responsaveis e deadlines
7. Priorizar acoes por impacto na prevencao de recorrencia
8. Atualizar playbooks e runbooks com lessons learned
9. Comunicar resultados do postmortem aos stakeholders
10. Registrar no `incident-registry` e `lessons-learned-registry`

## Output
- Relatorio de postmortem com timeline e causa raiz
- Lista de acoes corretivas com responsaveis e deadlines
- Playbooks atualizados com lessons learned
- Registro no `lessons-learned-registry`

## Quality Gates
- [ ] Postmortem conduzido de forma blameless
- [ ] Causa raiz identificada e documentada
- [ ] Acoes corretivas tem responsaveis e deadlines
- [ ] Lessons learned incorporados nos playbooks
- [ ] Metricas do incidente registradas (MTTD, MTTR)
- [ ] Checklist `carey-lessons-learned` atendido
- [ ] Checklist `carey-communication-under-pressure` validado
