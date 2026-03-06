# Threat Hunt Hypotheses

Hipoteses estruturadas para threat hunting proativo baseado em inteligencia.

## Estrutura de Hipotese

1. **Hipotese** - Afirmacao testavel sobre atividade maliciosa
2. **Motivacao** - Threat intel ou gap de deteccao que originou
3. **Data Sources** - Logs necessarios para investigar
4. **Hunt Query** - Logica de busca inicial
5. **Indicadores de Sucesso** - O que confirma a hipotese
6. **Resultado** - Finding, nova deteccao ou tuning

## Exemplo: C2 Beaconing

**Hipotese:** Existem endpoints realizando beaconing periodico para C2 servers.
**Motivacao:** Campanha de malware ativa no setor reportada pelo CERT.br.
**Data Sources:** Proxy logs, DNS logs, NetFlow.
**Hunt Query:**
```
connections WHERE interval_stddev < 5s
  AND dest_ip NOT IN known_good_list
  AND connection_count > 100 per day
  GROUP BY src_ip, dest_ip
```
**Indicadores:** Intervalos regulares, payload sizes consistentes, destinos nao categorizados.

## Banco de Hipoteses Prioritarias

- Lateral movement via SMB/WMI em horarios nao-comerciais
- Data staging em diretorios temporarios antes de exfiltration
- Credential dumping via LSASS memory access
- DNS tunneling para exfiltracao de dados
- Living-off-the-land binaries (LOLBins) em execucao anomala
- Persistence via scheduled tasks criados recentemente

## Ciclo de Hunt

- Frequencia recomendada: sprints semanais de 2-4 horas
- Documentar todos os hunts, inclusive negativos
- Converter hunts positivos em detection rules automatizadas
- Priorizar hipoteses baseado em threat landscape atual
