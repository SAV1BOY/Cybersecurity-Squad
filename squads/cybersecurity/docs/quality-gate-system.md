# Quality Gate System — Cybersecurity Squad

> Arquitetura completa do sistema de quality gates do Cybersecurity Squad.
> Este documento define tipos de gates, modelo de scoring, thresholds, mecanica de rework e instrucoes operacionais.

## 1. Visao Geral

O quality gate system garante que todo output do squad atenda padroes minimos de qualidade antes de avancar no workflow. Cada gate e uma barreira de validacao que avalia o output contra checklists especificos definidos em [`config.yaml`](../config.yaml) na secao `quality_gates`. Nenhum deliverable sai do squad sem passar por pelo menos um hard gate.

---

## 2. Tipos de Gate

### 2.1 Soft Gate (Advisory, Non-Blocking)

Gate informativo que gera alertas mas **nao bloqueia** o avanco do workflow. Utilizado para recomendacoes de melhoria e metricas de tendencia. O agente recebe o feedback mas pode prosseguir.

- **Exemplo**: revisao de estilo de report, sugestoes de melhoria em evidencias opcionais.
- **Registro**: logado no [`decisions-log.md`](../data/registries/decisions-log.md) como `gate_type: soft`.

### 2.2 Hard Gate (Blocking, Must Pass)

Gate **obrigatorio e bloqueante**. O output so avanca se o score atingir o threshold minimo. Aplicado a todos os quality gates listados em `config.yaml > quality_gates > mandatory`.

- **Checklists obrigatorios**: `scope-and-roe-quality`, `evidence-chain-quality`, `security-report-quality`
- **Consequencia de falha**: entrada automatica no rework loop (ver [`docs/rework-loop-protocol.md`](./rework-loop-protocol.md))

### 2.3 Domain Gate (Per Red Team / Blue Team / AppSec / CloudSec / IR)

Gate especifico por dominio operacional. Cada domain team tem checklists adicionais alem dos mandatory gates. A configuracao completa esta em `config.yaml > quality_gates > per_domain`.

### 2.4 Workflow Gate (Per Workflow Stage)

Gate aplicado na transicao entre stages de um workflow. O stage owner do proximo estagio valida o output do stage anterior antes de aceitar. Definido nos arquivos de workflow em [`workflows/`](../workflows/).

### 2.5 Final Gate (Before Delivery/Handoff)

Gate final antes da entrega ao stakeholder ou handoff cross-squad. Revisado obrigatoriamente pelo `cyber-chief`. Inclui validacao de todos os hard gates + domain gates aplicaveis + checklist de handoff. Ver criterios em `config.yaml > go_no_go > before_report_delivery` e `before_cross_squad_handoff`.

---

## 3. Modelo de Scoring

O scoring de cada gate segue formula simples e transparente:

```
Score = (checklist_items_checked / total_checklist_items) × 100
```

Cada item do checklist e binario: **checked** (atendido com evidencia) ou **unchecked** (nao atendido ou evidencia insuficiente). Nao ha scores parciais por item. O score final e a porcentagem de itens atendidos.

---

## 4. Thresholds e Classificacao

Os thresholds sao definidos em [`config.yaml`](../config.yaml) na secao `score_thresholds`:

| Score | Classificacao | Acao |
|-------|--------------|------|
| >= 95% | **SOTA** (State of the Art) | Aprovado automaticamente; pode pular review manual (`auto_approve`) |
| >= 90% | **GOLD** | Aprovado; referencia de excelencia para o squad |
| >= 80% | **PASS** | Aprovado; atende o minimo aceitavel |
| < 80% | **REWORK** | Reprovado; entra no rework loop obrigatoriamente |
| < 60% | **ESCALATION** | Reprovado com escalacao imediata ao `cyber-chief` |

---

## 5. Mecanica de Rework

Quando um gate falha (score < 80%), o output entra no rework loop:

1. **Iteracao 1**: retorno ao agente original com feedback especifico e itens reprovados. SLA: 4h.
2. **Iteracao 2**: revisao com supervisao do domain lead. SLA: 8h.
3. **Iteracao 3**: escalacao ao `cyber-chief`; possivel reassignment. SLA: 24h.
4. **Apos 3 iteracoes**: `cyber-chief` decide entre aprovar com excecoes documentadas ou redesenhar abordagem.

