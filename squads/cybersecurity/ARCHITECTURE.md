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

## 11. HRM Cascade Model

O squad opera em camadas hierarquicas de autoridade e execucao:

```
Layer 4: HRM Central Command (cross-squad governance — future)
    │
Layer 3: Cyber Chief (squad orchestrator)
    │   - Aprova/veta operacoes de alto risco
    │   - Roteia tasks via config.yaml
    │   - Revisa outputs e aplica quality gates finais
    │   - Coordena handoffs cross-squad
    │   - Mantem audit trail de todas as decisoes
    │
Layer 2: Domain Team Leads (coordenacao tatica)
    │   - Red Team Lead: peter-kim
    │   - Blue Team Lead: chris-sanders
    │   - AppSec Lead: jim-manico
    │   - CloudSec Lead: omar-santos
    │   - Discovery Lead: cartographer
    │   - Governance: marcus-carey
    │   Responsabilidades:
    │   - Coordenam execucao dentro do dominio
    │   - Aplicam quality gates intermediarios
    │   - Escalam para cyber-chief quando necessario
    │
Layer 1: Specialist Agents (execucao)
    - Executam tasks dentro do escopo declarado
    - Seguem frameworks e checklists obrigatorios
    - Produzem outputs em templates padronizados
    - Registram resultados nos registries
    - NUNCA operam fora do escopo sem autorizacao
```

### Escalation Flow
```
Agent detecta problema → Domain Lead avalia → Cyber Chief decide → HRM Central (se cross-squad)
```

### Authority Matrix

| Layer | Pode fazer | NAO pode fazer |
|-------|-----------|----------------|
| Agent | Executar task no escopo, registrar findings | Alterar escopo, aprovar reports, fazer handoff cross-squad |
| Domain Lead | Coordenar equipe, gate intermediario, escalar | Alterar config.yaml, aprovar handoff cross-squad |
| Cyber Chief | Tudo acima + aprovar/vetar, rotear, handoff cross-squad | Executar tasks tecnicas diretamente |

## 12. Decision-Making Protocol

### Principio: Risk-First, Evidence-Based

Toda decisao no squad segue este fluxo:

```
1. Identificar decisao necessaria
2. Classificar risco (baixo/medio/alto/critico)
3. Coletar evidencias e dados relevantes
4. Avaliar opcoes com framework aplicavel
5. Decidir e documentar no decisions-log
6. Comunicar decisao aos afetados
7. Monitorar resultado
```

### Resolucao de Conflitos

| Situacao | Resolucao |
|----------|-----------|
| Dois agentes discordam sobre severidade | Risk scoring model (framework) como arbitro |
| Prioridade conflitante entre tasks | Cyber chief prioriza por impacto ao negocio |
| Seguranca vs velocidade de entrega | fix-over-fear: seguranca prevalece com documentacao |
| Evidencia ambigua | Teste adicional antes de classificar; never assume |

### Ambiguidade

Quando a informacao e insuficiente para decidir:
1. **NAO assuma** — colete mais dados
2. **Documente a incerteza** — registre no decisions-log com confidence level
3. **Escale se necessario** — ambiguidade de alto risco vai ao cyber-chief
4. **Defina threshold** — "se X nao for confirmado em Y horas, assumir Z como default"

## 13. Out-of-Scope Protocol

### Identificacao
O agente verifica se a task esta no seu escopo usando:
- Lista de "Tasks que Executa" no arquivo do agente
- Lista de "Tasks que NAO Executa" no arquivo do agente
- config.yaml routing (task deve ter o agente listado)

### Quando a task esta FORA do escopo:
```
1. Agente identifica que task esta fora do seu escopo
2. Agente NAO executa — documenta razao
3. Agente notifica cyber-chief com:
   - Descricao da task
   - Por que esta fora do escopo
   - Sugestao de agente/squad adequado
4. Cyber-chief decide:
   a. Rotear para outro agente interno → delega com contexto
   b. Handoff cross-squad → inicia handoff protocol
   c. Recusar → documenta razao no decisions-log
```

### Sinais de task fora do escopo:
- Requer skills/tools nao listados no agente
- Envolve dominio de outro squad (ex: legal, financeiro, marketing)
- Requer acesso nao autorizado
- Conflita com principios do squad (ex: exploit ativo, dados reais)

## 14. Memory & Learning Mechanism

### Como outputs viram memoria

```
Task execution → Output gerado → Quality gate avaliado → Registrado em registry
                                                              │
                                                              ▼
                                                    data/registries/*.md
                                                    data/metrics/*.md
                                                    data/scorecards/squad-scorecard.md
```

### Como memoria influencia proximas execucoes

