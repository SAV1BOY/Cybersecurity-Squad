# Secure SDLC Policy Template

> Politica de desenvolvimento seguro de software.
> Define requisitos de seguranca em cada fase do ciclo de vida de desenvolvimento.

---

## 1. Informacoes do Documento

- **Titulo:** Politica de Secure SDLC
- **Versao:** [VERSAO]
- **Data de Vigencia:** [DATA]
- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Aprovado por:** [NOME_DO_APROVADOR]
- **Proxima Revisao:** [DATA_PROXIMA_REVISAO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DA_POLITICA_DE_DESENVOLVIMENTO_SEGURO]

## 3. Escopo

- **Aplica-se a:** [TODOS_OS_PROJETOS_DE_SOFTWARE / LISTA_ESPECIFICA]
- **Times cobertos:** [DESENVOLVIMENTO / DEVOPS / QA / PRODUTO]
- **Excecoes:** [EXCECOES_COM_APROVACAO_DE]

## 4. Requisitos por Fase

### 4.1 Requirements & Design

- [ ] Classificacao de dados processados pela aplicacao
- [ ] Security requirements definidos no backlog
- [ ] Threat modeling para features criticas: [CRITERIO_DE_OBRIGATORIEDADE]
- [ ] Privacy by design review (LGPD)
- [ ] Revisao de arquitetura de seguranca para novos servicos
- [ ] [REQUISITO_ADICIONAL]

### 4.2 Development

- [ ] Coding standards de seguranca seguidos: [REFERENCIA_GUIA]
- [ ] Secret management via [VAULT / SECRET_MANAGER]
- [ ] Input validation em todos os entry points
- [ ] Output encoding para prevencao de injection
- [ ] Uso de prepared statements para queries de banco
- [ ] Dependencias verificadas e atualizadas
- [ ] Pre-commit hooks de seguranca configurados
- [ ] [REQUISITO_ADICIONAL]

### 4.3 Code Review

- [ ] Security-focused code review obrigatorio para [CRITERIO]
- [ ] Checklist de seguranca utilizado: [REFERENCIA_CHECKLIST]
- [ ] Reviewer com treinamento de seguranca para PRs criticos
- [ ] Aprovacao obrigatoria do security champion para [CENARIOS]

### 4.4 Testing

- [ ] SAST executado em cada PR: [FERRAMENTA_SAST]
- [ ] SCA executado em cada PR: [FERRAMENTA_SCA]
- [ ] DAST executado em [FREQUENCIA]: [FERRAMENTA_DAST]
- [ ] Testes de seguranca automatizados no CI/CD
- [ ] Penetration testing antes de major releases: [CRITERIO]
- [ ] [REQUISITO_ADICIONAL]

### 4.5 Deployment

- [ ] Security gates no pipeline de CI/CD
- [ ] Criterios de bloqueio: [VULNERABILIDADES_CRITICAL_OU_HIGH_BLOQUEIAM]
- [ ] Container image scanning: [FERRAMENTA]
- [ ] Infrastructure as Code scanning: [FERRAMENTA]
- [ ] Secrets scanning no pipeline: [FERRAMENTA]
- [ ] Ambiente de producao hardened conforme baseline

### 4.6 Operations & Monitoring

- [ ] Security logging implementado
- [ ] Alertas de seguranca configurados
- [ ] Runtime application protection: [RASP / WAF]
- [ ] Vulnerability scanning periodico em producao
- [ ] [REQUISITO_ADICIONAL]

## 5. Security Champions

- Cada squad deve ter um security champion designado
- Responsabilidades: [LISTA_DE_RESPONSABILIDADES]
- Treinamento obrigatorio: [TREINAMENTO_REQUERIDO]
- Reuniao de security champions: [FREQUENCIA]

## 6. Treinamento

- **Treinamento obrigatorio para devs:** [PLATAFORMA_TREINAMENTO]
- **Frequencia:** [ANUAL / SEMESTRAL]
- **Topicos cobertos:** [OWASP_TOP_10 / SECURE_CODING / THREAT_MODELING]
- **Verificacao de conclusao:** [PROCESSO_DE_VERIFICACAO]

## 7. Ferramentas Obrigatorias

| Fase | Ferramenta | Responsavel | Obrigatorio |
|------|-----------|-------------|-------------|
| SAST | [FERRAMENTA] | [DEVSECOPS / APPSEC] | Sim |
| SCA | [FERRAMENTA] | [DEVSECOPS / APPSEC] | Sim |
| DAST | [FERRAMENTA] | [APPSEC] | [SIM / PARA_APPS_CRITICAS] |
| Secret Scanning | [FERRAMENTA] | [DEVSECOPS] | Sim |
| Container Scanning | [FERRAMENTA] | [DEVSECOPS] | [SIM / SE_APLICAVEL] |
| IaC Scanning | [FERRAMENTA] | [DEVSECOPS] | [SIM / SE_APLICAVEL] |

## 8. Metricas

| Metrica | Meta | Frequencia |
|---------|------|-----------|
| Cobertura SAST | [PERCENT]% dos repositorios | [FREQUENCIA] |
| Vulnerabilidades em producao | [META] | [FREQUENCIA] |
| MTTR de vulnerabilidades de codigo | [DIAS] | [FREQUENCIA] |
| Security champions ativos | [META] | [FREQUENCIA] |
| [METRICA_ADICIONAL] | [META] | [FREQUENCIA] |

## 9. Violacoes

O nao cumprimento desta politica pode resultar em [CONSEQUENCIAS].

## 10. Historico de Revisoes

| Versao | Data | Autor | Descricao |
|--------|------|-------|-----------|
| [VERSAO] | [DATA] | [NOME] | [DESCRICAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
