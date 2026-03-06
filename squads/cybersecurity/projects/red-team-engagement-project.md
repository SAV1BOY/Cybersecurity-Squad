# Red Team Engagement Project

Template de projeto para operacoes de Red Team com objetivos definidos.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Tipo | Red Team Engagement |
| Objetivo | [Ex: Acessar dados financeiros do board] |
| Duracao | [4-8 semanas] |
| Equipe | [Red team operators] |
| Sponsor | [CISO / CTO] |
| Blue Team Awareness | [Informed / Uninformed] |

## Objetivos do Engagement

Diferente de pentest, red team tem objetivos especificos de negocio:
1. [Objetivo primario: ex. Exfiltrar dados de clientes]
2. [Objetivo secundario: ex. Comprometer email de executivo]
3. [Objetivo terciario: ex. Obter acesso a ambiente de producao]

## Fases

### 1. Planning (Semana 1)
- [ ] Definicao de objetivos com sponsor
- [ ] Threat intelligence para selecao de TTPs
- [ ] Threat profile: qual adversario estamos simulando
- [ ] Rules of engagement e limites eticos
- [ ] Infra de ataque (C2, domains, redirectors)

### 2. Initial Access (Semana 2-3)
- [ ] Phishing campaigns direcionadas
- [ ] External attack surface exploitation
- [ ] Physical security testing (se no escopo)
- [ ] Social engineering

### 3. Post-Exploitation (Semana 3-5)
- [ ] Persistence establishment
- [ ] Internal reconnaissance
- [ ] Privilege escalation
- [ ] Lateral movement
- [ ] Objective completion

### 4. Exfiltration & Impact (Semana 5-6)
- [ ] Data exfiltration (simulada)
- [ ] Demonstracao de impacto
- [ ] Documentacao de todo o attack path

### 5. Reporting & Purple Team (Semana 6-8)
- [ ] Relatorio de attack narrative
- [ ] Purple team sessions com blue team
- [ ] Identificacao de gaps de deteccao
- [ ] Recomendacoes priorizadas

## Metricas de Sucesso

- Objetivos atingidos vs. planejados
- Tempo ate deteccao pelo blue team
- Numero de tecnicas nao detectadas
- Controles que funcionaram vs. falharam

## OPSEC

Manter operational security durante o engagement.
Documentar todas as acoes com timestamps para deconfliction.
