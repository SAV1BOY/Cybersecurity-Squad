# OWASP SAMM — Software Assurance Maturity Model

## Overview

O OWASP Software Assurance Maturity Model (SAMM) e um framework de maturidade que ajuda organizacoes a formular e implementar uma estrategia de seguranca de software alinhada aos riscos especificos do negocio. Diferente de checklists de vulnerabilidades, o SAMM avalia a maturidade dos processos de seguranca em todo o ciclo de vida do software. A versao 2.0 reestruturou o modelo em cinco funcoes de negocio com 15 praticas de seguranca, cada uma avaliada em tres niveis de maturidade.

## Core Concepts

### Funcoes de Negocio (Business Functions)

#### 1. Governance

Gestao das atividades de seguranca de software na organizacao:

- **Strategy and Metrics** — Definicao de estrategia de seguranca, objetivos mensuraveis e roadmap.
- **Policy and Compliance** — Politicas de seguranca, padroes de conformidade e auditorias.
- **Education and Guidance** — Programas de treinamento, guidelines e knowledge base de seguranca.

#### 2. Design

Incorporacao de seguranca no design de aplicacoes:

- **Threat Assessment** — Identificacao e avaliacao de ameacas por aplicacao e por feature.
- **Security Requirements** — Definicao de requisitos de seguranca derivados de riscos e compliance.
- **Security Architecture** — Padroes de arquitetura segura, componentes reutilizaveis e design review.

#### 3. Implementation

Praticas de seguranca durante a codificacao e build:

- **Secure Build** — Automacao de build seguro, dependency management e reproducible builds.
- **Secure Deployment** — Hardening de deploy, gestao de segredos e configuration management.
- **Defect Management** — Rastreamento, priorizacao e remediacao de defeitos de seguranca.

#### 4. Verification

Validacao de seguranca do software produzido:

- **Architecture Assessment** — Revisao de arquitetura contra ameacas e requisitos de seguranca.
- **Requirements-driven Testing** — Testes derivados de requisitos de seguranca e abuse cases.
- **Security Testing** — SAST, DAST, IAST e penetration testing integrados ao pipeline.

#### 5. Operations

Gestao de seguranca em software em producao:

- **Incident Management** — Deteccao, resposta e aprendizado com incidentes de seguranca.
- **Environment Management** — Hardening de infraestrutura, patching e configuration monitoring.
- **Operational Management** — Gestao de dados, continuidade de negocio e lifecycle management.

### Niveis de Maturidade

Cada pratica e avaliada em tres niveis progressivos:

| Nivel | Caracteristica | Descricao |
|-------|---------------|-----------|
| 1 | Initial | Entendimento basico e praticas ad hoc implementadas |
| 2 | Managed | Praticas definidas, documentadas e consistentemente aplicadas |
| 3 | Optimized | Automacao abrangente, melhoria continua e metricas integradas |

### Assessment Model

O SAMM utiliza um questionario estruturado com criterios objetivos para cada nivel de cada pratica. Cada resposta gera um score de 0 a 1, permitindo:

- Visualizacao de maturidade por pratica em formato radar/spider chart.
- Comparacao entre equipes, produtos ou unidades de negocio.
- Definicao de target scores e gap analysis para roadmap de melhoria.
- Benchmarking anonimo contra organizacoes do mesmo setor.

## Practical Application

### Processo de Assessment

1. Selecionar escopo do assessment (organizacao, unidade de negocio ou produto).
2. Conduzir assessment inicial utilizando o questionario SAMM com stakeholders relevantes.
3. Documentar scores atuais e gerar o Current Maturity Profile.
4. Definir Target Maturity Profile com base nos objetivos de seguranca e riscos do negocio.
5. Identificar gaps e priorizar acoes de melhoria por impacto e viabilidade.
6. Implementar melhorias em ciclos trimestrais com milestones mensuraveis.
7. Reassessar semestralmente para medir progresso e ajustar o roadmap.

### Exemplo de Roadmap

- **Trimestre 1** — Estabelecer Strategy and Metrics (Governance) e Secure Build (Implementation).
- **Trimestre 2** — Implementar Security Testing automatizado (Verification) e Defect Management (Implementation).
- **Trimestre 3** — Desenvolver Threat Assessment (Design) e Security Requirements (Design).
- **Trimestre 4** — Fortalecer Incident Management (Operations) e Education and Guidance (Governance).

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O governance-layer alinha-se a funcao Governance do SAMM para politicas e metricas de seguranca.
- O appsec-layer implementa praticas das funcoes Design, Implementation e Verification.
- O security-champion-program contribui para Education and Guidance da funcao Governance.
- O ir-layer mapeia-se a pratica Incident Management da funcao Operations.
- O nist-ssdf complementa o SAMM com praticas especificas de desenvolvimento seguro.
- Assessments SAMM semestrais sao conduzidos pelo squad e resultados exibidos no security-kpi-dashboard.
- Target profiles por equipe de desenvolvimento sao definidos em colaboracao com tech leads.
- O risk-scoring-model incorpora scores SAMM como fator de maturidade na avaliacao de risco por produto.
