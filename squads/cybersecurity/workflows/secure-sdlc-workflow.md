# Secure SDLC Workflow

Integracao de praticas de seguranca em cada fase do ciclo de desenvolvimento de software.

## Objetivo

Garantir que seguranca seja incorporada desde o design ate o deploy, reduzindo vulnerabilidades em producao e o custo de remediacao tardia.

## Inputs

- Requisitos funcionais do projeto
- Politica de seguranca de desenvolvimento
- Ferramentas de SAST, DAST e SCA configuradas
- Checklists de seguranca por fase

## Stages

### 1. Requirements e Design

- Responsavel: **Security Champion Agent**
- Participar da definicao de requisitos para incluir security requirements
- Conduzir threat modeling do design proposto
- Definir security acceptance criteria para cada feature

### 2. Secure Coding

- Responsavel: **Developer** (com suporte do **AppSec Agent**)
- Seguir secure coding guidelines da organizacao
- Utilizar bibliotecas e frameworks aprovados
- Evitar patterns inseguros documentados no swipe file

### 3. Static Analysis (SAST)

- Responsavel: **AppSec Agent**
- Executar SAST no pipeline de CI automaticamente
- Ponto de decisao: **Findings criticos identificados?**
  - Sim -> bloquear merge e notificar developer
  - Nao -> prosseguir para proxima fase

### 4. Software Composition Analysis (SCA)

- Responsavel: **AppSec Agent**
- Verificar dependencias contra bancos de vulnerabilidades conhecidas
- Identificar licencas incompativeis
- Ponto de decisao: **Dependencia vulneravel?**
  - Sim -> exigir atualizacao ou aprovacao de excecao
  - Nao -> prosseguir

### 5. Code Review

- Responsavel: **Security Reviewer Agent**
- Revisar mudancas com foco em seguranca
- Validar que findings de SAST e SCA foram tratados
- Aprovar ou solicitar correcoes

### 6. Dynamic Analysis (DAST)

- Responsavel: **AppSec Agent**
- Executar DAST em ambiente de staging
- Testar para OWASP Top 10 e vulnerabilidades especificas do contexto
- Documentar findings e encaminhar para correcao

### 7. Pre-Production Security Review

- Responsavel: **Security Architect Agent**
- Revisar configuracoes de deploy (secrets management, TLS, headers)
- Validar que todos os findings foram tratados ou aceitos
- Ponto de decisao: **Aprovado para producao?**
  - Sim -> autorizar deploy
  - Nao -> bloquear ate resolucao

### 8. Production Monitoring

- Responsavel: **Detection Engineer Agent**
- Configurar alertas de seguranca para a nova aplicacao
- Monitorar primeiros dias em producao para anomalias
- Integrar com vulnerability management para scans continuos

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| SAST bloqueante | Finding de severidade critica | Bloquear pipeline ate correcao |
| Dependencia com CVE critico | SCA encontra vulnerabilidade explorada | Exigir atualizacao imediata |
| Threat model incompleto | Design mudou significativamente | Refazer threat model antes de prosseguir |
| Deploy de emergencia | Hotfix critico em producao | Seguir fast-track com revisao pos-deploy |

## Outputs

- Relatorio de seguranca por release
- Metricas de findings por fase do SDLC
- Threat models atualizados
- Security acceptance criteria validados
