# Task: Create New Agent

## Objetivo
Criar um novo agent especializado para o Cybersecurity Squad, definindo identidade, autoridade, principios, playbooks e integracao com o ecosystem do squad.

## Agents
- **cyber-chief** (lead) — Define necessidade e supervisiona criacao

## Inputs
- Gap identificado no squad que justifica novo agent
- Referencia de especialista real ou arquetipo
- Config.yaml com routing atual
- Templates de agent existentes como referencia

## Steps
1. Identificar gap especifico que o novo agent deve cobrir
2. Selecionar especialista de referencia (autor, praticante, arquetipo)
3. Pesquisar obra, metodologia e principios do especialista
4. Definir identidade, tese central e principios operacionais
5. Elaborar heuristicas de decisao e anti-patterns
6. Criar playbooks padrao para as tasks do agent
7. Definir checklists de revisao especificos
8. Escrever system prompt de ativacao
9. Integrar agent no config.yaml (routing de tasks)
10. Registrar decisao no `decisions-log`

## Output
- Arquivo de agent (.md) completo e revisado
- Config.yaml atualizado com routing do novo agent
- Checklists especificos do agent criados
- Registro no `decisions-log`

## Quality Gates
- [ ] Gap claramente identificado e justificado
- [ ] Especialista de referencia coerente com o gap
- [ ] Identidade e principios consistentes e distintos
- [ ] Playbooks cobrem as tasks atribuidas
- [ ] System prompt testado e funcional
- [ ] Routing integrado no config.yaml
