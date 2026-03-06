# Incident Response Runbook Quality Gate

Checklist de qualidade para runbooks de resposta a incidentes.

## Estrutura do Runbook
- [ ] Titulo claro identificando o tipo de incidente coberto
- [ ] Objetivo e scope do runbook definidos
- [ ] Prerequisitos listados (acessos, tools, permissoes)
- [ ] Roles e responsabilidades definidos (IC, comms lead, tech lead)
- [ ] Versao e data da ultima revisao registradas
- [ ] Aprovacao por incident response manager documentada

## Fase de Deteccao e Triagem
- [ ] Detection sources listadas para o tipo de incidente
- [ ] Criterios de triagem para true/false positive definidos
- [ ] Severity classification criteria especificos para o cenario
- [ ] Initial data collection steps documentados
- [ ] Escalation criteria e paths definidos
- [ ] Communication templates preparados para cada severity

## Fase de Containment
- [ ] Short-term containment steps detalhados passo-a-passo
- [ ] Long-term containment strategy documentada
- [ ] Decision trees para diferentes cenarios de containment
- [ ] Evidence preservation steps antes de containment actions
- [ ] Rollback procedures para containment actions
- [ ] Impact assessment do containment em operacoes de negocio

## Fase de Eradication
- [ ] Root cause identification steps documentados
- [ ] Malware removal procedures (se aplicavel)
- [ ] Compromised credential reset procedures
- [ ] Vulnerability patching steps
- [ ] Configuration changes necessarios documentados
- [ ] Verification steps apos eradication

## Fase de Recovery
- [ ] System restoration procedures documentados
- [ ] Data integrity verification steps
- [ ] Service validation tests antes de retorno a producao
- [ ] Monitoring enhancements para detectar recorrencia
- [ ] Gradual service restoration plan
- [ ] User communication templates para retorno ao normal

## Post-Incident
- [ ] Post-mortem template referenciado
- [ ] Lessons learned collection process definido
- [ ] Runbook update triggers identificados
- [ ] Metricas de resposta a coletar definidas
- [ ] Regulatory reporting checklist referenciado
- [ ] Runbook testado em tabletop exercise pelo menos anualmente
