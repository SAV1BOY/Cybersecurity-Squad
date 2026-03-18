# Security Awareness Workflow

Processo para desenvolver, executar e medir campanhas de conscientizacao de seguranca.

## Objetivo

Reduzir o risco humano atraves de programas de awareness que educam colaboradores sobre ameacas comuns e comportamentos seguros, medindo eficacia ao longo do tempo.

## Inputs

- Metricas de incidentes causados por fator humano
- Resultados de phishing simulations anteriores
- Requisitos de compliance para treinamento
- Calendario organizacional e datas relevantes

## Stages

### 1. Needs Assessment

- Responsavel: **marcus-carey**
- Analisar incidentes recentes para identificar areas de maior risco humano
- Revisar resultados de campanhas anteriores
- Identificar grupos de alto risco (novos funcionarios, executivos, IT admins)

### 2. Content Development

- Responsavel: **marcus-carey**
- Desenvolver materiais de treinamento por topico (phishing, passwords, social engineering, data handling)
- Adaptar linguagem para cada publico-alvo
- Criar quizzes e exercicios praticos

### 3. Campaign Planning

- Responsavel: **marcus-carey**
- Definir cronograma de campanhas ao longo do ano
- Ponto de decisao: **Campanha inclui phishing simulation?**
  - Sim -> coordenar com red team para preparar templates
  - Nao -> prosseguir com treinamento direto

### 4. Execution

- Responsavel: **marcus-carey**
- Distribuir treinamentos via plataforma de learning
- Executar phishing simulations conforme planejado
- Enviar comunicacoes de reforco e lembretes

### 5. Measurement

- Responsavel: **cyber-chief**
- Coletar metricas de participacao e conclusao de treinamento
- Analisar resultados de phishing simulation (click rate, report rate)
- Ponto de decisao: **Metas de awareness atingidas?**
  - Sim -> documentar sucesso e planejar proxima campanha
  - Nao -> identificar gaps e ajustar abordagem

### 6. Follow-Up

- Responsavel: **marcus-carey**
- Oferecer treinamento adicional para quem falhou na simulation
- Reconhecer publicamente comportamentos seguros (report de phishing)
- Atualizar materiais com base no feedback recebido

### 7. Reporting

- Responsavel: **cyber-chief**
- Gerar relatorio de eficacia do programa para management
- Mostrar tendencias historicas e ROI do programa
- Recomendar investimentos para o proximo ciclo

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Alta taxa de clique em phishing | Click rate > 15% | Intensificar treinamento para grupo afetado |
| Baixa participacao | Conclusao < 80% | Escalar para management dos departamentos |
| Incidente pos-treinamento | Funcionario treinado comete erro | Revisar eficacia do conteudo |
| Novo tipo de ameaca | Ameaca emergente relevante | Criar campanha de awareness emergencial |

## Outputs

- Relatorio trimestral de awareness
- Metricas de phishing simulation por departamento
- Certificados de conclusao de treinamento
- Plano de campanhas para o proximo periodo

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
