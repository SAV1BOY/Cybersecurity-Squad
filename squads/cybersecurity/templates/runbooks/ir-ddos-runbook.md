# IR Runbook — DDoS

> Runbook de resposta a ataques de negacao de servico distribuido (DDoS).
> Foco em mitigacao rapida e restauracao da disponibilidade.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** DDoS (Distributed Denial of Service)
- **Severidade Padrao Inicial:** HIGH
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Indicadores de DDoS

- [ ] Aumento anormal de trafego de rede
- [ ] Latencia elevada ou timeout em servicos
- [ ] Alertas de monitoramento de disponibilidade
- [ ] Saturacao de bandwidth
- [ ] Alto consumo de CPU/memoria em load balancers ou servidores
- [ ] Alertas do CDN ou WAF
- [ ] Reports de usuarios sobre indisponibilidade

### 2.2 Fontes de Alerta

- Monitoramento de infra: [FERRAMENTA_MONITORING]
- CDN / WAF: [CLOUDFLARE / AKAMAI / AWS_SHIELD / OUTRO]
- Network monitoring: [FERRAMENTA_NETFLOW]
- SIEM: [REGRA_SIEM]
- [FONTE_ADICIONAL]

## 3. Triage (Triagem)

- [ ] Confirmar que e DDoS (nao um pico legitimo de trafego)
- [ ] Identificar tipo de ataque:
  - [ ] Volumetrico (UDP flood, amplification)
  - [ ] Protocolo (SYN flood, Ping of Death)
  - [ ] Application layer (HTTP flood, Slowloris)
- [ ] Identificar servicos e endpoints afetados
- [ ] Estimar volume do ataque: [GBPS / RPS]
- [ ] Verificar se e um ataque distracao (smokescreen)
- [ ] Severidade: [CRITICAL / HIGH / MEDIUM]

## 4. Containment e Mitigacao

### 4.1 Acoes Imediatas

- [ ] Ativar DDoS mitigation service: [SERVICO_MITIGACAO]
- [ ] Ativar modo "under attack" no CDN: [PROCEDIMENTO]
- [ ] Habilitar rate limiting agressivo
- [ ] Ativar geo-blocking se ataque de regioes especificas
- [ ] Escalar para ISP se necessario: [CONTATO_ISP]

### 4.2 Mitigacao por Tipo

**Volumetrico:**
- [ ] Ativar scrubbing center: [PROCEDIMENTO]
- [ ] Blackhole routing para IPs de origem (upstream)
- [ ] Aumentar capacidade de bandwidth temporariamente
- [ ] [ACAO_ADICIONAL]

**Application Layer:**
- [ ] Implementar CAPTCHA ou challenge pages
- [ ] Bloquear user agents / patterns maliciosos no WAF
- [ ] Rate limit por IP no application layer
- [ ] Ajustar regras de WAF: [REGRAS_ESPECIFICAS]
- [ ] [ACAO_ADICIONAL]

**Protocolo:**
- [ ] Habilitar SYN cookies
- [ ] Ajustar TCP timeout values
- [ ] Filtrar trafego anomalo no firewall de borda
- [ ] [ACAO_ADICIONAL]

### 4.3 Acoes de Infraestrutura

- [ ] Scale up de recursos (auto-scaling): [PROCEDIMENTO]
- [ ] Ativar failover para regiao secundaria (se disponivel)
- [ ] Desabilitar endpoints nao essenciais temporariamente
- [ ] [ACAO_ADICIONAL]

## 5. Comunicacao

- [ ] Notificar stakeholders sobre degradacao de servico
- [ ] Atualizar status page: [URL_STATUS_PAGE]
- [ ] Comunicar time de suporte ao cliente
- [ ] [COMUNICACAO_ADICIONAL]

## 6. Investigation

- [ ] Coletar logs de trafego durante o ataque
- [ ] Identificar IPs de origem e botnets utilizadas
- [ ] Verificar se houve extorsao (DDoS ransom note)
- [ ] Investigar se DDoS esta cobrindo outro ataque
- [ ] Correlacionar com threat intelligence
- [ ] [INVESTIGACAO_ADICIONAL]

## 7. Recovery (Recuperacao)

- [ ] Monitorar reducao do ataque
- [ ] Reverter gradualmente medidas de mitigacao
- [ ] Restaurar servicos afetados
- [ ] Validar performance e disponibilidade
- [ ] Manter monitoramento elevado por [PERIODO]
- [ ] [ACAO_ADICIONAL]

## 8. Post-Incident

- [ ] Postmortem com metricas do ataque
- [ ] Revisar e melhorar arquitetura de resiliencia
- [ ] Atualizar regras de WAF e rate limiting
- [ ] Considerar DDoS protection permanente se nao existente
- [ ] Realizar DDoS simulation test
- [ ] Atualizar este runbook

## 9. Contatos

| Papel | Contato | Canal |
|-------|---------|-------|
| NOC / SRE | [NOME] | [CANAL] |
| Security Team | [NOME] | [CANAL] |
| CDN / DDoS Provider | [CONTATO_PROVIDER] | [CANAL] |
| ISP | [CONTATO_ISP] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
