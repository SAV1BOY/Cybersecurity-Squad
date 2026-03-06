# Incident Response Project

Template de projeto para gestao de incidentes de seguranca.

## Ativacao

| Campo | Valor |
|-------|-------|
| Incident ID | [INC-YYYY-NNN] |
| Severidade | [Critical / High / Medium / Low] |
| Categoria | [Conforme incident-taxonomy] |
| Incident Commander | [Nome] |
| Ativado em | [Timestamp UTC] |

## Fase 1: Detection & Triage

- [ ] Alerta recebido e triado pelo SOC
- [ ] Severidade inicial definida
- [ ] Incident Commander designado
- [ ] Canal de comunicacao criado (Slack channel / bridge call)
- [ ] Stakeholders notificados conforme matriz de escalacao

## Fase 2: Investigation

- [ ] Escopo do incidente determinado (sistemas afetados)
- [ ] Timeline inicial construida
- [ ] IOCs identificados e documentados
- [ ] Impacto em dados avaliado (pessoais, financeiros)
- [ ] Attack vector identificado
- [ ] Threat actor characterization (se possivel)

## Fase 3: Containment

- [ ] Estrategia de contencao definida (curto e longo prazo)
- [ ] Contencao executada (isolamento, bloqueio, reset)
- [ ] Evidencias preservadas antes de contencao
- [ ] Validacao de que contencao foi efetiva
- [ ] Comunicacao de status para stakeholders

## Fase 4: Eradication

- [ ] Root cause identificada
- [ ] Artefatos maliciosos removidos
- [ ] Vulnerabilidade explorada remediada
- [ ] Credenciais comprometidas rotacionadas
- [ ] Validacao de que eradicacao foi completa

## Fase 5: Recovery

- [ ] Plano de restauracao definido
- [ ] Sistemas restaurados de backups confiáveis
- [ ] Monitoramento aprimorado habilitado
- [ ] Validacao de integridade pos-restauracao
- [ ] Comunicacao de retorno ao normal

## Fase 6: Post-Incident

- [ ] Post-incident review agendada (ate 5 dias uteis)
- [ ] Postmortem blameless documentado
- [ ] Lessons learned registradas
- [ ] Action items definidos com owners e prazos
- [ ] Metricas do incidente calculadas (MTTD, MTTC, MTTR)
- [ ] Comunicacao final para stakeholders

## Comunicacao

Usar templates do communications-snippets para cada tipo de comunicacao.
Updates regulares conforme severidade: Critical (a cada 1h), High (a cada 4h).
