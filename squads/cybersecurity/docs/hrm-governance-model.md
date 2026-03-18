# HRM Governance Model — Cybersecurity Squad

> Modelo de governanca hierarquico do Cybersecurity Squad baseado no padrao HRM (Hierarchical Resource Management).
> Define camadas de autoridade, composicao de domain teams, fluxo de escalacao e limites de atuacao de cada layer.

## 1. Visao Geral

O modelo HRM organiza o squad em camadas (layers) com responsabilidades e autoridades claramente delimitadas. Cada camada tem autonomia para operar dentro do seu escopo definido, mas deve escalar decisoes que ultrapassem seus limites. O objetivo e garantir execucao agil sem perder controle e rastreabilidade.

---

## 2. Layer 1 — Individual Agents

Agentes individuais sao a unidade de execucao do squad. Cada agente opera dentro do escopo definido em seu arquivo de configuracao em [`agents/`](../agents/).

**Responsabilidades**:
- Executar tasks dentro do escopo declarado no respectivo `agents/*.md`
- Seguir os frameworks e checklists designados no [`config.yaml`](../config.yaml) routing
- Produzir outputs utilizando os templates padrao do squad
- Registrar resultados nos registries apropriados em [`data/registries/`](../data/registries/)

**Limites**:
- NAO pode operar fora do escopo declarado em seu arquivo de agente
- NAO pode aprovar seus proprios outputs (self-review proibido)
- NAO pode alterar configuracoes do squad (config.yaml, ARCHITECTURE.md)
- NAO pode iniciar operacoes de alto risco sem aprovacao do domain lead ou cyber-chief

---

## 3. Layer 2 — Domain Teams

Cada domain team agrupa agentes por area de especialidade. O domain lead coordena o trabalho do time e serve como primeiro nivel de escalacao.

| Domain Team | Lead | Members | Escopo |
|-------------|------|---------|--------|
| **Red Team** | [`peter-kim`](../agents/peter-kim.md) | [`georgia-weidman`](../agents/georgia-weidman.md), [`rogue`](../agents/rogue.md), [`ripper`](../agents/ripper.md), [`fuzzer`](../agents/fuzzer.md) | Offensive security, vulnerability validation, exploitation simulation |
| **Blue Team** | [`chris-sanders`](../agents/chris-sanders.md) | [`omar-santos`](../agents/omar-santos.md), [`shannon-runner`](../agents/shannon-runner.md) | Detection, monitoring, threat hunting, SOC operations |
| **AppSec** | [`jim-manico`](../agents/jim-manico.md) | [`fuzzer`](../agents/fuzzer.md), [`command-generator`](../agents/command-generator.md) | Application security, SDLC, code review, API security |
| **CloudSec** | [`omar-santos`](../agents/omar-santos.md) | [`cartographer`](../agents/cartographer.md) | Cloud security, IAM, logging, network segmentation |
| **Discovery** | [`cartographer`](../agents/cartographer.md) | [`busterer`](../agents/busterer.md), [`dirber`](../agents/dirber.md) | Asset discovery, attack surface mapping, data flow mapping |
| **Incident Response** | [`chris-sanders`](../agents/chris-sanders.md) | [`omar-santos`](../agents/omar-santos.md), [`shannon-runner`](../agents/shannon-runner.md), [`marcus-carey`](../agents/marcus-carey.md) | Incident triage, containment, forensics, postmortem |
| **Governance** | [`cyber-chief`](../agents/cyber-chief.md) | [`marcus-carey`](../agents/marcus-carey.md) | Risk management, compliance, metrics, cross-squad coordination |

> Composicao extraida de [`config.yaml`](../config.yaml) secao `teams`.

**Autoridade do Domain Lead**:
- PODE: atribuir tasks dentro do domain, supervisionar rework (iteracao 2), validar outputs como reviewer delegado
- PODE: escalar ao cyber-chief quando necessario
- NAO PODE: aprovar excecoes de quality gate, modificar routing do config.yaml, delegar para fora do domain sem aprovacao do cyber-chief

---

