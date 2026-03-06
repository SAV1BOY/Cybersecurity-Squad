# Task: Social Engineering Campaign

## Objetivo
Executar campanha de social engineering autorizada para avaliar a resiliencia humana da organizacao contra ataques de phishing, pretexting e outras tecnicas de engenharia social.

## Agents
- **rogue** (lead) — Executa adversary simulation social
- **marcus-carey** (support) — Garante limites eticos e culturais

## Inputs
- ROE com autorizacao explicita para social engineering
- Escopo de alvos (departamentos, cargos, numero de alvos)
- Politicas internas de seguranca e awareness existentes

## Steps
1. Definir objetivo da campanha (credential harvest, payload delivery, pretexting)
2. Desenvolver pretexts e templates de phishing realisticos
3. Configurar infraestrutura de phishing (dominios, landing pages, tracking)
4. Validar que payloads sao seguros e nao destrutivos
5. Executar campanha em waves controladas conforme ROE
6. Monitorar metricas: open rate, click rate, credential submission
7. Documentar interacoes e respostas dos alvos
8. Parar campanha imediatamente se atingir stop-work condition
9. Gerar relatorio com metricas e recomendacoes de awareness
10. Registrar findings no `findings-registry`

## Output
- Relatorio de campanha com metricas agregadas (nao individuais)
- Analise de pontos fracos no security awareness
- Recomendacoes para programa de awareness training
- Evidencias da campanha (sem expor individuos)

## Quality Gates
- [ ] Autorizacao explicita para social engineering no ROE
- [ ] Payloads seguros e nao destrutivos validados
- [ ] Metricas reportadas de forma agregada (sem expor individuos)
- [ ] Stop-work conditions monitoradas durante toda campanha
- [ ] Limites eticos respeitados (sem coercao ou intimidacao)
- [ ] Checklist `social-engineering-assessment-quality` atendido
- [ ] Checklist `carey-ethical-boundaries` validado
