# Incident Response Policy Template

> Politica de resposta a incidentes de seguranca da informacao.
> Define papeis, responsabilidades e processos para tratamento de incidentes.

---

## 1. Informacoes do Documento

- **Titulo:** Politica de Resposta a Incidentes
- **Versao:** [VERSAO]
- **Data de Vigencia:** [DATA]
- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Aprovado por:** [NOME_DO_APROVADOR]
- **Proxima Revisao:** [DATA_PROXIMA_REVISAO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DA_POLITICA_DE_INCIDENT_RESPONSE]

## 3. Escopo

- **Aplica-se a:** [TODOS_OS_COLABORADORES_TERCEIROS_E_PARCEIROS]
- **Cobre incidentes em:** [TODOS_OS_ATIVOS_E_DADOS_DA_ORGANIZACAO]
- **Excecoes:** [EXCECOES_SE_HOUVER]

## 4. Definicoes

| Termo | Definicao |
|-------|-----------|
| Evento de seguranca | [DEFINICAO] |
| Incidente de seguranca | [DEFINICAO] |
| Crise de seguranca | [DEFINICAO] |
| Incident Commander | [DEFINICAO] |
| [TERMO_ADICIONAL] | [DEFINICAO] |

## 5. Classificacao de Severidade

| Severidade | Criterios | Exemplos | Tempo de Resposta |
|------------|-----------|----------|-------------------|
| Critical (P1) | [CRITERIOS] | [EXEMPLOS] | [MINUTOS] |
| High (P2) | [CRITERIOS] | [EXEMPLOS] | [HORAS] |
| Medium (P3) | [CRITERIOS] | [EXEMPLOS] | [HORAS] |
| Low (P4) | [CRITERIOS] | [EXEMPLOS] | [HORAS_OU_DIAS] |

## 6. Papeis e Responsabilidades

| Papel | Responsavel | Responsabilidades |
|-------|-------------|-------------------|
| Incident Commander | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| SOC Analyst | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| IR Lead | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| CISO | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| DPO | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| Comunicacao | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| Juridico | [NOME_OU_ROLE] | [LISTA_DE_RESPONSABILIDADES] |
| [PAPEL_ADICIONAL] | [NOME_OU_ROLE] | [RESPONSABILIDADES] |

## 7. Fases da Resposta a Incidentes

### 7.1 Preparation (Preparacao)

- Manter runbooks atualizados para cenarios comuns
- Realizar exercicios de table-top: [FREQUENCIA]
- Manter ferramentas de IR operacionais
- Treinamento da equipe de IR: [FREQUENCIA]
- [ACAO_ADICIONAL]

### 7.2 Detection & Analysis (Deteccao e Analise)

- Canais de report: [EMAIL / TELEFONE / SLACK / PORTAL]
- Triagem inicial: [PROCESSO_DE_TRIAGEM]
- Classificacao e priorizacao conforme secao 5
- Documentacao em [FERRAMENTA_DE_TICKETS]

### 7.3 Containment (Contencao)

- Contencao de curto prazo: isolar ameaca imediata
- Contencao de longo prazo: solucao temporaria enquanto remedia
- Preservacao de evidencias antes de qualquer acao
- Decisao documentada pelo Incident Commander

### 7.4 Eradication (Erradicacao)

- Remocao da causa raiz
- Verificacao de completude
- Aplicacao de correcoes e patches

### 7.5 Recovery (Recuperacao)

- Restauracao de sistemas e servicos
- Monitoramento intensificado pos-recuperacao: [PERIODO]
- Validacao de funcionamento normal

### 7.6 Post-Incident (Pos-Incidente)

- Postmortem obrigatorio para incidentes P1 e P2: prazo de [DIAS]
- Lessons learned documentadas
- Action items trackeados ate conclusao
- Atualizacao de runbooks e controles

## 8. Comunicacao

### 8.1 Comunicacao Interna

| Severidade | Notificar | Canal | Frequencia de Updates |
|------------|-----------|-------|-----------------------|
| Critical | [LISTA] | [CANAL] | [FREQUENCIA] |
| High | [LISTA] | [CANAL] | [FREQUENCIA] |
| Medium | [LISTA] | [CANAL] | [FREQUENCIA] |

### 8.2 Comunicacao Externa

- Notificacao a ANPD (LGPD): conforme [PRAZO_LEGAL]
- Notificacao a clientes: conforme [CRITERIOS]
- Comunicacao publica: aprovada por [CARGO]
- Templates de comunicacao: [REFERENCIA]

## 9. Requisitos Legais e Regulatorios

- LGPD: [REQUISITOS_ESPECIFICOS]
- [REGULAMENTACAO]: [REQUISITOS]
- Preservacao de evidencias para possivel acao legal

## 10. Metricas

| Metrica | Meta |
|---------|------|
| MTTD | [HORAS] |
| MTTR | [HORAS] |
| Incidentes com postmortem | [PERCENT]% |
| Action items concluidos no prazo | [PERCENT]% |

## 11. Historico de Revisoes

| Versao | Data | Autor | Descricao |
|--------|------|-------|-----------|
| [VERSAO] | [DATA] | [NOME] | [DESCRICAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