## 4. Layer 3 — Cyber Chief (Orchestrator)

O [`cyber-chief`](../agents/cyber-chief.md) e o orquestrador central do squad. Todas as decisoes estrategicas e cross-domain passam por este layer.

**Autoridade completa**:
- Orquestrar tasks entre domain teams usando o delegation protocol (ver [`docs/delegation-protocol.md`](./delegation-protocol.md))
- Aprovar ou rejeitar outputs em final gates
- Redirecionar tasks entre agentes (reassignment)
- Aprovar excecoes documentadas de quality gates
- Coordenar handoffs cross-squad
- Ativar workflows de emergencia (IR, breach response)
- Manter e atualizar scorecards, metricas e risk register

**Limites do Cyber Chief**:
- NAO pode executar tasks tecnicas diretamente (delegacao obrigatoria)
- NAO pode ignorar quality gates sem documentar excecao formal
- NAO pode modificar principios do squad unilateralmente

---

## 5. Layer 4 — Cross-Squad HRM (Future Central Command)

Camada futura de integracao entre squads. Quando implementada, coordenara:

- Resolucao de conflitos de prioridade entre squads
- Alocacao de recursos compartilhados
- Metricas organizacionais consolidadas
- Governanca unificada de risk registers

Atualmente, a coordenacao cross-squad e feita pelo `cyber-chief` com suporte de [`marcus-carey`](../agents/marcus-carey.md) conforme definido em `config.yaml > cross_squad`.

---

## 6. Matriz de Autoridade por Layer

| Acao | Layer 1 (Agent) | Layer 2 (Domain Lead) | Layer 3 (Cyber Chief) | Layer 4 (Cross-Squad) |
|------|:---:|:---:|:---:|:---:|
| Executar task dentro do escopo | SIM | SIM | NAO (delega) | NAO |
| Revisar output de outro agente | NAO | SIM (dentro do domain) | SIM (qualquer) | SIM |
| Aprovar quality gate | NAO | SIM (domain gate) | SIM (qualquer gate) | SIM |
| Aprovar excecao de gate | NAO | NAO | SIM | SIM |
| Reassign task | NAO | SIM (dentro do domain) | SIM (qualquer) | SIM |
| Handoff cross-squad | NAO | NAO | SIM | SIM |
| Modificar config.yaml | NAO | NAO | SIM | SIM |
| Ativar IR workflow | NAO | SIM (domain lead IR) | SIM | SIM |
| Escalar | SIM (para domain lead) | SIM (para cyber-chief) | SIM (para Layer 4) | N/A |

---

## 7. Fluxo de Escalacao

```
Agent (Layer 1)
    |
    | Problema fora do escopo? Score < 80%? Decisao incerta?
    v
Domain Lead (Layer 2)
    |
    | Cross-domain? Excecao necessaria? 3a iteracao rework?
    v
Cyber Chief (Layer 3)
    |
    | Conflito cross-squad? Decisao organizacional?
    v
Cross-Squad HRM (Layer 4 — futuro)
```

**Regras de escalacao**:
- Escalacao deve incluir: contexto completo, tentativas ja realizadas, opcoes propostas
- Tempo maximo para resposta de escalacao: 4h (Layer 2), 8h (Layer 3)
- Toda escalacao e registrada em [`data/registries/decisions-log.md`](../data/registries/decisions-log.md)
- Detalhes completos em [`config.yaml`](../config.yaml) secao `escalation_rules`

---

## Referencias Cruzadas

- [`agents/*.md`](../agents/) — definicao de escopo e capacidades de cada agente
- [`config.yaml`](../config.yaml) — secao `teams`, `delegation_rules`, `escalation_rules`
- [`ARCHITECTURE.md`](../ARCHITECTURE.md) — secao 11 (HRM Cascade Model)
- [`docs/delegation-protocol.md`](./delegation-protocol.md) — protocolo de delegacao
- [`docs/quality-gate-system.md`](./quality-gate-system.md) — sistema de quality gates

---

*Cybersecurity Squad — HRM Governance Model v1.0.0*
