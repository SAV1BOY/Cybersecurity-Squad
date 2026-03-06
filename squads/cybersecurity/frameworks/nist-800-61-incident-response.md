# NIST 800-61 — Incident Response Lifecycle

## Overview

O NIST Special Publication 800-61 (Computer Security Incident Handling Guide) fornece diretrizes para estabelecer um programa eficaz de resposta a incidentes de seguranca computacional. Publicado pelo National Institute of Standards and Technology, o documento define um ciclo de vida estruturado em quatro fases que orienta equipes de seguranca desde a preparacao ate a analise pos-incidente. E o padrao de referencia mais adotado globalmente para construcao de processos de Incident Response.

## Core Concepts

### Fases do IR Lifecycle

#### 1. Preparation

Fase dedicada a garantir que a organizacao esteja pronta para responder a incidentes de forma eficaz:

- Estabelecimento do Incident Response Team (IRT) com papeis e responsabilidades claros.
- Criacao e manutencao de playbooks para cenarios comuns (ransomware, phishing, data breach).
- Provisionamento de ferramentas forenses, canais de comunicacao seguros e ambientes de analise.
- Treinamento periodico e exercicios de tabletop para validar a prontidao da equipe.
- Documentacao de contatos de escalacao incluindo juridico, comunicacao e fornecedores externos.

#### 2. Detection and Analysis

Fase focada em identificar e confirmar a ocorrencia de incidentes de seguranca:

- Monitoramento continuo via SIEM, IDS/IPS, EDR e logs de aplicacao.
- Correlacao de alertas para distinguir falsos positivos de incidentes reais.
- Classificacao de incidentes por categoria (malware, unauthorized access, DoS, insider threat).
- Priorizacao baseada em impacto funcional, impacto informacional e capacidade de recuperacao.
- Documentacao inicial do incidente com timeline, sistemas afetados e indicadores de comprometimento (IoCs).

#### 3. Containment, Eradication and Recovery

Fase que abrange as acoes para limitar danos, eliminar a ameaca e restaurar operacoes:

- **Short-term Containment** — Isolamento imediato para impedir propagacao (network segmentation, account lockout).
- **Evidence Preservation** — Coleta forense antes de alteracoes no ambiente (memory dumps, disk images).
- **Long-term Containment** — Aplicacao de patches temporarios e controles compensatorios.
- **Eradication** — Remocao completa do artefato malicioso, backdoors e persistence mechanisms.
- **Recovery** — Restauracao de sistemas a partir de backups validados e monitoramento intensificado.

#### 4. Post-Incident Activity

Fase de aprendizado e melhoria continua apos o encerramento do incidente:

- Conducao de lessons learned meeting com todos os envolvidos em ate 5 dias uteis.
- Elaboracao do incident report final com root cause analysis e timeline detalhada.
- Atualizacao de playbooks, regras de deteccao e controles baseados nos findings.
- Retencao de evidencias conforme politica de retencao e requisitos legais.
- Calculo de metricas como MTTD (Mean Time to Detect) e MTTR (Mean Time to Respond).

### Severity Classification

| Nivel | Nome | Descricao |
|-------|------|-----------|
| SEV-1 | Critical | Comprometimento confirmado de dados sensiveis ou indisponibilidade de servico critico |
| SEV-2 | High | Ataque ativo com potencial de escalacao ou impacto significativo |
| SEV-3 | Medium | Atividade suspeita confirmada com impacto limitado |
| SEV-4 | Low | Evento de seguranca menor sem impacto operacional direto |

## Practical Application

### Construcao de um IR Plan

1. Obter sponsorship executivo e definir o charter do programa de IR.
2. Identificar os tipos de incidentes mais provaveis com base no threat landscape do setor.
3. Desenvolver playbooks especificos para cada categoria de incidente prioritaria.
4. Estabelecer SLAs de resposta por nivel de severidade alinhados ao apetite de risco.
5. Implementar canais de comunicacao redundantes para coordenacao durante crises.
6. Agendar exercicios trimestrais alternando entre tabletop e simulacao tecnica.
7. Revisar e atualizar o plano anualmente ou apos cada incidente significativo.

### Indicadores de Eficacia

- MTTD abaixo de 24 horas para incidentes de severidade alta e critica.
- MTTR abaixo de 72 horas para contencao completa.
- Taxa de falsos positivos escalados abaixo de 15 por cento.
- 100 por cento dos incidentes SEV-1 e SEV-2 com post-mortem documentado.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O ir-layer implementa diretamente as quatro fases descritas neste framework.
- Playbooks sao armazenados e versionados no repositorio do squad com templates padronizados.
- O detection-coverage-matrix alimenta a fase de Detection and Analysis com cobertura por tecnica MITRE.
- O evidence-standard define os procedimentos de coleta forense referenciados na fase de Containment.
- Metricas de MTTD e MTTR sao exibidas no security-kpi-dashboard para acompanhamento executivo.
- O vuln-triage-playbook conecta-se ao IR lifecycle quando vulnerabilidades exploradas ativamente sao identificadas.
- Lessons learned alimentam o backlog de melhoria continua do squad via refinamento quinzenal.
