# PASTA — Process for Attack Simulation and Threat Analysis

## Overview

O PASTA (Process for Attack Simulation and Threat Analysis) e uma metodologia de modelagem de ameacas centrada em risco que combina perspectivas de negocio e tecnicas em sete estagios estruturados. Diferente do STRIDE que foca em categorias de ameacas, o PASTA e orientado a objetivos de negocio e simula ataques reais para produzir um modelo de ameacas que reflete o risco efetivo para a organizacao. E particularmente adequado para sistemas complexos que requerem alinhamento entre stakeholders tecnicos e de negocio.

## Core Concepts

### Os 7 Estagios do PASTA

#### Stage 1 — Define Objectives

Estabelecimento do contexto de negocio e objetivos de seguranca:

- Identificar os objetivos de negocio do sistema ou aplicacao analisada.
- Definir requisitos de compliance e regulatorios aplicaveis.
- Estabelecer apetite de risco e criterios de aceitacao com stakeholders.
- Alinhar o escopo do threat model com prioridades de negocio.

#### Stage 2 — Define Technical Scope

Documentacao do ambiente tecnico e superficie de ataque:

- Mapear a arquitetura do sistema incluindo componentes, dependencias e integrações.
- Documentar tecnologias, protocolos e frameworks utilizados.
- Identificar trust boundaries e pontos de entrada de dados.
- Criar ou atualizar diagramas de arquitetura e data flow.

#### Stage 3 — Application Decomposition

Decomposicao detalhada da aplicacao para identificar ativos criticos:

- Criar Data Flow Diagrams (DFDs) detalhados com todos os componentes.
- Identificar ativos de informacao e classificar por sensibilidade.
- Mapear controles de seguranca existentes por componente.
- Documentar dependencias externas e integrações com terceiros.
- Identificar atores e seus niveis de acesso e privilegios.

#### Stage 4 — Threat Analysis

Analise de ameacas baseada em inteligencia e contexto:

- Pesquisar ameacas relevantes ao setor e tecnologias utilizadas.
- Consultar fontes de threat intelligence (MITRE ATT&CK, CVE databases, threat reports).
- Identificar adversarios provaveis e suas motivacoes e capacidades.
- Mapear attack vectors especificos para a superficie de ataque documentada.
- Criar threat library com ameacas categorizadas e priorizadas.

#### Stage 5 — Vulnerability Analysis

Identificacao de vulnerabilidades que viabilizam as ameacas:

- Correlacionar ameacas identificadas com vulnerabilidades conhecidas (CVEs, CWEs).
- Analisar resultados de scans de vulnerabilidade e pentests anteriores.
- Avaliar fraquezas de design e implementacao nos componentes criticos.
- Identificar vulnerabilidades em dependencias de terceiros e supply chain.
- Mapear gaps em controles de seguranca existentes.

#### Stage 6 — Attack Modeling and Simulation

Simulacao de ataques para validar cenarios de risco:

- Construir attack trees detalhadas para cada cenario de ameaca relevante.
- Mapear cadeias de ataque completas do ponto de entrada ate o objetivo adversario.
- Simular ataques em ambiente controlado para validar viabilidade.
- Calcular probabilidade de sucesso de cada cenario baseado em controles existentes.
- Priorizar cenarios por impacto de negocio e probabilidade de exploracao.

#### Stage 7 — Risk and Impact Analysis

Analise final de risco e definicao de estrategia de mitigacao:

- Calcular risco residual para cada cenario de ataque (probabilidade x impacto).
- Priorizar mitigacoes com base em reducao de risco e custo de implementacao.
- Definir controles compensatorios para riscos aceitos.
- Documentar plano de mitigacao com responsaveis e prazos.
- Comunicar resultados para stakeholders de negocio e tecnicos.

## Practical Application

### Quando Utilizar PASTA vs STRIDE

| Criterio | PASTA | STRIDE |
|----------|-------|--------|
| Complexidade do sistema | Alta | Baixa a media |
| Envolvimento de negocio | Essencial | Opcional |
| Profundidade de analise | Muito profunda | Moderada |
| Tempo de execucao | 2-4 semanas | 1-2 sessoes |
| Equipe necessaria | Multidisciplinar | Tecnica |
| Simulacao de ataques | Incluida | Nao incluida |

### Entregaveis por Estagio

| Estagio | Entregavel |
|---------|------------|
| Stage 1 | Business Context Document |
| Stage 2 | Technical Scope e Architecture Diagrams |
| Stage 3 | DFDs, Asset Inventory e Control Mapping |
| Stage 4 | Threat Library e Adversary Profiles |
| Stage 5 | Vulnerability Assessment Results |
| Stage 6 | Attack Trees e Simulation Results |
| Stage 7 | Risk Register e Mitigation Plan |

### Boas Praticas

1. Envolver product owners e business stakeholders desde o Stage 1.
2. Reutilizar artefatos de threat models anteriores para acelerar a analise.
3. Atualizar o threat model a cada mudanca significativa de arquitetura.
4. Integrar resultados no backlog de desenvolvimento como user stories de seguranca.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer conduz PASTA para sistemas de alta criticidade e complexidade.
- O stride-threat-model e utilizado como alternativa leve para componentes de menor risco.
- O risk-scoring-model recebe inputs do Stage 7 para calibracao de risco por sistema.
- O offense-layer executa simulacoes do Stage 6 como parte de red team engagements.
- O mitre-att-ck alimenta o Stage 4 com TTPs de adversarios relevantes ao setor.
- O finding-structure-standard documenta vulnerabilidades identificadas no Stage 5.
- Resultados de PASTA sao armazenados no repositorio do squad e revisados semestralmente.
- O security-kpi-dashboard exibe cobertura de threat modeling por sistema critico.
