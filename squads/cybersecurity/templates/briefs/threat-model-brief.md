# Threat Model Brief

> Documento de escopo para modelagem de ameacas.
> Deve ser preenchido antes da sessao de threat modeling.

---

## 1. Informacoes do Projeto

- **Nome do Sistema / Aplicacao:** [NOME_DO_SISTEMA]
- **Versao:** [VERSAO_OU_RELEASE]
- **Owner do Produto:** [NOME_DO_PRODUCT_OWNER]
- **Arquiteto / Tech Lead:** [NOME_DO_TECH_LEAD]
- **Data da Sessao:** [DATA_PREVISTA]
- **Participantes:** [LISTA_DE_PARTICIPANTES]

## 2. Descricao do Sistema

[DESCREVA_O_PROPOSITO_DO_SISTEMA_FUNCIONALIDADES_PRINCIPAIS_E_CONTEXTO_DE_NEGOCIO]

## 3. Arquitetura de Alto Nivel

- **Tipo de aplicacao:** [WEB / MOBILE / API / MICROSERVICES / MONOLITO / IOT]
- **Stack tecnologico:** [LINGUAGENS_FRAMEWORKS_E_PLATAFORMAS]
- **Infraestrutura:** [ON_PREMISE / CLOUD_PROVIDER / HIBRIDO]
- **Diagrama de arquitetura:** [LINK_PARA_DIAGRAMA_OU_REFERENCIA]

## 4. Data Flow (Fluxo de Dados)

| Origem | Destino | Tipo de Dado | Protocolo | Criptografia |
|--------|---------|--------------|-----------|--------------|
| [COMPONENTE_ORIGEM] | [COMPONENTE_DESTINO] | [TIPO_DADO] | [HTTPS / gRPC / TCP] | [TLS / mTLS / NENHUMA] |
| [COMPONENTE_ORIGEM] | [COMPONENTE_DESTINO] | [TIPO_DADO] | [HTTPS / gRPC / TCP] | [TLS / mTLS / NENHUMA] |

## 5. Trust Boundaries

- [TRUST_BOUNDARY_1 — DESCRICAO]
- [TRUST_BOUNDARY_2 — DESCRICAO]
- [TRUST_BOUNDARY_3 — DESCRICAO]

## 6. Atores e Entry Points

| Ator | Nivel de Confianca | Entry Point | Autenticacao |
|------|--------------------|-------------|--------------|
| [USUARIO_FINAL] | [BAIXO / MEDIO / ALTO] | [WEB_UI / API_ENDPOINT] | [OAUTH / JWT / BASIC] |
| [ADMIN] | [ALTO] | [ADMIN_PANEL / SSH] | [MFA / CERTIFICADO] |

## 7. Dados Sensiveis

| Dado | Classificacao | Armazenamento | Regulamentacao |
|------|---------------|---------------|----------------|
| [TIPO_DE_DADO] | [PUBLICO / INTERNO / CONFIDENCIAL / RESTRITO] | [DB / S3 / FILESYSTEM] | [LGPD / PCI / HIPAA / NA] |

## 8. Metodologia

- **Framework:** [STRIDE / PASTA / ATTACK_TREES / LINDDUN / OUTRO]
- **Scope limitado a:** [COMPONENTES_OU_FUNCIONALIDADES_ESPECIFICAS]
- **Threat intelligence sources:** [MITRE_ATT&CK / OWASP / CUSTOM]

## 9. Premissas e Dependencias

- [PREMISSA_1]
- [PREMISSA_2]
- [DEPENDENCIA_EXTERNA_1]

## 10. Entregaveis Esperados

- [ ] Diagrama de Data Flow (DFD)
- [ ] Lista de threats identificadas
- [ ] Matriz de risco
- [ ] Recomendacoes de mitigacao
- [ ] [ENTREGAVEL_ADICIONAL]

---

*Template versao 1.0 — Cybersecurity Squad*
