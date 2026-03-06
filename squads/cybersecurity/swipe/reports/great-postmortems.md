# Great Postmortems

Exemplos de postmortems de incidentes que promovem aprendizado sem atribuir culpa.

## Estrutura Blameless Postmortem

1. **Incident Summary** - O que aconteceu em 2-3 frases
2. **Timeline** - Cronologia detalhada com timestamps UTC
3. **Impact** - Usuarios afetados, duracao, dados comprometidos
4. **Root Cause** - Analise tecnica da causa raiz
5. **Contributing Factors** - Fatores que amplificaram o impacto
6. **What Went Well** - O que funcionou na resposta
7. **What Went Wrong** - Gaps identificados no processo
8. **Action Items** - Melhorias com owners e deadlines
9. **Lessons Learned** - Insights para prevencao futura

## Exemplo: Credential Stuffing Incident

> **Summary:** Em 2024-01-15, atacantes realizaram credential stuffing contra /login,
> comprometendo 1.2k contas em 4 horas antes da deteccao.
>
> **Root Cause:** Ausencia de rate limiting no endpoint de autenticacao combinada
> com falta de MFA obrigatorio.
>
> **Detection Gap:** Alertas de failed login existiam mas threshold era 1000/min,
> muito alto para detectar low-and-slow attacks.

## Principios de Qualidade

- Focar em sistemas e processos, nunca em individuos
- Incluir metricas de MTTD, MTTR e MTTC
- Garantir que action items tenham owners definidos
- Revisar postmortem com todos os envolvidos antes de publicar
- Agendar follow-up em 30 dias para verificar action items
- Compartilhar learnings com toda a organizacao
