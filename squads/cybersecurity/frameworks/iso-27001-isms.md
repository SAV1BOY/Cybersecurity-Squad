# ISO 27001 — Information Security Management System (ISMS)

## Overview

A ISO/IEC 27001 e o padrao internacional mais reconhecido para estabelecimento, implementacao, manutencao e melhoria continua de um Sistema de Gestao de Seguranca da Informacao (ISMS). Publicada pela International Organization for Standardization, a versao 2022 reestruturou os controles do Annex A em quatro temas e adicionou 11 novos controles. A certificacao ISO 27001 e frequentemente exigida por clientes enterprise e reguladores como evidencia de maturidade em seguranca da informacao.

## Core Concepts

### Estrutura do ISMS

O ISMS e baseado no ciclo PDCA (Plan-Do-Check-Act) aplicado a seguranca da informacao:

- **Plan** — Estabelecer politica, objetivos, processos e procedimentos do ISMS relevantes para gestao de risco e melhoria da seguranca da informacao.
- **Do** — Implementar e operar a politica, controles, processos e procedimentos do ISMS.
- **Check** — Avaliar e medir o desempenho dos processos contra a politica, objetivos e experiencia pratica, reportando resultados para analise critica.
- **Act** — Tomar acoes corretivas e preventivas baseadas nos resultados da auditoria interna e analise critica para alcancar melhoria continua.

### Clausulas Obrigatorias (4-10)

| Clausula | Titulo | Requisito |
|----------|--------|-----------|
| 4 | Context of the Organization | Entender o contexto interno e externo, partes interessadas e escopo |
| 5 | Leadership | Comprometimento da lideranca, politica e papeis organizacionais |
| 6 | Planning | Acoes para tratar riscos e oportunidades, objetivos de seguranca |
| 7 | Support | Recursos, competencia, conscientizacao, comunicacao e informacao documentada |
| 8 | Operation | Planejamento operacional, risk assessment e risk treatment |
| 9 | Performance Evaluation | Monitoramento, auditoria interna e analise critica pela direcao |
| 10 | Improvement | Nao conformidades, acoes corretivas e melhoria continua |

### Annex A — Controles de Referencia (ISO 27001:2022)

A versao 2022 reorganizou os controles em quatro temas:

- **Organizational Controls (37 controles)** — Politicas, papeis, segregacao de funcoes, threat intelligence, seguranca em projetos e cadeia de suprimentos.
- **People Controls (8 controles)** — Screening, termos de emprego, conscientizacao, treinamento e disciplina.
- **Physical Controls (14 controles)** — Perimetros de seguranca, controle de entrada, protecao contra ameacas ambientais.
- **Technological Controls (34 controles)** — Endpoint, acesso privilegiado, restricao de acesso a informacao, codificacao segura, monitoramento e filtragem web.

Total: 93 controles (reduzidos de 114 na versao 2013 por consolidacao).

### Novos Controles na Versao 2022

- Threat Intelligence (5.7)
- Information Security for Cloud Services (5.23)
- ICT Readiness for Business Continuity (5.30)
- Configuration Management (8.9)
- Information Deletion (8.10)
- Data Masking (8.11)
- Data Leakage Prevention (8.12)
- Monitoring Activities (8.16)
- Web Filtering (8.23)
- Secure Coding (8.28)

## Practical Application

### Jornada de Certificacao

1. Obter comprometimento executivo e definir o escopo do ISMS.
2. Conduzir risk assessment abrangente dos ativos de informacao no escopo.
3. Selecionar controles aplicaveis do Annex A e documentar a Statement of Applicability (SoA).
4. Implementar controles e processos documentando evidencias conforme clausula 7.5.
5. Executar ciclo completo de auditoria interna (clausula 9.2) e management review (clausula 9.3).
6. Contratar organismo certificador acreditado para auditoria Stage 1 (documentacao) e Stage 2 (implementacao).
7. Manter certificacao com auditorias de supervisao anuais e recertificacao a cada tres anos.

### Documentacao Essencial

- Politica de Seguranca da Informacao e Escopo do ISMS.
- Metodologia e resultados do Risk Assessment.
- Statement of Applicability (SoA) com justificativa para inclusao e exclusao de controles.
- Risk Treatment Plan com responsaveis e prazos.
- Registros de treinamento, auditorias internas e management reviews.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O governance-layer implementa as clausulas 4 a 10 como estrutura de governanca do programa de seguranca.
- O risk-scoring-model e calibrado para ser compativel com a metodologia de risk assessment da ISO 27001.
- Controles Organizational do Annex A sao mapeados para politicas mantidas no governance-layer.
- Controles Technological alimentam requisitos do defense-layer, identity-layer e appsec-layer.
- O evidence-standard define formatos de evidencia compativeis com requisitos de auditoria ISO 27001.
- Auditorias internas semestrais sao conduzidas pelo squad e resultados rastreados no security-kpi-dashboard.
- A Statement of Applicability e revisada a cada ciclo de auditoria e armazenada no repositorio do squad.
- O security-champion-program contribui para o controle People relacionado a conscientizacao (6.3).
