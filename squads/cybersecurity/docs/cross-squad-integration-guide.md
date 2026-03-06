# Cross-Squad Integration Guide

Guia para integracao e colaboracao entre o Cybersecurity Squad e outros squads da organizacao.

## Principio de Integracao

Seguranca nao e responsabilidade exclusiva do Cybersecurity Squad. A integracao com outros squads e essencial para que seguranca seja incorporada em todos os processos.

## Pontos de Integracao

### Com Squads de Desenvolvimento
- **Security reviews** de novas features antes do deploy
- **SAST/DAST** integrado no pipeline de CI/CD
- **Feedback de seguranca** em code reviews
- **Threat modeling** de novos componentes
- Workflow relacionado: secure-sdlc-workflow.md

### Com Squad de Infraestrutura
- **Hardening reviews** de novas configuracoes
- **Cloud security reviews** de novos workloads
- **Vulnerability scanning** coordenado
- **Incident response** em sistemas de infraestrutura
- Workflow relacionado: cloud-security-review-workflow.md

### Com Squad de Dados
- **Classificacao de dados** e controles de acesso
- **Monitoramento de acesso** a dados sensiveis
- **Privacy impact assessments** para novos processamentos
- Compliance com LGPD e regulacoes de dados

### Com Squad de Produto
- **Security requirements** no backlog de produto
- **Risk assessment** de novas funcionalidades
- **Bug bounty triage** com impacto em produto
- Comunicacao de vulnerabilidades com impacto em clientes

## Processo de Handoff

Toda transferencia de trabalho entre squads deve seguir o cross-squad-handoff-workflow.md para garantir continuidade e rastreabilidade.

## Canais de Comunicacao

| Tipo | Canal | SLA |
|------|-------|-----|
| Solicitacao de review | Formulario de intake | 2 dias uteis para triagem |
| Incidente de seguranca | Canal de emergencia | 15 minutos para resposta |
| Consultoria | Canal do squad | 1 dia util para resposta |
| Feedback de code review | Pull request comments | Proximo dia util |

## Responsabilidades Compartilhadas

| Atividade | Cybersecurity Squad | Outro Squad |
|-----------|---------------------|-------------|
| Vulnerability fix | Identifica e prioriza | Implementa e testa |
| Detection rule | Desenvolve e monitora | Fornece contexto de negocio |
| Incident response | Coordena e investiga | Executa containment tecnico |
| Security review | Conduz avaliacao | Fornece documentacao e acesso |

## Escalacao entre Squads

- Conflitos de priorizacao sao escalados para os leads de ambos os squads
- Se nao resolvido, escalar para management compartilhado
- Decisoes de risco que afetam multiplos squads requerem aprovacao conjunta

## Metricas de Integracao

- Tempo medio de resposta a solicitacoes de outros squads
- Numero de reviews conduzidos por periodo
- Satisfacao dos squads parceiros (pesquisa trimestral)
- Findings remediados dentro do SLA por squad
