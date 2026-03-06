# Incident Response Workflow

Processo de resposta a incidentes de seguranca desde a deteccao ate o encerramento e lessons learned.

## Objetivo

Coordenar a resposta a incidentes de seguranca de forma rapida, organizada e documentada, minimizando impacto e garantindo preservacao de evidencias.

## Inputs

- Alerta do SIEM, SOC ou reporte manual
- Playbooks de resposta por tipo de incidente
- Lista de contatos de emergencia e escalation matrix
- Inventario de assets e criticidade

## Stages

### 1. Detection e Triage

- Responsavel: **SOC Analyst Agent (Tier 1)**
- Receber e registrar o alerta no sistema de tracking
- Realizar triage inicial: validar se e um true positive
- Ponto de decisao: **Incidente confirmado?**
  - Sim -> classificar severidade e escalar
  - Nao -> documentar como false positive e fechar

### 2. Classification e Escalation

- Responsavel: **SOC Analyst Agent (Tier 2)**
- Classificar o incidente por tipo (malware, phishing, data breach, unauthorized access)
- Atribuir severidade (P1-P4) com base em impacto e urgencia
- Escalar conforme a escalation matrix

### 3. Containment

- Responsavel: **Incident Handler Agent**
- Executar acoes de containment imediato (isolamento de host, bloqueio de conta)
- Ponto de decisao: **Containment efetivo?**
  - Sim -> prosseguir para investigacao
  - Nao -> escalar para containment mais agressivo
- Preservar evidencias antes de qualquer acao destrutiva

### 4. Investigation

- Responsavel: **Forensics Agent**
- Coletar e preservar evidencias digitais com chain of custody
- Analisar logs, memoria, disco e trafego de rede
- Determinar root cause, timeline e scope do comprometimento

### 5. Eradication

- Responsavel: **Incident Handler Agent**
- Remover presenca do adversario (malware, backdoors, contas comprometidas)
- Aplicar patches ou configuracoes necessarias
- Validar que o ambiente esta limpo

### 6. Recovery

- Responsavel: **System Owner** (com suporte do **IR Team**)
- Restaurar sistemas ao estado operacional normal
- Monitorar de perto para sinais de re-comprometimento
- Validar integridade dos dados restaurados

### 7. Post-Incident Review

- Responsavel: **IR Lead Agent**
- Conduzir blameless postmortem com todos os envolvidos
- Documentar lessons learned e action items
- Atualizar playbooks e detection rules conforme necessario

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Incidente P1 | Impacto critico em producao | Ativar war room e notificar C-level |
| Dados pessoais expostos | Indicios de data breach | Acionar equipe juridica e DPO |
| Adversario ativo | Atacante ainda presente | Priorizar containment sobre investigacao |
| Evidencia juridica | Possivel acao legal | Preservar chain of custody rigorosa |

## Outputs

- Incident report completo com timeline
- Root cause analysis documentado
- Action items de melhoria com owners e prazos
- Metricas de resposta (MTTD, MTTR, MTTC)
