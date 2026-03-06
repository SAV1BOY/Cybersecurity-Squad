# Security Architecture Review Workflow

Processo para avaliar a seguranca de arquiteturas de sistemas antes e durante a implementacao.

## Objetivo

Identificar riscos de seguranca em decisoes de arquitetura antes que se tornem vulnerabilidades em producao, garantindo que princípios de security by design sejam aplicados.

## Inputs

- Documento de arquitetura ou design proposto
- Diagramas de componentes, dados e infraestrutura
- Requisitos de seguranca e compliance aplicaveis
- Historico de reviews de sistemas similares

## Stages

### 1. Request Intake

- Responsavel: **Architecture Review Agent**
- Receber solicitacao de review via intake form
- Validar que documentacao minima esta disponivel
- Classificar complexidade e agendar review

### 2. Documentation Review

- Responsavel: **Security Architect Agent**
- Analisar diagramas de arquitetura e data flows
- Identificar trust boundaries e pontos de integracao
- Ponto de decisao: **Documentacao suficiente para review?**
  - Sim -> prosseguir com analise
  - Nao -> solicitar informacoes adicionais ao time de engenharia

### 3. Threat Analysis

- Responsavel: **Threat Model Lead Agent**
- Aplicar threat modeling ao design proposto
- Identificar ameacas por componente e data flow
- Priorizar ameacas por likelihood e impact

### 4. Control Assessment

- Responsavel: **Security Architect Agent**
- Verificar quais controles de seguranca estao previstos no design
- Identificar controles ausentes ou insuficientes
- Mapear recomendacoes a frameworks de referencia

### 5. Review Session

- Responsavel: **Security Architect Agent**
- Conduzir sessao de review com a equipe de engenharia
- Apresentar findings e discutir recomendacoes
- Ponto de decisao: **Riscos criticos identificados?**
  - Sim -> bloquear implementacao ate resolucao
  - Nao -> aprovar com condicoes ou sem ressalvas

### 6. Recommendations Documentation

- Responsavel: **Security Architect Agent**
- Documentar todas as recomendacoes com justificativa
- Classificar como mandatory, recommended ou nice-to-have
- Definir criterios de aceitacao para cada recomendacao

### 7. Follow-Up

- Responsavel: **Architecture Review Agent**
- Verificar implementacao das recomendacoes mandatory
- Conduzir re-review se mudancas significativas foram feitas
- Atualizar catalogo de patterns aprovados se aplicavel

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Dados sensiveis sem encryption | PII ou dados regulados expostos | Bloquear ate implementar encryption |
| Autenticacao fraca | Sem MFA para acesso privilegiado | Exigir MFA antes do deploy |
| Single point of failure | Sem redundancia para componente critico | Recomendar alta disponibilidade |
| Integracao insegura | API sem autenticacao ou rate limiting | Exigir controles antes de aprovar |

## Outputs

- Relatorio de security architecture review
- Lista de recomendacoes priorizadas
- Decisao formal (aprovado, aprovado com condicoes, bloqueado)
- Threat model do sistema revisado
