# OWASP Top 10 — Web Application Security Risks

## Overview

O OWASP Top 10 e o documento de conscientizacao mais reconhecido sobre riscos de seguranca em aplicacoes web. Publicado pela Open Worldwide Application Security Project, o ranking e atualizado periodicamente com base em dados de vulnerabilidades coletados de centenas de organizacoes. A edicao 2021 introduziu tres novas categorias e reorganizou riscos existentes para refletir a evolucao do cenario de ameacas. Serve como ponto de partida essencial para programas de AppSec.

## Core Concepts

### As 10 Categorias de Risco (2021)

#### A01:2021 — Broken Access Control

Controles de acesso mal implementados permitem que usuarios ajam fora de suas permissoes. Inclui IDOR, escalacao de privilegios, manipulacao de tokens e bypass de controles via path traversal. Subiu da quinta posicao em 2017 para a primeira em 2021.

#### A02:2021 — Cryptographic Failures

Anteriormente chamado Sensitive Data Exposure, foca em falhas criptograficas que levam a exposicao de dados sensiveis. Inclui uso de algoritmos fracos, chaves hardcoded, transmissao em texto plano e armazenamento inseguro.

#### A03:2021 — Injection

Abrange SQL Injection, NoSQL Injection, OS Command Injection, LDAP Injection e Cross-Site Scripting (XSS). Dados nao confiaveis enviados como parte de comandos ou queries permitem execucao nao autorizada.

#### A04:2021 — Insecure Design

Categoria nova focada em falhas de design e arquitetura. Diferencia-se de implementacao insegura pois nenhum nivel de qualidade de codigo corrige um design fundamentalmente inseguro. Requer threat modeling e secure design patterns.

#### A05:2021 — Security Misconfiguration

Configuracoes inseguras em qualquer nivel do stack, incluindo permissoes excessivas, features desnecessarias habilitadas, default credentials, stack traces expostas e headers de seguranca ausentes.

#### A06:2021 — Vulnerable and Outdated Components

Uso de bibliotecas, frameworks e componentes com vulnerabilidades conhecidas. Inclui falta de inventario de dependencias, ausencia de monitoramento de CVEs e incapacidade de atualizar componentes em tempo habil.

#### A07:2021 — Identification and Authentication Failures

Falhas em confirmacao de identidade, autenticacao e gestao de sessoes. Inclui credential stuffing, brute force, senhas fracas, recuperacao de senha insegura e fixacao de sessao.

#### A08:2021 — Software and Data Integrity Failures

Categoria nova que abrange falhas de integridade em software e dados. Inclui CI/CD pipelines inseguros, auto-update sem verificacao de integridade e desserializacao insegura.

#### A09:2021 — Security Logging and Monitoring Failures

Insuficiencia de logging, deteccao, monitoramento e resposta ativa. Sem estas capacidades, ataques podem persistir sem deteccao por longos periodos.

#### A10:2021 — Server-Side Request Forgery (SSRF)

Categoria nova onde a aplicacao busca recursos remotos sem validar a URL fornecida pelo usuario. Permite que atacantes facam a aplicacao enviar requests para destinos inesperados, mesmo protegidos por firewalls.

## Practical Application

### Abordagem por Fase do SDLC

| Fase | Atividade | Categorias Cobertas |
|------|-----------|-------------------|
| Design | Threat Modeling | A01, A04, A08 |
| Development | Secure Coding Standards | A02, A03, A07 |
| Build | SAST e SCA | A03, A06, A08 |
| Test | DAST e Pentest | A01, A05, A10 |
| Deploy | Configuration Review | A05, A09 |
| Operate | Monitoring e WAF | A01, A03, A09, A10 |

### Estrategia de Mitigacao

1. Implementar access control robusto no server-side com deny-by-default (A01).
2. Adotar criptografia forte para dados em transito e em repouso (A02).
3. Utilizar parameterized queries e input validation em todas as entradas (A03).
4. Conduzir threat modeling em cada feature de alto risco (A04).
5. Automatizar verificacao de configuracao com Infrastructure as Code (A05).
6. Implementar SCA continuo com alertas de vulnerabilidades em dependencias (A06).
7. Adotar MFA e politicas de senha alinhadas ao NIST 800-63 (A07).
8. Verificar integridade de artefatos no CI/CD pipeline (A08).
9. Centralizar logs de seguranca com alertas para eventos criticos (A09).
10. Validar e sanitizar URLs em funcionalidades de fetch remoto (A10).

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer utiliza o OWASP Top 10 como baseline minimo para security testing de aplicacoes web.
- O finding-structure-standard referencia categorias do Top 10 para classificacao de vulnerabilidades.
- O offense-layer inclui cobertura das 10 categorias como requisito em todo web application pentest.
- O security-champion-program utiliza o Top 10 como conteudo fundamental de treinamento para desenvolvedores.
- O owasp-asvs expande cada categoria com requisitos de verificacao detalhados por nivel.
- O vuln-triage-playbook mapeia severidade padrao por categoria para agilizar priorizacao.
- O bug-bounty-framework define recompensas alinhadas as categorias do Top 10 por criticidade.
