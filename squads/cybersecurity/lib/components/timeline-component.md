# Timeline Component

Componente para construcao de timelines em incidentes e investigacoes de seguranca.

## Estrutura

```
## Incident Timeline: [INC-ID]

| Timestamp (UTC) | Source | Event | Actor | Impact | Notes |
|-----------------|--------|-------|-------|--------|-------|
| 2026-01-15 02:14 | EDR | Malicious process detected | - | Endpoint compromised | Hash: abc123 |
| 2026-01-15 02:15 | SIEM | Alert triggered | SOC Analyst | - | Alert ID: ALT-4521 |
| 2026-01-15 02:18 | SOC | Alert acknowledged | @analyst-01 | - | Severity: High |
| 2026-01-15 02:25 | SOC | Investigation started | @analyst-01 | - | Scope assessment |
| 2026-01-15 02:40 | IR | Containment initiated | @ir-lead | Host isolated | Network quarantine |
| 2026-01-15 03:00 | IR | Incident declared | @ir-lead | IR process activated | Sev: Critical |
```

## Fontes de Dados para Timeline

- **SIEM**: Logs correlacionados e alertas
- **EDR**: Eventos de endpoint e process trees
- **Firewall/IDS**: Conexoes de rede e alertas
- **Cloud Logs**: CloudTrail, Azure Activity Log
- **Application Logs**: Access logs, error logs
- **Email**: Headers e metadata de phishing

## Boas Praticas

- Usar sempre UTC para evitar confusao de timezone
- Incluir fonte de cada evento para rastreabilidade
- Marcar claramente eventos confirmados vs estimados
- Separar acoes do atacante de acoes de resposta
- Incluir gaps conhecidos na timeline ("periodo sem visibilidade")

## Visualizacao

Para apresentacoes executivas, converter a tabela em formato visual:
- Linha do tempo horizontal com marcos principais
- Codigo de cores: vermelho (ataque), azul (deteccao), verde (resposta)
- Destacar MTTD e MTTC visualmente

## Uso em Post-Incident Review

A timeline e o artefato central da post-incident review. Deve ser
revisada com todo o time para identificar gaps de deteccao,
oportunidades de automacao e melhorias no processo de resposta.
