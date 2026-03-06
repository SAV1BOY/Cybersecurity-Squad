# Workflow Guide

Guia para entender e utilizar os workflows do Cybersecurity Squad de forma eficaz.

## O que sao Workflows

Workflows sao processos repetiveis e documentados que descrevem o fluxo completo de uma atividade de seguranca, desde o inicio ate a conclusao. Cada workflow foi projetado para ser seguido por agentes do squad.

## Estrutura de um Workflow

Todo workflow do squad segue a mesma estrutura:

### Objetivo
Descricao clara do proposito do workflow e o que ele busca alcancar.

### Inputs
Lista de pre-requisitos e informacoes necessarias para iniciar o processo.

### Stages
Etapas sequenciais do processo, cada uma com:
- **Responsavel** - Agente designado para executar o stage
- **Atividades** - Acoes concretas a serem realizadas
- **Decision points** - Momentos de decisao com criterios claros

### Decision Points
Tabela consolidada de pontos de decisao criticos com condicoes e acoes correspondentes.

### Outputs
Artefatos e resultados esperados ao final do workflow.

## Como Escolher o Workflow Correto

| Situacao | Workflow |
|----------|----------|
| Preciso conduzir um pentest | pentest-engagement-workflow.md |
| Preciso acompanhar remediacao | pentest-to-remediation-loop.md |
| Preciso modelar ameacas | threat-model-to-controls-workflow.md |
| Preciso criar detection rules | detection-engineering-workflow.md |
| Preciso responder a incidente | incident-response-workflow.md |
| Preciso avaliar cobertura de deteccao | detection-to-coverage-loop.md |
| Preciso conduzir hunting | threat-hunting-sprint-workflow.md |
| Preciso transferir trabalho | cross-squad-handoff-workflow.md |

## Boas Praticas

1. **Leia o workflow completo** antes de iniciar a execucao
2. **Valide os inputs** antes de avancar para o primeiro stage
3. **Respeite os decision points** - eles existem para evitar erros
4. **Documente desvios** quando for necessario adaptar o processo
5. **Atualize o workflow** se identificar melhorias durante a execucao

## Adaptacao de Workflows

Workflows podem ser adaptados ao contexto, desde que:
- O objetivo original seja mantido
- Decision points criticos nao sejam ignorados
- Desvios sejam documentados e justificados
- A qualidade dos outputs nao seja comprometida

## Contribuindo com Melhorias

Para sugerir melhorias em workflows existentes:
1. Identifique o gap ou oportunidade de melhoria
2. Documente a proposta com justificativa
3. Submeta para review do squad lead
4. Apos aprovacao, atualize o arquivo e registre no changelog
