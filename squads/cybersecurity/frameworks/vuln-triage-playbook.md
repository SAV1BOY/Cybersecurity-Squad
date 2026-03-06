# Vulnerability Triage Playbook — Framework Interno

> Como triar vulnerabilidades: severidade real, contexto, exploracao e priorizacao.

## Principio Central

Vulnerability triage nao e CVSS cego. E a combinacao de: severidade tecnica + contexto do ambiente + evidencia de exploracao real + impacto ao negocio. Uma vuln CVSS 9.8 em um sistema air-gapped e menos urgente que uma CVSS 6.5 em um endpoint internet-facing com dados de pagamento.

## Processo de Triage

### 1. Classificacao Inicial (< 2 min por vuln)
```
Perguntas rapidas:
1. E exploravel remotamente? (network vs. local)
2. Existe exploit publico? (exploit-db, PoC no GitHub)
3. Esta sendo explorada in-the-wild? (CISA KEV, threat intel)
4. O sistema e internet-facing?
5. O sistema processa dados sensiveis?
```

### 2. Contextualizacao (< 5 min)
```
Adicionar contexto:
1. Asset criticality (da asset-registry)
2. Network exposure (external/internal/segmented)
3. Compensating controls (WAF, EDR, network segmentation)
4. Data classification (PII, financeiro, publico)
5. Business function (core/support/test)
```

### 3. Priorizacao
```
Prioridade = Severidade Tecnica x Contexto

P1 — Imediato (< 72h):
- Exploit publico + internet-facing + dados sensiveis
- In-the-wild exploitation
- RCE sem autenticacao em sistema exposto

P2 — Urgente (< 2 semanas):
- Exploit publico + interno + dados sensiveis
- Privilege escalation em sistema critico
- Auth bypass

P3 — Planejado (< 30 dias):
- Vulnerabilidade sem exploit publico mas com impacto
- Misconfiguration com risco moderado
- Vuln em sistema interno nao-critico

P4 — Backlog (< 90 dias):
- Risco baixo
- Compensating controls efetivos
- Sistema em decommissioning

P5 — Accept/Defer:
- Risco minimo
- Custo de fix > risco
- Documentar no exception-registry
```

### 4. Routing
```
Apos priorizar:
1. Criar ticket com finding padronizado
2. Atribuir ao owner do asset
3. Definir SLA baseado na prioridade
4. Incluir recomendacao de correcao e referencia
5. Registrar no findings-registry e remediation-registry
```

## Fontes de Intel para Triage

- **CISA KEV**: Known Exploited Vulnerabilities (obrigatorio checar)
- **EPSS**: Exploit Prediction Scoring System (probabilidade de exploit)
- **Vendor advisories**: Patches e workarounds
- **Threat intel feeds**: Ameacas ativas no setor
- **Internal telemetry**: Tentativas de exploracao observadas

## Anti-Patterns de Triage

- **CVSS cego**: Nao usar CVSS sozinho, sempre adicionar contexto
- **Tudo e critico**: Se tudo e P1, nada e P1 — priorizar de verdade
- **Ignorar contexto**: CVSS 4.0 em internet-facing > CVSS 9.8 air-gapped
- **Vulnerability fatigue**: Se o backlog cresce sem parar, o triage esta errado
- **Fix without verify**: Correcao sem reteste nao conta como corrigido
