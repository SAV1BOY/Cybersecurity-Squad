# Delegation Protocol — Cybersecurity Squad

> Protocolo completo de delegacao de tasks dentro do Cybersecurity Squad e para squads externos.
> Define o context packet obrigatorio, arvore de decisao, regras de accountability e anti-patterns a evitar.

## 1. Visao Geral

Delegacao e o mecanismo pelo qual o [`cyber-chief`](../agents/cyber-chief.md) ou um domain lead atribui uma task a um agente executor. Toda delegacao exige um context packet completo e segue o chain definido em [`config.yaml`](../config.yaml) secao `delegation_rules > delegation_chain`:

```
intake:    cyber-chief -> domain_lead -> executor
execution: domain_lead -> specialist_agent
review:    cyber-chief ou domain_lead
handoff:   cyber-chief -> receiving_squad_lead
```

---

## 2. Context Packet — Campos Obrigatorios

Todo context packet deve conter **todos** os campos abaixo. Delegacao sem context packet completo e um anti-pattern e deve ser rejeitada pelo agente receptor.

| Campo | Tipo | Descricao | Exemplo |
|-------|------|-----------|---------|
| `task_id` | string | Identificador unico da task | `RT-2026-042` |
| `scope` | string | Descricao clara do que deve ser feito e limites | "Validar CVE-2025-1234 no servidor web prod-01, sem escalar privilegios" |
| `constraints` | list | Restricoes explicitas (tempo, ferramentas, escopo negativo) | ["Somente scanning passivo", "Sem fuzzing em producao"] |
| `deadline` | datetime | Prazo maximo para entrega | `2026-03-20T18:00:00Z` |
| `risk_level` | enum | Nivel de risco: low / medium / high / critical | `high` |
| `context` | string | Informacoes de background necessarias para execucao | "Servidor ja teve incidente em Jan/2026, ver IR-2026-003" |
| `expected_output` | string | Formato e conteudo esperado do deliverable | "Finding report usando finding-template com evidencias SHA-256" |
| `quality_gate` | list | Checklists que serao aplicados na revisao | ["vuln-assessment-quality", "evidence-chain-quality"] |

> Os checklists aplicaveis podem ser consultados em [`config.yaml`](../config.yaml) secao `routing` para a task correspondente.

---

## 3. Arvore de Decisao de Delegacao

```
Task recebida pelo cyber-chief
  +-- No escopo? NAO --> Rejeitar / escalar Layer 4
  +-- SIM --> Identificar domain (config.yaml routing)
      +-- Agente disponivel? NAO --> Escalar / cross-squad
      +-- SIM --> Agente tem capacidade? NAO --> Alternativo
      +-- SIM --> Risco alto? SIM --> cyber-chief pre-aprova
      +-- Montar context packet --> Delegar --> Registrar decisions-log
```

---

## 4. Regras de Accountability

A delegacao distribui responsabilidade mas **nao transfere accountability**:

| Papel | Responsabilidade | Accountability |
|-------|-----------------|----------------|
| **Delegador** (cyber-chief ou domain lead) | Montar context packet completo, selecionar agente correto, definir deadline | Retida — o delegador responde pelo resultado final |
| **Executor** (agente designado) | Executar dentro do escopo, produzir output com qualidade, cumprir deadline | Qualidade do output e aderencia ao escopo |
| **Reviewer** (cyber-chief ou domain lead) | Avaliar output contra quality gates, fornecer feedback especifico | Validacao e decisao de aprovacao |

**Principio fundamental**: conforme [`config.yaml`](../config.yaml) secao `delegation_rules > principles` — "Delegation does not transfer accountability — cyber-chief remains accountable."

---

## 5. Delegacao Cross-Squad

Quando uma task requer handoff para outro squad (dev, infra, compliance), requisitos adicionais se aplicam conforme `config.yaml > go_no_go > before_cross_squad_handoff`:

### 5.1 Handoff Package (obrigatorio)

O pacote de handoff deve conter:
- **Contexto completo** da task e decisoes tomadas
- **Outputs produzidos** com evidencias e scores dos quality gates passados
- **Requisitos para o squad receptor** com criterios de aceitacao
- **SLA proposto** para conclusao pelo squad receptor
- **Ponto de contato** para duvidas e escalacoes

### 5.2 Fluxo de Handoff

1. `cyber-chief` prepara handoff package
2. Package passa pelo final gate (ver [`docs/quality-gate-system.md`](./quality-gate-system.md))
3. Envio ao squad receptor com solicitacao de ACK
4. Squad receptor confirma recebimento e aceita SLA
5. Registro em `data/handoffs/handoff-tracking`
6. Clock de SLA inicia apos ACK

### 5.3 Handoff Rejeitado

Se o squad receptor rejeitar o handoff:
- Feedback especifico e obrigatorio (itens faltantes, qualidade insuficiente)
- Package retorna ao `cyber-chief` para remediar
- Se nao resolvido apos remediacoes, escalacao conforme `config.yaml > escalation_rules > cross_squad_escalation`

---

## 6. Anti-Patterns de Delegacao

Padroes que devem ser **evitados** e constituem violacoes do protocolo:

| Anti-Pattern | Problema | Correcao |
|-------------|----------|----------|
| **Delegar sem contexto** | Agente nao sabe o que fazer, produz output errado | Sempre incluir context packet completo (secao 2) |
| **Delegar fora do escopo do agente** | Agente nao tem capacidade para a task | Consultar `agents/*.md` secao "Tasks que NAO Executa" |
| **Delegar sem deadline** | Task fica indefinida no backlog, sem urgencia | Sempre definir deadline explicito no context packet |
| **Self-delegation** | Agente delega para si mesmo, perde check de qualidade | Delegacao requer pelo menos 2 partes distintas |
| **Cascade delegation sem accountability** | Cada nivel "passa adiante" sem reter responsabilidade | Delegador original mantem accountability (secao 4) |
| **Delegar alto risco sem pre-aprovacao** | Operacoes de risco executadas sem supervisao | Operacoes high/critical requerem pre-aprovacao do cyber-chief |

---

## 7. Registro de Delegacoes

Toda delegacao e registrada em [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) com:

| Campo | Valor |
|-------|-------|
| `action` | delegation |
| `delegator` | Quem delegou |
| `executor` | Quem recebeu |
| `task_id` | ID da task |
| `context_packet` | Referencia ao context packet |
| `deadline` | Prazo definido |
| `risk_level` | low / medium / high / critical |
| `rationale` | Justificativa da escolha do agente |

---

## Referencias Cruzadas

- [`config.yaml`](../config.yaml) — secao `delegation_rules`, `delegation_chain`, `go_no_go > before_cross_squad_handoff`
- [`agents/cyber-chief.md`](../agents/cyber-chief.md) — papel do orquestrador no delegation flow
- [`ARCHITECTURE.md`](../ARCHITECTURE.md) — secao 16 (Delegation Protocol)
- [`docs/rework-loop-protocol.md`](./rework-loop-protocol.md) — fluxo de rework quando output delegado falha no gate
- [`docs/hrm-governance-model.md`](./hrm-governance-model.md) — modelo de camadas de autoridade
- [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) — registro de todas as delegacoes

---

*Cybersecurity Squad — Delegation Protocol v1.0.0*
