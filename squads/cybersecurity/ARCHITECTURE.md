# ARCHITECTURE.md — Cybersecurity Squad

> Mapa de interconexao, fluxo de dados, camadas operacionais e principios do squad.

## 1. Diagrama de Dependencias

```
config.yaml (cerebro de roteamento)
    │
    ├── tasks/ ─────────────────────────────────────────┐
    │   (o que fazer)                                    │
    │                                                    ▼
    ├── agents/ ◄──── frameworks/ ◄──── reference/     checklists/
    │   (quem faz)    (como fazer)      (base intelectual) (quality gates)
    │                                                    │
    │                                                    ▼
    ├── templates/ ◄──── lib/components/               data/registries/
    │   (formato output)  (blocos reutilizaveis)       (onde registrar)
    │                                                    │
    ├── voice/ + phrases/                                ▼
    │   (como comunicar)                              data/metrics/
    │                                                (o que medir)
    └── workflows/
        (fluxo ponta-a-ponta)
```

## 2. Fluxo Principal

```
INTAKE ──► DISCOVERY ──► EXECUTION ──► REPORT ──► REMEDIATION ──► RETEST ──► METRICS ──► IMPROVEMENT
  │            │              │            │            │              │          │            │
  ▼            ▼              ▼            ▼            ▼              ▼          ▼            ▼
 ROE        Assets        Red/Blue/    Findings     Fix Plan       Verify    KPIs/SLA    Feedback
 Scope      Surface       AppSec/      Evidence     Owners         Close     Dashboard   Loop
 Auth       Threats       Cloud/IR     Risk         SLA            Regress   Trends      Iterate
```

## 3. Camadas Operacionais

### Camada 1: Discovery (Descoberta)
- **Objetivo**: Mapear tudo que existe e tudo que pode ser atacado
- **Agentes**: Cartographer, Busterer, Dirber
- **Frameworks**: discovery-layer.md
- **Output**: Inventario de ativos, mapa de superficie, trust boundaries

### Camada 2: Offense (Red Team)
- **Objetivo**: Validar vulnerabilidades e simular ataques reais
- **Agentes**: Peter Kim, Georgia Weidman, Rogue, Ripper, Fuzzer
- **Frameworks**: offense-layer.md, MITRE ATT&CK, Kill Chain
- **Output**: Findings validados com prova de conceito
- **Restricoes**: ROE obrigatorio, stop rules, minima alteracao

### Camada 3: Defense (Blue Team)
- **Objetivo**: Detectar, responder e melhorar continuamente
- **Agentes**: Chris Sanders, Omar Santos, Shannon Runner
- **Frameworks**: defense-layer.md, MITRE D3FEND, detection-coverage-matrix
- **Output**: Regras de deteccao, cobertura ATT&CK, playbooks de resposta

### Camada 4: AppSec
- **Objetivo**: Seguranca no ciclo de desenvolvimento
- **Agentes**: Jim Manico, Fuzzer, Command Generator
- **Frameworks**: appsec-layer.md, OWASP ASVS, SAMM
- **Output**: Code reviews, gates SDLC, threat models

### Camada 5: CloudSec
- **Objetivo**: Seguranca de infraestrutura cloud
- **Agentes**: Omar Santos, Cyber Chief
- **Frameworks**: cloudsec-layer.md, Zero Trust
- **Output**: IAM audits, logging configs, guardrails

### Camada 6: Incident Response
- **Objetivo**: Resposta rapida e estruturada a incidentes
- **Agentes**: Chris Sanders, Omar Santos, Cyber Chief
- **Frameworks**: ir-layer.md, NIST 800-61
- **Output**: Timeline, contencao, RCA, postmortem

### Camada 7: Governance
- **Objetivo**: Risco, compliance util e metricas
- **Agentes**: Cyber Chief, Marcus Carey
- **Frameworks**: governance-layer.md, NIST CSF, FAIR
- **Output**: Risk register, KPIs, quarterly reviews

## 4. Modelo de Routing (config.yaml)

Para cada **task**, o config.yaml define:

