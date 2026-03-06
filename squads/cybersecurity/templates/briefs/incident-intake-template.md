# Incident Intake Template

> Formulario de registro inicial de incidentes de seguranca.
> Preencha o mais rapido possivel ao identificar um potencial incidente.

---

## 1. Identificacao do Incidente

- **Incident ID:** [AUTO_GERADO_OU_MANUAL]
- **Data/Hora da Deteccao:** [YYYY-MM-DD HH:MM UTC]
- **Reportado por:** [NOME_DO_REPORTER]
- **Canal de Report:** [EMAIL / SIEM / ALERTA / TELEFONE / OUTRO]
- **Severidade Inicial:** [CRITICAL / HIGH / MEDIUM / LOW]

## 2. Classificacao Preliminar

- **Tipo de Incidente:** [PHISHING / MALWARE / DATA_BREACH / UNAUTHORIZED_ACCESS / DDOS / INSIDER_THREAT / OUTRO]
- **Categoria NIST:** [IDENTIFY / PROTECT / DETECT / RESPOND / RECOVER]
- **Vetor de Ataque Suspeito:** [EMAIL / WEB / REDE / FISICO / SUPPLY_CHAIN / DESCONHECIDO]

## 3. Descricao do Incidente

[DESCREVA_O_INCIDENTE_COM_O_MAXIMO_DE_DETALHES_POSSIVEIS_INCLUINDO_O_QUE_FOI_OBSERVADO_E_QUANDO]

## 4. Sistemas Afetados

| Sistema / Ativo | IP / Hostname | Criticidade | Status Atual |
|-----------------|---------------|-------------|--------------|
| [SISTEMA_1] | [IP_HOSTNAME] | [CRITICO / ALTO / MEDIO] | [ONLINE / OFFLINE / ISOLADO] |
| [SISTEMA_2] | [IP_HOSTNAME] | [CRITICO / ALTO / MEDIO] | [ONLINE / OFFLINE / ISOLADO] |

## 5. Impacto Preliminar

- **Usuarios afetados:** [NUMERO_OU_GRUPO]
- **Dados comprometidos:** [SIM / NAO / EM_INVESTIGACAO]
- **Tipo de dados:** [PII / FINANCEIRO / CREDENCIAIS / PROPRIEDADE_INTELECTUAL / NA]
- **Servicos impactados:** [LISTA_DE_SERVICOS]
- **Impacto no negocio:** [DESCRICAO_DO_IMPACTO]

## 6. Acoes Imediatas Tomadas

- [ ] [ACAO_1_DESCRICAO]
- [ ] [ACAO_2_DESCRICAO]
- [ ] [ACAO_3_DESCRICAO]

## 7. Evidencias Iniciais

| Tipo | Descricao | Localizacao | Hash (se aplicavel) |
|------|-----------|-------------|---------------------|
| [LOG / SCREENSHOT / PCAP / ARTEFATO] | [DESCRICAO] | [CAMINHO_OU_URL] | [SHA256_HASH] |

## 8. Escalacao

- **Incident Commander designado:** [NOME]
- **Equipes notificadas:** [SOC / IR_TEAM / DEVOPS / LEGAL / MANAGEMENT]
- **Necessita escalacao externa:** [SIM / NAO]
- **Autoridades notificadas:** [SIM / NAO / NA]

## 9. Proximos Passos

- [ ] [PROXIMO_PASSO_1]
- [ ] [PROXIMO_PASSO_2]
- [ ] [PROXIMO_PASSO_3]

---

*Template versao 1.0 — Cybersecurity Squad*