**Regras fundamentais**:
- Maximo de **3 iteracoes** antes de escalacao final
- Feedback **deve** ser especifico — itens exatos que falharam, esperado vs. encontrado, orientacao de remediacao
- Score < 60% na primeira iteracao → escalacao imediata, sem passar pelas 3 iteracoes

Detalhes completos do rework loop em [`docs/rework-loop-protocol.md`](./rework-loop-protocol.md).

---

## 6. Gate Registry

Toda avaliacao de gate e registrada em [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) com os seguintes campos:

| Campo | Descricao |
|-------|-----------|
| `timestamp` | Data e hora da avaliacao |
| `task_id` | Referencia a task avaliada |
| `gate_type` | soft / hard / domain / workflow / final |
| `checklist_applied` | Nome(s) do(s) checklist(s) utilizado(s) |
| `score` | Porcentagem obtida |
| `classification` | SOTA / GOLD / PASS / REWORK / ESCALATION |
| `reviewer` | Agente que avaliou |
| `decision` | approved / rework / escalated |
| `feedback` | Detalhes de itens reprovados (se aplicavel) |
| `iteration` | Numero da iteracao de rework (se aplicavel) |

---

## 7. Matriz de Gates por Dominio

Extraida de [`config.yaml`](../config.yaml) secao `quality_gates`:

| Dominio | Checklists Mandatory (todos) | Checklists de Dominio |
|---------|-----------------------------|-----------------------|
| **Red Team** | scope-and-roe-quality, evidence-chain-quality, security-report-quality | [pentest-execution-quality](../checklists/pentest-execution-quality.md), redteam-safe-testing-rules |
| **AppSec** | scope-and-roe-quality, evidence-chain-quality, security-report-quality | [code-review-security-quality](../checklists/code-review-security-quality.md), manico-ssdlc-gates |
| **Blue Team** | scope-and-roe-quality, evidence-chain-quality, security-report-quality | [detection-engineering-quality](../checklists/detection-engineering-quality.md), blueteam-detection-coverage |
| **IR** | scope-and-roe-quality, evidence-chain-quality, security-report-quality | [incident-triage-quality](../checklists/incident-triage-quality.md), [forensics-collection-quality](../checklists/forensics-collection-quality.md) |
| **CloudSec** | scope-and-roe-quality, evidence-chain-quality, security-report-quality | [cloud-security-assessment-quality](../checklists/cloud-security-assessment-quality.md), cloud-iam-least-privilege |

Os checklists mandatory aplicam-se a **todos** os dominios sem excecao. Os de dominio sao adicionais. Todos no diretorio [`checklists/`](../checklists/).

---

## 8. Como Avaliar um Gate — Instrucoes Operacionais

1. **Identificar checklists aplicaveis**: consulte [`config.yaml`](../config.yaml) secao `routing` para a task em questao.
2. **Verificar tipo de gate**: determine se e soft, hard, domain, workflow ou final. Hard gates e domain gates sao sempre bloqueantes.
3. **Obter o checklist**: acesse o arquivo no diretorio [`checklists/`](../checklists/). Leia cada item criteriosamente.
4. **Avaliar cada item**: marque como **checked** (atendido com evidencia) ou **unchecked** (nao atendido). Nao ha meio-termo.
5. **Calcular o score**: aplique `(checked / total) x 100`. Compare com os thresholds da secao 4.
6. **Se score >= 80%**: aprove, registre no [`decisions-log.md`](../data/registries/decisions-log.md) e avance no workflow.
7. **Se score < 80%**: retorne ao agente com feedback especifico. Inicie o rework loop conforme [`docs/rework-loop-protocol.md`](./rework-loop-protocol.md). Se < 60%, escale imediatamente ao `cyber-chief`.
8. **Final gate** (se aplicavel): antes de delivery/handoff, `cyber-chief` valida todos os hard gates + domain gates + criterios go/no-go.

---

## Referencias Cruzadas

- [`config.yaml`](../config.yaml) — secoes `quality_gates`, `score_thresholds`, `go_no_go`, `rework_loop`
- [`docs/rework-loop-protocol.md`](./rework-loop-protocol.md) — protocolo completo de rework
- [`checklists/`](../checklists/) — todos os checklists disponiveis
- [`data/registries/decisions-log.md`](../data/registries/decisions-log.md) — registro de avaliacoes
- [`ARCHITECTURE.md`](../ARCHITECTURE.md) — secao 7 (Quality Gates Obrigatorios), secao 15 (Rework Loop Architecture)

---

*Cybersecurity Squad — Quality Gate System v1.0.0*