```yaml
task-name:
  agents: [quem executa]
  frameworks: [metodologia obrigatoria]
  checklists: [quality gates]
  templates: [formato de output]
  registry: [onde registrar resultado]
```

### Exemplo: `vuln-validation`
```yaml
vuln-validation:
  agents: [georgia-weidman, peter-kim, fuzzer]
  frameworks: [offense-layer, risk-scoring-model]
  checklists: [vuln-assessment-quality, weidman/weidman-exploitation-validation, evidence-chain-quality]
  templates: [reports/finding-template, reports/technical-report-template]
  registry: [data/registries/findings-registry]
```

## 5. Ciclos de Feedback

### Red -> Blue (Purple Team Loop)
```
Red Team finding ──► Blue Team detection gap ──► New detection rule ──► Validate ──► Coverage++
```

### Finding -> Fix -> Verify
```
Finding ──► Remediation plan ──► Dev fix ──► Retest ──► Close/Reopen ──► Metrics
```

### Incident -> Improvement
```
Incident ──► Response ──► Postmortem ──► Actions ──► Detection improvement ──► Tabletop validation
```

## 6. Cross-Squad Integration

### CyberSec -> Dev Squad
- Findings com prioridade e SLA -> backlog de desenvolvimento
- Secure coding guidelines -> reference do dev squad
- SDLC security gates -> workflows do dev squad
- Shared: threat models, security requirements

### CyberSec -> Infra Squad
- Hardening baselines -> standards de infra
- Detection rules -> monitoring de infra
- Cloud guardrails -> policies de infra
- Shared: asset inventory, network diagrams

### CyberSec -> Compliance Squad
- Evidence packages -> evidence vault
- Control mappings -> framework mapping
- Risk register -> risk management
- Shared: audit findings, remediation tracking

## 7. Quality Gates Obrigatorios

### Para TODO output do squad:
1. `scope-and-roe-quality` — Autorizacao e limites verificados
2. `evidence-chain-quality` — Cadeia de custodia e integridade
3. `security-report-quality` — Clareza, prova e acionabilidade

### Por dominio:
- **Red Team**: pentest-execution-quality + redteam-safe-testing-rules
- **AppSec**: code-review-security-quality + manico-ssdlc-gates
- **Blue Team**: detection-engineering-quality + blueteam-detection-coverage
- **IR**: incident-triage-quality + forensics-collection-quality

## 8. OPSEC do Squad

### O que este repositorio NUNCA contem:
- Credenciais, tokens, API keys ou segredos reais
- Exploits funcionais ou payloads armados
- Dados de clientes ou sistemas em producao
- Resultados nao-sanitizados de engajamentos reais
- Wordlists ofensivas nao-curadas

### Principios de OPSEC:
- Todo conteudo e sanitizado e orientado a referencia
- Exemplos usam dados ficticios e IPs RFC 5737 (192.0.2.0/24)
- Hashes de evidencia usam SHA-256
- Comunicacao de incidentes segue templates padronizados
- Acesso ao repositorio e controlado por papeis

## 9. Metricas e KPIs

| KPI | Descricao | Target |
|-----|-----------|--------|
| MTTD | Mean Time to Detect | < 24h |
| MTTR | Mean Time to Respond | < 4h (critico) |
| Vuln SLA | % corrigidas no prazo | > 90% |
| Detection Coverage | % ATT&CK com deteccao | > 70% |
| FP Rate | Taxa de falsos positivos | < 10% |
| Maturity Score | Score de maturidade (1-5) | > 3.5 |
| Critical Backlog | Vulns criticas abertas | < 5 |

## 10. Evolucao

O squad evolui em 4 packs:

1. **Pack Core**: agents/ + frameworks core + config.yaml + ARCHITECTURE.md
2. **Pack Operacional**: templates/ + checklists/ principais + workflows/
3. **Pack Profundidade**: swipe/ + reference/ + scripts/ + registries
4. **Pack Maturidade**: archive/ + authority/ + phrases/ + lib/ + voice/

---

*Cybersecurity Squad Architecture v1.0.0*
