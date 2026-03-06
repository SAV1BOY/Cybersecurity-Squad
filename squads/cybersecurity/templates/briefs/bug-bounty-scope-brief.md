# Bug Bounty Scope Brief

> Documento de definicao de escopo e regras para programas de bug bounty.
> Deve ser revisado e atualizado a cada ciclo do programa.

---

## 1. Informacoes do Programa

- **Nome do Programa:** [NOME_DO_PROGRAMA]
- **Responsavel pelo Programa:** [NOME_DO_RESPONSAVEL]
- **Plataforma:** [HACKERONE / BUGCROWD / INTIGRITI / PRIVADO]
- **Tipo:** [PUBLICO / PRIVADO / VDP]
- **Data de Lancamento:** [DATA]
- **Status:** [ATIVO / PAUSADO / EM_REVISAO]

## 2. Objetivo do Programa

[DESCREVA_O_OBJETIVO_DO_PROGRAMA_E_O_QUE_SE_ESPERA_DOS_PESQUISADORES]

## 3. In-Scope Assets

| Asset | Tipo | Criticidade | Elegivel para Bounty |
|-------|------|-------------|----------------------|
| [URL_OU_APP] | [WEB / MOBILE / API / HARDWARE] | [CRITICO / ALTO / MEDIO] | [SIM / NAO] |
| [URL_OU_APP] | [WEB / MOBILE / API / HARDWARE] | [CRITICO / ALTO / MEDIO] | [SIM / NAO] |
| [URL_OU_APP] | [WEB / MOBILE / API / HARDWARE] | [CRITICO / ALTO / MEDIO] | [SIM / NAO] |

## 4. Out-of-Scope

- [ATIVO_FORA_DO_ESCOPO_1]
- [ATIVO_FORA_DO_ESCOPO_2]
- Ambientes de terceiros e servicos SaaS
- [EXCLUSAO_ADICIONAL]

## 5. Vulnerabilidades Elegiveis

### 5.1 In-Scope Vulnerability Types

- [ ] Remote Code Execution (RCE)
- [ ] SQL Injection
- [ ] Authentication Bypass
- [ ] IDOR / Broken Access Control
- [ ] XSS (Stored / Reflected)
- [ ] SSRF
- [ ] [TIPO_ADICIONAL]

### 5.2 Out-of-Scope Vulnerability Types

- Self-XSS sem impacto demonstravel
- Rate limiting em endpoints nao criticos
- Missing security headers sem impacto
- [EXCLUSAO_DE_VULN_ADICIONAL]

## 6. Tabela de Recompensas

| Severidade | Faixa de Valor | Exemplos |
|------------|----------------|----------|
| Critical | [VALOR_MIN] - [VALOR_MAX] | RCE, Auth Bypass em admin |
| High | [VALOR_MIN] - [VALOR_MAX] | SQLi, SSRF com impacto |
| Medium | [VALOR_MIN] - [VALOR_MAX] | Stored XSS, IDOR |
| Low | [VALOR_MIN] - [VALOR_MAX] | Reflected XSS, info disclosure |

## 7. Regras do Programa

- Nao realizar ataques de DoS/DDoS
- Nao acessar dados de outros usuarios
- Reports devem incluir PoC funcional
- Tempo de resposta inicial: [HORAS_SLA]
- Tempo de triagem: [DIAS_SLA]
- [REGRA_ADICIONAL]

## 8. Processo de Triagem

- **Time de triagem:** [INTERNO / PLATAFORMA / HIBRIDO]
- **SLA de primeira resposta:** [HORAS]
- **SLA de resolucao:** [DIAS_POR_SEVERIDADE]
- **Escalacao:** [PROCESSO_DE_ESCALACAO]

## 9. Contatos

- **Programa Manager:** [EMAIL]
- **Triagem:** [EMAIL_OU_CANAL]
- **Escalacao:** [EMAIL_OU_CANAL]

---

*Template versao 1.0 — Cybersecurity Squad*
