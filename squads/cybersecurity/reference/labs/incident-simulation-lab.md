# Incident Simulation Lab

## Objetivo
Ambiente para simulacao de incidentes de seguranca, pratica de resposta e
validacao de playbooks e procedimentos de IR.

## Tipos de Simulacao

### Tabletop Exercises
- Discussoes baseadas em cenarios sem execucao tecnica
- Participacao de stakeholders tecnicos e de negocio
- Foco em comunicacao, decisao e coordenacao
- Duracao: 1-2 horas por sessao

### Technical Simulations
- Execucao real de ataques no lab environment
- Resposta em tempo real pelo blue team
- Documentacao de timeline e decisoes
- Duracao: 4-8 horas por sessao

### Full-Scale Exercises
- Combinacao de tabletop e execucao tecnica
- Envolvimento de toda a equipe de seguranca
- Simulacao de comunicacao com stakeholders
- Duracao: 1-2 dias

## Cenarios Padrao

### Cenario 1: Ransomware Attack
- Initial access via phishing
- Lateral movement no Active Directory
- Data exfiltration pre-encryption
- Ransomware deployment
- Decisao: pagar ou nao pagar?
- Comunicacao com executivos e autoridades

### Cenario 2: Data Breach
- Descoberta de exfiltracao de dados
- Investigacao forense do incidente
- Avaliacao de dados comprometidos
- Notificacao LGPD (ANPD e titulares)
- Comunicacao publica e media handling

### Cenario 3: Insider Threat
- Deteccao de comportamento anomalo
- Investigacao sem alertar o suspeito
- Coleta de evidencias forenses
- Coordenacao com RH e juridico
- Acoes disciplinares e legais

### Cenario 4: Supply Chain Compromise
- Descoberta de backdoor em dependencia
- Avaliacao de blast radius
- Contenimento e remediacao
- Comunicacao com fornecedor
- Verificacao de integridade

### Cenario 5: Cloud Account Compromise
- Credenciais cloud comprometidas
- Investigacao de acoes do atacante
- Contenimento em ambiente cloud
- Revisao de IAM e access controls
- Hardening pos-incidente

## Metricas de Simulacao
- **MTTD**: Mean Time to Detect
- **MTTR**: Mean Time to Respond
- **Decision Quality**: qualidade das decisoes tomadas
- **Communication**: eficacia da comunicacao
- **Playbook Adherence**: aderencia aos playbooks
- **Gaps Identified**: lacunas descobertas

## Infraestrutura de Simulacao
- Ambiente AD Lab para cenarios Windows
- Cloud Lab para cenarios cloud
- Communication channels (Slack simulado, email)
- War room virtual ou fisico
- Timeline tracking tool

## Cadencia Recomendada
- Tabletop exercises: mensal
- Technical simulations: trimestral
- Full-scale exercises: semestral
- Post-simulation review: imediato

## Documentacao
- Template de cenario pre-exercise
- Formulario de observacoes durante exercise
- Template de after-action report
- Tracking de action items pos-exercise

## Notas do Squad
Simulacoes sao tao importantes quanto ferramentas. Praticar resposta a
incidentes regularmente reduz drasticamente o MTTR em incidentes reais.
