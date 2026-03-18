# Cross-Squad Integration Guide — Cybersecurity Squad

Guia operacional de integracao entre o Cybersecurity Squad e os 11 squads externos do MMOS.
Cada squad possui handoffs bidirecionais, SLAs definidos e assets compartilhados.

> **Referencia de configuracao:** `squads/cybersecurity/config.yaml` secao `cross_squad`
> **Protocolo de delegacao:** `docs/delegation-protocol.md`
> **Workflow de handoff:** `workflows/cross-squad-handoff-workflow.md`

---

## Principios Gerais

- Todo handoff segue o `cross-squad-handoff-workflow.md` — sem excecoes.
- O `cyber-chief` e responsavel por aprovar handoffs que saem do Cybersecurity Squad.
- Handoffs rejeitados retornam ao squad de origem com feedback especifico (ver `delegation-protocol.md`).
- Todos os handoffs sao registrados em `data/handoffs/handoff-tracking`.

---

## 1. Pre-Programming Squad

Integracao na fase de arquitetura e design de sistemas, antes do codigo ser escrito.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | architecture-docs para security review; system-design-specs para threat-modeling input |
| **handoff_from_cyber** | threat-model-results; security-architecture-review; sdlc-security-gates |

**Shared assets:** threat-models, security-requirements, architecture-diagrams

**SLAs:**
- Security architecture review: 3 dias uteis
- Threat model results: 5 dias uteis
- Feedback sobre design specs: 2 dias uteis

---

## 2. Data Squad

Protecao de dados, controles de acesso e conformidade com regulacoes de privacidade.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | data-pipeline-configs para review; data-classification-requests para assessment |
| **handoff_from_cyber** | data-protection-controls; access-audit-findings; privacy-impact-assessment |

**Shared assets:** data-classification-matrix, access-logs, privacy-controls

**SLAs:**
- Privacy impact assessment: 5 dias uteis
- Data protection control review: 3 dias uteis
- Access audit findings: 2 dias uteis

---

## 3. Design Squad

Revisao de seguranca e privacidade em interfaces de usuario e experiencia do usuario.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | ui-designs para accessibility/privacy review |
| **handoff_from_cyber** | security-ux-recommendations; privacy-pattern-library |

**Shared assets:** authentication-ux-patterns, error-message-guidelines

**SLAs:**
- Security UX review: 3 dias uteis
- Privacy pattern library updates: 5 dias uteis

---

## 4. Brand Squad

Protecao de propriedade intelectual e alinhamento de marca em comunicacoes de seguranca.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | brand-assets para IP protection review |
| **handoff_from_cyber** | phishing-simulation-brand-guidelines; incident-communication-templates |

**Shared assets:** communication-templates, brand-voice-for-security-comms

**SLAs:**
- Phishing simulation brand review: 3 dias uteis
- Incident communication template: 1 dia util (urgente)

---

## 5. Copy Squad

Producao de conteudo de seguranca e revisao tecnica de comunicacoes.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | security-content-drafts para technical review |
| **handoff_from_cyber** | security-awareness-content; incident-notification-drafts |

**Shared assets:** security-terminology, user-facing-error-messages

**SLAs:**
- Technical review de conteudo: 2 dias uteis
- Incident notification drafts: 4 horas (durante incidente ativo)
- Security awareness content: 5 dias uteis

---

## 6. C-Level Squad

Reportes executivos, alinhamento estrategico e briefings de incidentes criticos.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | strategic-priorities para alignment; risk-appetite-definition para risk-framework |
| **handoff_from_cyber** | security-posture-report; quarterly-security-review; critical-incident-briefing |

**Shared assets:** risk-register, maturity-scorecard, compliance-status

**SLAs:**
- Security posture report: entrega trimestral (ate dia 10 do trimestre)
- Critical incident briefing: 1 hora apos confirmacao de incidente critico
- Quarterly security review: 5 dias uteis antes da reuniao trimestral

---

## 7. Advisory Board Squad

Governanca, oversight e alinhamento com diretrizes estrategicas do board.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | governance-directives para policy alignment |
| **handoff_from_cyber** | security-program-maturity-report; risk-register-summary |

**Shared assets:** governance-frameworks, risk-appetite-statements

**SLAs:**
- Maturity report: entrega semestral
- Risk register summary: entrega trimestral
- Policy alignment response: 5 dias uteis

