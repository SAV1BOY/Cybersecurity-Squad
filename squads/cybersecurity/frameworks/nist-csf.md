# NIST Cybersecurity Framework (CSF)

## Overview

O NIST Cybersecurity Framework e um conjunto de diretrizes voluntarias criado pelo National Institute of Standards and Technology para ajudar organizacoes a gerenciar e reduzir riscos de ciberseguranca. Originalmente publicado em 2014 e atualizado na versao 2.0 em 2024, o framework fornece uma linguagem comum para comunicar postura de seguranca entre stakeholders tecnicos e executivos. Sua estrutura flexivel permite adocao por organizacoes de qualquer porte ou setor.

## Core Concepts

### Functions (Funcoes Principais)

O framework e organizado em seis funcoes que representam o ciclo de vida completo de gestao de risco cibernetico:

- **Govern (GV)** — Estabelece e monitora a estrategia de gestao de risco da organizacao, expectativas e politicas. Funcao adicionada na versao 2.0.
- **Identify (ID)** — Compreensao do contexto organizacional, ativos criticos, riscos e vulnerabilidades que afetam o ambiente.
- **Protect (PR)** — Implementacao de salvaguardas para garantir a entrega de servicos criticos e limitar o impacto de incidentes.
- **Detect (DE)** — Desenvolvimento e implementacao de atividades para identificar a ocorrencia de eventos de seguranca em tempo habil.
- **Respond (RS)** — Acoes tomadas apos a deteccao de um incidente para conter e mitigar seu impacto.
- **Recover (RC)** — Planejamento e execucao de atividades para restaurar capacidades afetadas por incidentes de seguranca.

### Implementation Tiers

Os Tiers descrevem o grau de rigor e sofisticacao das praticas de gestao de risco:

| Tier | Nome | Descricao |
|------|------|-----------|
| Tier 1 | Partial | Praticas reativas e ad hoc, sem processo formalizado |
| Tier 2 | Risk Informed | Consciencia de risco existe mas sem politica organizacional ampla |
| Tier 3 | Repeatable | Politicas formais aprovadas e processos consistentes |
| Tier 4 | Adaptive | Melhoria continua baseada em lessons learned e indicadores preditivos |

### Profiles

Profiles representam o alinhamento entre as funcoes do framework e os requisitos de negocio da organizacao. Dois tipos sao utilizados:

- **Current Profile** — Estado atual de seguranca da organizacao mapeado contra as categorias e subcategorias.
- **Target Profile** — Estado desejado que reflete os objetivos de reducao de risco e prioridades de negocio.

A comparacao entre Current e Target Profile gera um gap analysis que orienta o roadmap de investimentos em seguranca.

## Practical Application

### Processo de Implementacao

1. Definir o escopo e prioridades organizacionais junto ao board executivo.
2. Realizar inventario de sistemas, ativos e dados criticos (funcao Identify).
3. Criar o Current Profile documentando controles existentes por subcategoria.
4. Conduzir risk assessment para identificar lacunas e ameacas relevantes.
5. Estabelecer o Target Profile com base no apetite de risco aprovado.
6. Priorizar gaps e desenvolver o plano de acao com timelines e responsaveis.
7. Implementar controles e monitorar progresso com metricas definidas.

### Mapeamento com Outros Frameworks

O NIST CSF fornece Informative References que mapeiam subcategorias para controles especificos de outros padroes como ISO 27001, CIS Controls e COBIT. Isso permite que organizacoes com multiplas obrigacoes de compliance reutilizem evidencias e reduzam esforco duplicado.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- **Govern e Identify** sao utilizados pelo governance-layer para estruturar politicas e inventario de ativos.
- **Protect** orienta os controles implementados no defense-layer e identity-layer.
- **Detect** alimenta diretamente o detection-coverage-matrix e as capacidades do defense-layer SIEM/SOC.
- **Respond** e a base do ir-layer e do nist-800-61-incident-response workflow.
- **Recover** conecta-se ao plano de continuidade e ao processo de post-incident review.
- O risk-scoring-model utiliza os Tiers para calibrar a maturidade de cada dominio avaliado.
- Profiles sao gerados trimestralmente e apresentados no security-kpi-dashboard como indicador de maturidade.

### Metricas Relacionadas

| Metrica | Fonte | Frequencia |
|---------|-------|------------|
| CSF Coverage Score | Gap analysis por subcategoria | Trimestral |
| Tier Progression | Avaliacao de maturidade | Semestral |
| Profile Delta | Diferenca Current vs Target | Trimestral |
| Control Implementation Rate | Percentual de controles ativos | Mensal |
