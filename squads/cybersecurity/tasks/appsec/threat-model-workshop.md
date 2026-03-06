# Task: Threat Model Workshop

## Objetivo
Facilitar workshops colaborativos de threat modeling com equipes de desenvolvimento e arquitetura, capacitando-os a identificar e mitigar ameacas desde o design.

## Agents
- **jim-manico** (lead) — Facilita workshop e ensina metodologia
- **cyber-chief** (support) — Alinha com estrategia de seguranca

## Inputs
- Arquitetura do sistema a ser modelado
- Data flow diagrams existentes
- Lista de participantes (devs, architects, product owners)
- Threat models anteriores (se disponiveis)

## Steps
1. Preparar materiais do workshop (templates, exemplos, guias)
2. Selecionar metodologia adequada (STRIDE, PASTA, Attack Trees)
3. Apresentar conceitos de threat modeling para participantes
4. Facilitar decomposicao do sistema em componentes e trust boundaries
5. Guiar identificacao de ameacas usando metodologia selecionada
6. Priorizar ameacas colaborativamente por impacto e probabilidade
7. Identificar controles existentes e gaps
8. Definir mitigacoes e atribuir responsaveis
9. Documentar threat model resultante usando template padrao
10. Registrar no `risk-register`

## Output
- Threat model documentado e aprovado pelos participantes
- Lista de ameacas priorizadas com responsaveis definidos
- Plano de mitigacao com timeline
- Registro no `risk-register`

## Quality Gates
- [ ] Participantes incluem devs, architects e product owners
- [ ] Metodologia de threat modeling aplicada consistentemente
- [ ] Trust boundaries e data flows documentados
- [ ] Ameacas priorizadas por impacto e probabilidade
- [ ] Mitigacoes tem responsaveis e timeline definidos
- [ ] Threat model documentado e armazenado
- [ ] Checklist `threat-model-quality` 100% atendido
