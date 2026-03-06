# Blue Team - Tuning Checklist

Checklist para processo de tuning de deteccoes e alertas.

## Identificacao de Necessidade de Tuning
- [ ] Alertas com alta taxa de false positive identificados
- [ ] Alertas nunca disparados nos ultimos 90 dias revisados
- [ ] Feedback de analistas sobre alert quality coletado
- [ ] New environment changes que impactam deteccoes identificados
- [ ] Red team/purple team findings que requerem tuning processados
- [ ] Threat intelligence updates que demandam rule changes aplicados

## Analise Pre-Tuning
- [ ] Baseline de metricas da regra atual documentado (TP rate, FP rate, volume)
- [ ] Root cause dos false positives identificado
- [ ] Sample de alertas analisado (minimo 20 eventos)
- [ ] True positives preservados apos tuning estimados
- [ ] Impacto do tuning na detection coverage avaliado
- [ ] Alternative detection approaches considerados

## Implementacao do Tuning
- [ ] Rule logic ajustada com justificativa documentada
- [ ] Whitelisting entries adicionadas com justificativa
- [ ] Threshold values ajustados com base em dados estatisticos
- [ ] Time window ajustado se necessario
- [ ] Enrichment adicionado para melhor contexto
- [ ] Rule severity ajustada se necessario
- [ ] Change versionada em sistema de controle

## Tipos de Tuning
- [ ] Source-based tuning (whitelist known-good sources)
- [ ] Value-based tuning (exclude specific values/patterns)
- [ ] Threshold tuning (adjust count/frequency)
- [ ] Time-based tuning (adjust detection window)
- [ ] Logic tuning (refine detection logic)
- [ ] Correlation tuning (add/remove correlation conditions)
- [ ] Severity tuning (adjust alert priority)

## Validacao Pos-Tuning
- [ ] Regra testada com known true positive scenario
- [ ] Regra testada para confirmar false positives eliminados
- [ ] Alert volume medido apos tuning e comparado com baseline
- [ ] True positive rate medido apos tuning (nao deve diminuir)
- [ ] False positive rate medido apos tuning (deve diminuir)
- [ ] Monitoring period definido pos-tuning (2 semanas minimo)
- [ ] Rollback realizado se tuning degradou detection quality

## Documentacao e Governance
- [ ] Tuning request documentado com justificativa
- [ ] Approval obtido de detection engineering lead
- [ ] Change log atualizado com detalhes do tuning
- [ ] Knowledge base atualizada com novo pattern
- [ ] Tuning metricas rastreadas (tuning requests/month, impact)
- [ ] Regular tuning review cycle mantido (monthly)
- [ ] Tuning report compartilhado com SOC management
