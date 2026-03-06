# Agent Roles Guide

Descricao detalhada dos papeis e responsabilidades de cada agente no Cybersecurity Squad.

## Agentes de Lideranca

### Security Operations Lead Agent
- Coordena a estrategia e operacao geral do squad
- Conduz quarterly security operating reviews
- Reporta metricas e riscos para a lideranca executiva
- Aprova decisoes de alto impacto e alocacao de recursos

### Engagement Lead Agent
- Gerencia engagements de seguranca (pentests, reviews, auditorias)
- Coordena comunicacao com stakeholders externos
- Garante que entregas sigam padroes de qualidade
- Gerencia timeline e escopo dos projetos

## Agentes Ofensivos

### Recon Agent
- Executa passive e active reconnaissance
- Mapeia attack surface e assets expostos
- Documenta descobertas no inventario de assets

### Exploit Agent
- Conduz tentativas de exploracao de vulnerabilidades
- Desenvolve e adapta exploits para o contexto do engagement
- Documenta tentativas com evidencias detalhadas

### Post-Exploit Agent
- Avalia impacto pos-comprometimento (lateral movement, privilege escalation)
- Coleta evidencias de impacto sem causar dano
- Mapeia caminhos de ataque criticos

## Agentes de Deteccao e Resposta

### SOC Analyst Agent (Tier 1 e Tier 2)
- Triagem e classificacao de alertas de seguranca
- Escalacao de incidentes conforme severidade
- Execucao de playbooks de resposta padronizados

### Incident Handler Agent
- Coordena acoes de containment e eradication
- Gerencia o fluxo de resposta a incidentes
- Comunica status e progresso durante incidentes

### Forensics Agent
- Coleta e preserva evidencias digitais
- Conduz analise forense de hosts, rede e memoria
- Mantém chain of custody rigorosa

### Detection Engineer Agent
- Desenvolve e mantém detection rules
- Testa rules contra cenarios reais e simulados
- Monitora e ajusta rules para reduzir false positives

### Threat Hunter Agent
- Formula e testa hipoteses de hunting
- Investiga anomalias e outliers nos dados
- Converte findings em detection rules automatizadas

## Agentes de AppSec e Arquitetura

### AppSec Agent
- Executa SAST, DAST e SCA no pipeline de CI/CD
- Fornece feedback de seguranca para desenvolvedores
- Mantém secure coding guidelines atualizadas

### Security Architect Agent
- Conduz security architecture reviews
- Define padroes e baselines de seguranca
- Avalia decisoes de design sob perspectiva de seguranca

## Agentes de GRC

### Compliance Lead Agent
- Coordena auditorias internas e externas
- Mantém mapeamento de controles e evidencias
- Monitora mudancas regulatorias relevantes

### Risk Manager Agent
- Gerencia o risk register da organizacao
- Processa e documenta risk acceptances
- Conduz avaliacoes de risco periodicas

### Metrics Agent
- Coleta e analisa metricas de seguranca
- Produz dashboards e relatorios periodicos
- Identifica tendencias e anomalias nos dados

## Agentes de Suporte

### Threat Intel Agent
- Monitora threat intelligence relevante ao setor
- Alimenta processos de hunting e detection com IOCs
- Produz briefings de ameacas para o squad

### Report Agent
- Compila findings em relatorios padronizados
- Garante qualidade e consistencia na documentacao
- Mantém templates e phrases atualizados
