# Asset Inventory Tracker

> Inventario de ativos de TI para gerenciamento de seguranca.
> Base para vulnerability management, incident response e compliance.

---

## 1. Informacoes do Tracker

- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Ultima Atualizacao:** [DATA]
- **Ferramenta de Inventario:** [CMDB / SPREADSHEET / FERRAMENTA_ESPECIFICA]
- **Frequencia de Revisao:** [MENSAL / TRIMESTRAL]
- **Fonte de Discovery:** [AGENT / SCAN / MANUAL / API]

## 2. Resumo do Inventario

| Tipo de Ativo | Quantidade | Criticos | Com Owner | Cobertura EDR | Cobertura Vuln Scan |
|---------------|-----------|----------|-----------|---------------|---------------------|
| Servidores (fisicos) | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| Servidores (virtuais/cloud) | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| Endpoints (desktops) | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| Endpoints (laptops) | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| Dispositivos moveis | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| Aplicacoes web | [NUM] | [NUM] | [PERCENT]% | N/A | [PERCENT]% |
| APIs | [NUM] | [NUM] | [PERCENT]% | N/A | [PERCENT]% |
| Bancos de dados | [NUM] | [NUM] | [PERCENT]% | N/A | [PERCENT]% |
| Network devices | [NUM] | [NUM] | [PERCENT]% | N/A | [PERCENT]% |
| Containers / Kubernetes | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| [TIPO_ADICIONAL] | [NUM] | [NUM] | [PERCENT]% | [PERCENT]% | [PERCENT]% |
| **Total** | **[NUM]** | **[NUM]** | **[PERCENT]%** | **[PERCENT]%** | **[PERCENT]%** |

## 3. Classificacao de Criticidade

| Nivel | Criterios | Exemplos |
|-------|-----------|----------|
| Critico | [CRITERIOS_DE_CLASSIFICACAO] | [EXEMPLOS_DE_ATIVOS] |
| Alto | [CRITERIOS] | [EXEMPLOS] |
| Medio | [CRITERIOS] | [EXEMPLOS] |
| Baixo | [CRITERIOS] | [EXEMPLOS] |

## 4. Inventario Detalhado — Servidores

| Asset ID | Hostname | IP | OS | Versao | Ambiente | Criticidade | Owner | Funcao | EDR | Vuln Scan | Ultimo Patch |
|----------|----------|----|----|--------|----------|-------------|-------|--------|-----|-----------|-------------|
| [ID] | [HOSTNAME] | [IP] | [OS] | [VERSAO] | [PROD/STG/DEV] | [CRIT/ALTO/MED/BAIXO] | [NOME] | [FUNCAO] | [SIM/NAO] | [SIM/NAO] | [DATA] |
| [ID] | [HOSTNAME] | [IP] | [OS] | [VERSAO] | [AMBIENTE] | [CRITICIDADE] | [NOME] | [FUNCAO] | [SIM/NAO] | [SIM/NAO] | [DATA] |

## 5. Inventario Detalhado — Aplicacoes

| Asset ID | Nome | URL | Stack | Ambiente | Criticidade | Owner | Dados Sensiveis | SAST | DAST | Ultimo Assessment |
|----------|------|-----|-------|----------|-------------|-------|-----------------|------|------|-------------------|
| [ID] | [NOME] | [URL] | [STACK] | [AMBIENTE] | [CRITICIDADE] | [NOME] | [SIM/NAO — TIPO] | [SIM/NAO] | [SIM/NAO] | [DATA] |
| [ID] | [NOME] | [URL] | [STACK] | [AMBIENTE] | [CRITICIDADE] | [NOME] | [SIM/NAO — TIPO] | [SIM/NAO] | [SIM/NAO] | [DATA] |

## 6. Inventario Detalhado — Cloud Resources

| Asset ID | Provider | Account | Servico | Regiao | Criticidade | Owner | Tags | Ultimo Review |
|----------|----------|---------|---------|--------|-------------|-------|------|---------------|
| [ID] | [AWS/GCP/AZURE] | [ACCOUNT_ID] | [SERVICO] | [REGIAO] | [CRITICIDADE] | [NOME] | [TAGS] | [DATA] |

## 7. Ativos sem Owner

| Asset ID | Tipo | Hostname / Nome | Descoberto em | Acao Necessaria |
|----------|------|-----------------|---------------|-----------------|
| [ID] | [TIPO] | [IDENTIFICACAO] | [DATA] | [ACAO] |

## 8. Metricas do Inventario

| Metrica | Valor | Meta |
|---------|-------|------|
| Ativos com owner atribuido | [PERCENT]% | 100% |
| Cobertura de EDR | [PERCENT]% | [META]% |
| Cobertura de vulnerability scanning | [PERCENT]% | [META]% |
| Ativos com patch em dia | [PERCENT]% | [META]% |
| Shadow IT identificado no periodo | [NUM] | [META] |

---

*Template versao 1.0 — Cybersecurity Squad*
