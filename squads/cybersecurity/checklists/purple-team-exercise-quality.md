# Purple Team Exercise Quality Gate

Checklist de qualidade para exercicios de purple team.

## Planejamento
- [ ] Objetivos do exercicio definidos (detection gaps, response improvement)
- [ ] MITRE ATT&CK techniques alvo selecionadas e priorizadas
- [ ] Red team operator e blue team analyst designados
- [ ] Scenario/attack chain planejado com injects
- [ ] Communication channel entre red e blue estabelecido
- [ ] Ferramentas de simulacao preparadas (Atomic Red Team, Caldera)
- [ ] Baseline de deteccoes existentes documentado
- [ ] Success criteria definidos para cada technique testada

## Execucao Colaborativa
- [ ] Cada technique executada com blue team ciente do timing
- [ ] Red team documenta exatamente o que foi executado (commands, tools)
- [ ] Blue team documenta o que foi detectado e como
- [ ] Gap entre execucao e deteccao medido (dwell time)
- [ ] Cada technique testada em multiplas variantes
- [ ] Evasion techniques aplicadas progressivamente
- [ ] Feedback loop em tempo real entre red e blue

## Avaliacao de Deteccao
- [ ] Cada technique classificada: Detected, Partially Detected, Not Detected
- [ ] Detection source identificada (EDR, SIEM, NDR, manual)
- [ ] Alert fidelity avaliada (false positive potential)
- [ ] Time to detect medido para cada technique
- [ ] Data sources necessarias vs disponiveis mapeadas
- [ ] Visibility gaps identificados por ATT&CK tactic

## Avaliacao de Resposta
- [ ] Response actions avaliadas por technique detectada
- [ ] Playbook/runbook acionado corretamente avaliado
- [ ] Containment effectiveness avaliada
- [ ] Escalation paths testados e funcionais
- [ ] Communication procedures avaliadas

## Improvement Actions
- [ ] Novas detection rules criadas para gaps identificados
- [ ] Detection rules existentes tuned para melhor fidelidade
- [ ] Logging gaps endereçados (new data sources)
- [ ] Playbooks atualizados com novos cenarios
- [ ] Training needs identificados para analistas

## Documentacao e Metricas
- [ ] ATT&CK Navigator heatmap atualizado com resultados
- [ ] Detection coverage score calculado (pre vs post)
- [ ] MTTD (Mean Time to Detect) calculado por technique
- [ ] Report com findings e improvements entregue
- [ ] Proximo exercicio agendado com techniques diferentes
- [ ] Resultados compartilhados com management
