# Escalation Procedures

Procedimentos de escalation claros para garantir resposta rapida e adequada.

## Matriz de Escalation por Severidade

| Severidade | Notificacao Inicial | Escalation (30 min) | Escalation (2h) |
|-----------|--------------------|--------------------|-----------------|
| Critical  | SOC Lead + CISO    | VP Engineering + Legal | CEO + Board |
| High      | SOC Lead           | Security Manager   | CISO            |
| Medium    | Analista Senior    | SOC Lead           | Security Manager|
| Low       | Ticket no backlog  | Analista Senior    | SOC Lead        |

## Criterios de Escalation

**Escalar imediatamente para CISO quando:**
- Dados pessoais (LGPD) confirmados como comprometidos
- Sistemas de producao indisponiveis por mais de 30 minutos
- Evidencia de APT ou nation-state actor
- Cobertura de midia sobre o incidente
- Ransomware confirmado em qualquer sistema

**Escalar para Legal quando:**
- Breach de dados pessoais confirmado
- Necessidade de notificacao regulatoria (ANPD, BACEN)
- Ameaca de extorsao ou ransom
- Envolvimento de law enforcement necessario

## Canais de Comunicacao

- **P1 (Critical):** Telefone direto + War room dedicado
- **P2 (High):** Slack channel #incident-response + bridge call
- **P3 (Medium):** Slack channel #security-alerts
- **P4 (Low):** Jira ticket com SLA tracking

## Regras de Ouro

- Na duvida, escale. Melhor sobre-comunicar do que sub-comunicar
- Nunca escalar sem contexto: inclua summary, impacto e acoes tomadas
- Manter registro de todas as comunicacoes de escalation
- Testar arvore de escalation trimestralmente
