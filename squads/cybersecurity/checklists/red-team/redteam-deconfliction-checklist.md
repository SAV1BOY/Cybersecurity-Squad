# Red Team - Deconfliction Checklist

Checklist para processo de deconfliction entre red team e operacoes.

## Pre-Engagement Setup
- [ ] Trusted agent(s) designados pelo cliente
- [ ] Deconfliction communication channel estabelecido (out-of-band)
- [ ] Red team IPs e infrastructure compartilhados com trusted agent
- [ ] Deconfliction process documentado e acordado
- [ ] Escalation path para emergencias definido
- [ ] Regular check-in schedule definido com trusted agent
- [ ] Code word ou identifier definido para deconfliction requests

## Informacoes Compartilhadas com Trusted Agent
- [ ] Source IPs do red team (para deconfliction, nao para whitelisting)
- [ ] Domains e infrastructure utilizados
- [ ] Timeframes gerais de atividade (sem detalhes de TTPs)
- [ ] Emergency contact numbers dos operadores
- [ ] General objectives (sem revelar attack paths especificos)
- [ ] Tipos de atividades planejadas (phishing, exploitation, etc.)

## Durante o Engagement
- [ ] Check-ins regulares realizados conforme schedule
- [ ] Atividades de alto risco notificadas previamente ao trusted agent
- [ ] Qualquer service disruption reportado imediatamente
- [ ] Deconfliction requests do SOC processados via trusted agent
- [ ] Red team activity confirmada ou negada para SOC (via trusted agent)
- [ ] Incidentes reais diferenciados de atividades de red team
- [ ] Log de deconfliction requests mantido

## Resposta a Deteccao
- [ ] Protocolo definido quando blue team detecta red team
- [ ] Decisao de continuar vs parar atividade documentada
- [ ] Trusted agent intermediando sem revelar TTPs ao SOC
- [ ] Blue team response quality observada e documentada
- [ ] Detection details registrados para report final
- [ ] Decisao de revelar ao SOC (se engagement permite) documentada

## Incidentes Reais Durante Engagement
- [ ] Processo para diferenciar real incident de red team activity
- [ ] Red team pausa atividades durante real incident (se necessario)
- [ ] Red team apoia investigacao de real incident (se solicitado)
- [ ] Atividades de red team claramente separadas de real incident
- [ ] Timeline de red team vs real incident documentada
- [ ] Evidencias de red team compartilhadas para exclusao

## Pos-Engagement
- [ ] All red team infrastructure descomissionada
- [ ] Final deconfliction meeting com trusted agent
- [ ] All red team IOCs compartilhados com SOC para cleanup
- [ ] Cleanup confirmado pelo trusted agent
- [ ] Deconfliction log incluido no engagement report
- [ ] Lessons learned de deconfliction documentadas
- [ ] Blue team debrief agendado com red team findings
