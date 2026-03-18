# Rework Loop Protocol — Cybersecurity Squad

> Protocolo completo do ciclo de rework do Cybersecurity Squad.
> Define condicoes de trigger, formato de feedback, regras de iteracao, fluxo de escalacao e mecanismos de tracking.

## 1. Visao Geral

O rework loop e ativado quando um output nao atinge o threshold minimo de qualidade. O objetivo e corrigir deficiencias de forma iterativa e controlada, com limites claros de tempo e tentativas. Apos esgotar as iteracoes permitidas, o `cyber-chief` assume a decisao final. Configuracao de referencia em [`config.yaml`](../config.yaml) secao `rework_loop`.

---

## 2. Condicoes de Trigger

O rework loop e iniciado quando **qualquer** das seguintes condicoes e verdadeira:

| Condicao | Threshold | Referencia |
|----------|-----------|------------|
| Quality gate score abaixo do minimo | Score < 80% | `config.yaml > score_thresholds > rework_trigger` |
| Reviewer rejeita output explicitamente | N/A (decisao qualitativa) | `config.yaml > review_loops > per_task_output > fail_action` |
| Evidence chain incompleta | Hash SHA-256 ausente ou inconsistente | [`checklists/evidence-chain-quality.md`](../checklists/evidence-chain-quality.md) |
| Scope violation detectada | Qualquer desvio do escopo autorizado | `config.yaml > escalation_rules > scope_violation` |

**Caso especial — ESCALATION imediata**: se o score for < 60%, o rework loop **nao** e iniciado. Em vez disso, escalacao imediata ao `cyber-chief` conforme `config.yaml > score_thresholds > escalation_trigger`. Ver [`docs/quality-gate-system.md`](./quality-gate-system.md) secao 4.

---

## 3. Formato de Feedback

O feedback de rework **deve** ser especifico e acionavel. Feedback vago ou generico e um anti-pattern (ver [`docs/delegation-protocol.md`](./delegation-protocol.md) secao 6).

### 3.1 Campos Obrigatorios do Feedback

| Campo | Descricao | Exemplo |
|-------|-----------|---------|
| `failed_items` | Lista exata dos itens do checklist que falharam | "Items 3, 7, 12 do pentest-execution-quality" |
| `expected` | O que era esperado para cada item | "Item 3: evidencia com screenshot + hash SHA-256" |
| `actual` | O que foi encontrado | "Item 3: apenas descricao textual, sem screenshot" |
| `remediation_guidance` | Orientacao concreta de como corrigir | "Capturar screenshot da exploracao, gerar hash, anexar ao finding" |
| `priority` | Quais itens sao bloqueantes vs. desejaveis | "Items 3, 7: bloqueantes; Item 12: desejavel" |

### 3.2 Exemplo de Feedback Completo

```yaml
rework_feedback:
  task_id: RT-2026-042
  iteration: 1
  reviewer: peter-kim
  score: 72%
  failed_items:
    - item: 3
      checklist: pentest-execution-quality
      expected: "Evidencia fotografica com hash SHA-256"
      actual: "Apenas descricao textual"
      remediation: "Capturar screenshot, gerar hash com sha256sum, anexar"
      blocking: true
```

---

## 4. Regras de Iteracao

Cada iteracao tem SLA, responsavel e escopo de acao diferenciado:

| Iteracao | SLA | Responsavel | Acao |
|----------|-----|-------------|------|
| **1** | 4h (ou proximo dia util) | Agente original | Corrige itens falhados com base no feedback recebido. Resubmete para review. |
| **2** | 8h | Agente + Domain Lead | Domain lead supervisiona a correcao. Revisao conjunta antes do resubmit. |
| **3** | 24h | Escalado ao `cyber-chief` | Cyber-chief pode: reassignar a outro agente, pedir abordagem diferente, ou intervir diretamente. |

**Regras adicionais**:
- Cada iteracao deve resolver **pelo menos** os itens bloqueantes identificados no feedback
- O score deve melhorar em cada iteracao — estagnacao em 2 iteracoes consecutivas dispara escalacao
- O reviewer da iteracao N+1 deve ser o mesmo da iteracao N (continuidade de contexto)

---

## 5. Fluxo de Rework — Diagrama

```
Output --> Quality Gate Avaliacao
              |
              +--- >= 80% --> APROVADO (registra decisions-log)
              +--- < 60%  --> ESCALACAO IMEDIATA (cyber-chief)
              +--- 60-79% --> ITERACAO 1 (4h, agente) --> Re-avaliacao
                                 |                            |
                            >= 80% = APROVADO            < 80% = ITERACAO 2 (8h, domain lead)
                                                              |
                                                         Re-avaliacao
                                                              |
                                                    >= 80% = APROVADO
                                                    < 80% = ITERACAO 3 (24h, cyber-chief)
                                                                  |
                                                             Re-avaliacao
                                                                  |
                                                        >= 80% = APROVADO
                                                        < 80% = DECISAO FINAL (cyber-chief)
```

---

## 6. Escalacao Apos Max Iteracoes

Quando as 3 iteracoes sao esgotadas sem atingir o threshold, o `cyber-chief` tem tres opcoes:

| Opcao | Quando Usar | Registro |
|-------|-------------|----------|
| **Reassign** | Agente original nao tem capacidade para esta task | Novo context packet, novo agente, reinicia contagem |
| **Approve with exceptions** | Itens faltantes sao menores e nao comprometem seguranca | Excecao documentada no decisions-log com justificativa |
| **Redesign approach** | Abordagem fundamental esta errada, precisa novo plano | Nova task criada com abordagem diferente |

Toda decisao pos-max-iteracao e registrada em [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) com `action: rework_escalation_decision`.

---

## 7. Tracking e Registro

Toda iteracao de rework e registrada no [`data/registries/decisions-log.md`](../data/registries/decisions-log.md):

| Campo | Descricao |
|-------|-----------|
| `task_id` | ID da task em rework |
| `iteration` | Numero da iteracao (1, 2, 3) |
| `feedback_given` | Resumo do feedback fornecido (referencia ao feedback completo) |
| `score_before` | Score antes da correcao |
| `score_after` | Score apos a correcao |
| `reviewer` | Quem avaliou |
| `decision` | rework / approved / escalated |
| `sla_met` | Se o SLA da iteracao foi cumprido (true/false) |

Melhorias identificadas durante rework sao adicionadas ao `data/backlog/improvement-backlog` conforme `config.yaml > rework_loop > tracking`.

---

## Referencias Cruzadas

- [`config.yaml`](../config.yaml) — secao `rework_loop`, `score_thresholds`, `review_loops`
- [`docs/quality-gate-system.md`](./quality-gate-system.md) — sistema de quality gates e thresholds
- [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) — registro de todas as iteracoes
- [`ARCHITECTURE.md`](../ARCHITECTURE.md) — secao 15 (Rework Loop Architecture)
- [`checklists/`](../checklists/) — checklists utilizados nas avaliacoes de gate
- [`docs/delegation-protocol.md`](./delegation-protocol.md) — reassignment via delegation protocol

---

*Cybersecurity Squad — Rework Loop Protocol v1.0.0*
