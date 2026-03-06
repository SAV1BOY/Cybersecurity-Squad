# Detection Coverage Tracker

> Tracker de cobertura de deteccao mapeada ao MITRE ATT&CK.
> Utilizado para identificar gaps e priorizar desenvolvimento de regras.

---

## 1. Informacoes do Tracker

- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Ultima Atualizacao:** [DATA]
- **Framework de Referencia:** MITRE ATT&CK v[VERSAO]
- **Plataforma SIEM/EDR:** [FERRAMENTA]
- **Frequencia de Revisao:** [MENSAL / TRIMESTRAL]

## 2. Resumo de Cobertura

| Metrica | Valor |
|---------|-------|
| Total de Techniques no ATT&CK | [NUM] |
| Techniques com deteccao | [NUM] |
| Cobertura geral | [PERCENT]% |
| Regras ativas | [NUM] |
| Regras em desenvolvimento | [NUM] |
| Regras desativadas | [NUM] |

## 3. Cobertura por Tactic

| Tactic | ID | Techniques Total | Com Deteccao | Cobertura | Prioridade |
|--------|----|------------------|--------------|-----------|------------|
| Reconnaissance | TA0043 | [NUM] | [NUM] | [PERCENT]% | [ALTA/MEDIA/BAIXA] |
| Resource Development | TA0042 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Initial Access | TA0001 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Execution | TA0002 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Persistence | TA0003 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Privilege Escalation | TA0004 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Defense Evasion | TA0005 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Credential Access | TA0006 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Discovery | TA0007 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Lateral Movement | TA0008 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Collection | TA0009 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| C&C | TA0011 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Exfiltration | TA0010 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |
| Impact | TA0040 | [NUM] | [NUM] | [PERCENT]% | [PRIORIDADE] |

## 4. Detalhamento de Regras Ativas

| Rule ID | Nome | ATT&CK Technique | Data Source | Severidade | TP Rate |
|---------|------|-------------------|-------------|------------|---------|
| [RULE_ID] | [NOME_REGRA] | [TECHNIQUE_ID] | [DATA_SOURCE] | [SEV] | [PERCENT]% |
| [RULE_ID] | [NOME_REGRA] | [TECHNIQUE_ID] | [DATA_SOURCE] | [SEV] | [PERCENT]% |
| [RULE_ID] | [NOME_REGRA] | [TECHNIQUE_ID] | [DATA_SOURCE] | [SEV] | [PERCENT]% |

## 5. Gaps Prioritarios

| Technique ID | Nome | Tactic | Relevancia | Data Source Disponivel | Status |
|-------------|------|--------|------------|----------------------|--------|
| [TECH_ID] | [NOME] | [TACTIC] | [ALTA/MEDIA] | [SIM/NAO] | [BACKLOG / EM_DESENVOLVIMENTO] |
| [TECH_ID] | [NOME] | [TACTIC] | [ALTA/MEDIA] | [SIM/NAO] | [STATUS] |
| [TECH_ID] | [NOME] | [TACTIC] | [ALTA/MEDIA] | [SIM/NAO] | [STATUS] |

## 6. Regras em Desenvolvimento

| Rule ID | Nome | ATT&CK Technique | Responsavel | ETA | Status |
|---------|------|-------------------|-------------|-----|--------|
| [RULE_ID] | [NOME] | [TECHNIQUE_ID] | [NOME] | [DATA] | [EM_DEV / EM_TESTE] |
| [RULE_ID] | [NOME] | [TECHNIQUE_ID] | [NOME] | [DATA] | [STATUS] |

## 7. Data Sources

| Data Source | Status | Qualidade | Cobertura de Ativos |
|-------------|--------|-----------|---------------------|
| [WINDOWS_EVENT_LOGS] | [ATIVO / PARCIAL / AUSENTE] | [BOA / MEDIA / RUIM] | [PERCENT]% |
| [NETWORK_FLOW] | [STATUS] | [QUALIDADE] | [PERCENT]% |
| [CLOUD_AUDIT_LOGS] | [STATUS] | [QUALIDADE] | [PERCENT]% |
| [ENDPOINT_TELEMETRY] | [STATUS] | [QUALIDADE] | [PERCENT]% |
| [DNS_LOGS] | [STATUS] | [QUALIDADE] | [PERCENT]% |
| [DATA_SOURCE_ADICIONAL] | [STATUS] | [QUALIDADE] | [PERCENT]% |

## 8. Notas

[OBSERVACOES_SOBRE_GAPS_BLOQUEIOS_OU_PLANOS_DE_MELHORIA]

---

*Template versao 1.0 — Cybersecurity Squad*