---

## 8. Storytelling Squad

Case studies sanitizados e narrativas de licoes aprendidas para uso interno e externo.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | narrative-content para sensitivity review |
| **handoff_from_cyber** | case-studies-sanitized; lessons-learned-narratives |

**Shared assets:** incident-case-studies, security-culture-stories

**SLAs:**
- Sensitivity review de conteudo: 3 dias uteis
- Case study sanitization: 5 dias uteis
- Lessons learned narratives: 5 dias uteis

---

## 9. Movement Squad

Programas de cultura de seguranca e rede de security champions na comunidade.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | community-platform-plans para security review |
| **handoff_from_cyber** | security-culture-program; security-champion-network |

**Shared assets:** security-awareness-campaigns, champion-program

**SLAs:**
- Community platform security review: 5 dias uteis
- Security culture program materials: 10 dias uteis
- Champion network onboarding: 5 dias uteis

---

## 10. Traffic Masters Squad

Deteccao de fraude, analise de bot traffic e revisao de privacidade em tracking.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | ad-platform-configs para review; tracking-pixel-deployments para privacy review |
| **handoff_from_cyber** | fraud-detection-alerts; bot-traffic-analysis |

**Shared assets:** fraud-indicators, bot-signatures, ad-fraud-patterns

**SLAs:**
- Fraud detection alerts: 4 horas (tempo real quando possivel)
- Ad platform security review: 3 dias uteis
- Privacy review de tracking pixels: 3 dias uteis

---

## 11. DeepResearch Squad

Pesquisa de ameacas emergentes, analise de vulnerabilidades e inteligencia de mercado.

| Direcao | Handoffs |
|---------|----------|
| **handoff_to_cyber** | research-on-emerging-threats para threat-intel |
| **handoff_from_cyber** | threat-landscape-analysis-requests; vulnerability-research-requests |

**Shared assets:** threat-research, vulnerability-analysis, industry-reports

**SLAs:**
- Threat landscape analysis request: 10 dias uteis
- Vulnerability research request: 5 dias uteis
- Emerging threat intel ingestion: 2 dias uteis

---

## Tabela Resumo de SLAs

| Squad | SLA Padrao | SLA Urgente |
|-------|-----------|-------------|
| Pre-Programming | 3 dias uteis | 1 dia util |
| Data | 3 dias uteis | 1 dia util |
| Design | 3 dias uteis | 1 dia util |
| Brand | 3 dias uteis | 1 dia util |
| Copy | 2 dias uteis | 4 horas |
| C-Level | 5 dias uteis | 1 hora |
| Advisory Board | 5 dias uteis | 2 dias uteis |
| Storytelling | 3 dias uteis | 2 dias uteis |
| Movement | 5 dias uteis | 2 dias uteis |
| Traffic Masters | 3 dias uteis | 4 horas |
| DeepResearch | 5 dias uteis | 2 dias uteis |

---

## Processo de Escalacao Cross-Squad

1. Handoff rejeitado: retorna ao squad de origem com feedback; `cyber-chief` media se nao resolvido.
2. SLA expirado: escalacao para leads de ambos os squads em 24h.
3. Conflito de prioridades: reuniao de triagem conjunta em 24h.
4. Seguranca vs. delivery: decisao baseada em risco pelo `cyber-chief` com rationale documentado.

Detalhes completos em `config.yaml` secao `escalation_rules.cross_squad_escalation`.

---

## Cross-References

| Documento | Caminho | Descricao |
|-----------|---------|-----------|
| Config de roteamento | `squads/cybersecurity/config.yaml` | Secao `cross_squad` com handoffs e shared assets por squad |
| Protocolo de delegacao | `docs/delegation-protocol.md` | Regras para delegacao e handoff packages |
| Workflow de handoff | `workflows/cross-squad-handoff-workflow.md` | Workflow operacional para transferencia entre squads |
| Handoff tracking | `data/handoffs/handoff-tracking` | Registry de todos os handoffs realizados |
| Decisions log | `data/registries/decisions-log` | Registro de decisoes de escalacao e override |
| Escalation rules | `config.yaml` secao `escalation_rules` | Regras de escalacao por severidade e cross-squad |
| Quality gates | `config.yaml` secao `go_no_go.before_cross_squad_handoff` | Criterios obrigatorios antes de handoff |
