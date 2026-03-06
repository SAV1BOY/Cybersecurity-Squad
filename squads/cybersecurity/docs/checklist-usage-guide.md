# Checklist Usage Guide

Guia para utilizar os checklists de seguranca do squad de forma consistente e eficaz.

## Proposito dos Checklists

Checklists sao ferramentas de verificacao que garantem que nenhuma etapa critica seja esquecida durante a execucao de atividades de seguranca. Eles complementam os workflows, nao os substituem.

## Como Usar um Checklist

1. **Selecione o checklist** adequado para a atividade
2. **Revise todos os itens** antes de iniciar a execucao
3. **Marque cada item** conforme for completado
4. **Documente desvios** quando um item nao puder ser atendido
5. **Assine e date** o checklist ao final da execucao
6. **Arquive** como evidencia junto ao artefato principal

## Tipos de Checklists

### Pre-Engagement Checklist
- Verificacoes antes de iniciar um pentest ou review
- Itens incluem: autorizacao assinada, escopo definido, acessos provistos
- Responsavel: Engagement Lead Agent

### Hardening Checklist
- Verificacoes de configuracao segura para sistemas e servicos
- Baseado em CIS Benchmarks e baselines internos
- Responsavel: Infra Security Agent ou System Owner

### Incident Response Checklist
- Passos obrigatorios durante resposta a incidentes
- Garante que nada critico seja esquecido sob pressao
- Responsavel: Incident Handler Agent

### Code Review Security Checklist
- Verificacoes de seguranca durante code review
- Cobre OWASP Top 10 e patterns inseguros comuns
- Responsavel: AppSec Agent ou Security Reviewer

### Closeout Checklist
- Verificacoes de encerramento de engagements
- Itens incluem: relatorio entregue, credenciais revogadas, artifacts limpos
- Responsavel: Engagement Lead Agent

## Regras de Uso

- Checklists nao sao opcionais para atividades onde estao definidos
- Itens marcados como N/A devem ter justificativa documentada
- Checklists incompletos bloqueiam a finalizacao da atividade
- Revisoes periodicas dos checklists garantem que estejam atualizados

## Criando Novos Checklists

Para criar um novo checklist:
1. Identifique a atividade que se beneficiaria de verificacao sistematica
2. Liste todos os itens criticos baseado em experiencia e incidentes passados
3. Organize itens em ordem logica de execucao
4. Submeta para review e aprovacao do squad lead
5. Registre no repositorio e comunique ao squad

## Manutencao

- Checklists devem ser revisados trimestralmente
- Cada incidente ou near-miss deve gerar avaliacao de checklist
- Itens obsoletos devem ser removidos para evitar fadiga
- Novos itens devem ser adicionados quando gaps sao identificados