```
Nova task recebida → Agente consulta:
  1. findings-registry (findings similares anteriores?)
  2. lessons-learned-registry (erros a evitar?)
  3. decisions-log (decisoes precedentes relevantes?)
  4. risk-register (riscos conhecidos nesta area?)
  5. improvement-backlog (melhorias pendentes relacionadas?)
```

### Kaizen Loop (Melhoria Continua)

```
Execute → Measure (metrics/) → Analyze (scorecards/) → Improve (backlog/) → Execute
    │                                                        │
    └── postmortem findings ─────────────────────────────────┘
```

**Cadencia do Kaizen:**
- **Diario**: Alert triage atualiza incident-registry
- **Semanal**: Vuln backlog review atualiza findings-registry
- **Mensal**: Metrics review atualiza scorecards e improvement-backlog
- **Trimestral**: Tabletop + risk review gera lessons-learned e risk-register updates
- **Anual**: Strategy review redefine KPI targets e maturity goals

### Traceabilidade
Toda decisao significativa e rastreavel por:
- **decisions-log**: quem decidiu, quando, por que, quais alternativas consideradas
- **findings-registry**: lifecycle completo do finding (descoberta → triagem → remediacao → verificacao)
- **incident-registry**: timeline completa do incidente

## 15. Rework Loop Architecture

```
┌─────────────┐     ┌──────────────┐     ┌──────────────────┐
│ Agent        │────►│ Quality Gate │────►│ Score >= 80%?    │
│ executa task │     │ (checklist)  │     │                  │
└─────────────┘     └──────────────┘     └────────┬─────────┘
                                                   │
                                          ┌────────┼────────┐
                                          │ SIM    │        │ NAO
                                          ▼        │        ▼
                                    ┌───────────┐  │  ┌──────────────┐
                                    │ APROVADO  │  │  │ Iteracao     │
                                    │ → registry│  │  │ <= 3?        │
                                    │ → next    │  │  └──────┬───────┘
                                    └───────────┘  │         │
                                                   │    ┌────┼────┐
                                                   │    │ SIM│    │ NAO
                                                   │    ▼    │    ▼
                                                   │ ┌──────┐│ ┌──────────────┐
                                                   │ │Return││ │ ESCALATE     │
                                                   │ │w/    ││ │ → cyber-chief│
                                                   │ │feed- ││ │ → reassign   │
                                                   │ │back  ││ │   ou approve │
                                                   │ └──┬───┘│ │   c/ excecao │
                                                   │    │    │ └──────────────┘
                                                   │    ▼    │
                                                   │ Agent   │
                                                   │ revisa  │
                                                   │ e resub.│
                                                   └────►────┘
```

**Regras do Rework:**
- Maximo 3 iteracoes antes de escalacao
- Cada iteracao deve ter feedback especifico (nao vago)
- Score < 60% na primeira iteracao → escalacao imediata
- Todas as iteracoes logadas no decisions-log
- Ver detalhes completos em `docs/rework-loop-protocol.md`

## 16. Delegation Protocol

### Requisitos para Delegacao

Toda delegacao do cyber-chief para um agente deve incluir:

| Campo | Obrigatorio | Descricao |
|-------|-------------|-----------|
| Task ID | Sim | Referencia a task no config.yaml |
| Scope | Sim | Limites claros do que fazer e NAO fazer |
| Constraints | Sim | Restricoes tecnicas, temporais e de acesso |
| Deadline | Sim | Prazo para entrega |
| Risk Level | Sim | Baixo/Medio/Alto/Critico |
| Context | Sim | Informacoes necessarias para execucao |
| Expected Output | Sim | O que o agente deve entregar |
| Quality Gate | Sim | Qual checklist aplicar ao output |

### Decision Tree para Delegacao

```
Nova task chega →
  1. E tecnica? → Sim → Qual dominio?
     - Red Team → peter-kim (lead) + especialistas
     - Blue Team → chris-sanders (lead) + especialistas
     - AppSec → jim-manico (lead) + especialistas
     - CloudSec → omar-santos (lead)
     - Discovery → cartographer (lead) + busterer/dirber
     - IR → chris-sanders (lead) + omar-santos
  2. E governance? → Sim → cyber-chief + marcus-carey
  3. E cross-squad? → Sim → cyber-chief inicia handoff protocol
  4. E fora do escopo? → Sim → Recusar ou encaminhar (ver secao 13)
```

### Accountability
- **Delegador** (cyber-chief): Responsavel pelo resultado final
- **Executante** (agente): Responsavel pela execucao com qualidade
- **Reviewer** (cyber-chief ou domain lead): Responsavel pela validacao

Ver detalhes completos em `docs/delegation-protocol.md`.

---

*Cybersecurity Squad Architecture v2.0.0 — MMOS Audit Upgrade*
