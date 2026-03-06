# Social Engineering Assessment Quality Gate

Checklist de qualidade para avaliacao de engenharia social.

## Planejamento e Autorizacao
- [ ] Scope de social engineering definido (phishing, vishing, physical)
- [ ] Authorization explicita obtida para cada tecnica
- [ ] Target list aprovada pelo cliente
- [ ] Ethical boundaries documentadas e aceitas
- [ ] Escalation path definido caso alguem reporte o teste
- [ ] Deconfliction plan com HR e Security definido
- [ ] Data handling rules para credenciais capturadas definidas

## Phishing Campaign
- [ ] Pretexto criado de forma realista e contextualizada
- [ ] Domain similar registrado para campanha
- [ ] Email template revisado para verossimilhanca
- [ ] Landing page criada com tracking mecanismo
- [ ] Payload seguro (nao malicioso) preparado
- [ ] SPF/DKIM configurado para domain de envio
- [ ] Campaign tracking configurado (opens, clicks, credentials)
- [ ] Phishing emails enviados em waves conforme planejado

## Vishing (Voice Phishing)
- [ ] Script de vishing preparado e revisado
- [ ] Pretexto adequado ao contexto da organizacao
- [ ] Caller ID spoofing configurado (se autorizado)
- [ ] Gravacao de chamadas autorizada e configurada
- [ ] Criterios de sucesso definidos (info obtida, acesso concedido)
- [ ] Limite de pressao definido para proteger colaboradores

## Physical Social Engineering
- [ ] Pretexto fisico preparado (contractor, delivery, IT support)
- [ ] Props e uniforme preparados se necessario
- [ ] Badge cloning tentado (se autorizado)
- [ ] Tailgating testado em diferentes horarios
- [ ] Baiting (USB drops) executado em areas estrategicas
- [ ] Dumpster diving realizado (se autorizado)

## Coleta e Analise de Resultados
- [ ] Metricas coletadas por campanha (click rate, credential rate)
- [ ] Resultados anonimizados (nao expor individuos)
- [ ] Departamentos/areas com maior vulnerabilidade identificados
- [ ] Comparacao com benchmarks do setor realizada
- [ ] Analise de tendencias vs campanhas anteriores

## Reporting e Awareness
- [ ] Report sem naming-and-shaming de individuos
- [ ] Recommendations de awareness training especificas
- [ ] Technical controls recomendados (email filtering, MFA)
- [ ] Executive summary com metricas claras
- [ ] Awareness session pos-teste planejada
- [ ] Credenciais capturadas destruidas apos report
- [ ] Infraestrutura de phishing descomissionada
