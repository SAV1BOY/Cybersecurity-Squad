# NIST 800-53 — Security and Privacy Controls

## Overview

O NIST Special Publication 800-53 Revision 5 fornece um catalogo abrangente de controles de seguranca e privacidade para sistemas de informacao e organizacoes federais. Com mais de 1000 controles organizados em 20 familias, e o framework de controles mais detalhado disponivel e serve como base para outros padroes como FedRAMP e FISMA. A Revisao 5 unificou controles de seguranca e privacidade em um unico catalogo integrado.

## Core Concepts

### Familias de Controles

Os controles sao organizados em 20 familias, cada uma representando uma area de seguranca:

| ID | Familia | Descricao |
|----|---------|-----------|
| AC | Access Control | Politicas e mecanismos de controle de acesso |
| AT | Awareness and Training | Conscientizacao e treinamento de seguranca |
| AU | Audit and Accountability | Registros de auditoria e rastreabilidade |
| CA | Assessment, Authorization and Monitoring | Avaliacao e autorizacao de sistemas |
| CM | Configuration Management | Gestao de configuracao e baselines |
| CP | Contingency Planning | Planos de contingencia e continuidade |
| IA | Identification and Authentication | Identificacao e autenticacao de usuarios |
| IR | Incident Response | Resposta a incidentes de seguranca |
| MA | Maintenance | Manutencao de sistemas |
| MP | Media Protection | Protecao de midias de armazenamento |
| PE | Physical and Environmental Protection | Seguranca fisica e ambiental |
| PL | Planning | Planejamento de seguranca |
| PM | Program Management | Gestao do programa de seguranca |
| PS | Personnel Security | Seguranca de pessoal |
| PT | PII Processing and Transparency | Processamento de dados pessoais |
| RA | Risk Assessment | Avaliacao de riscos |
| SA | System and Services Acquisition | Aquisicao de sistemas e servicos |
| SC | System and Communications Protection | Protecao de sistemas e comunicacoes |
| SI | System and Information Integrity | Integridade de sistemas e informacoes |
| SR | Supply Chain Risk Management | Gestao de risco da cadeia de suprimentos |

### Baselines de Controles

Tres baselines predefinidos agrupam controles por nivel de impacto:

- **Low Baseline** — Controles minimos para sistemas de baixo impacto. Aproximadamente 130 controles.
- **Moderate Baseline** — Controles para sistemas de impacto moderado. Aproximadamente 260 controles.
- **High Baseline** — Controles completos para sistemas de alto impacto. Aproximadamente 340 controles.

### Estrutura de um Controle

Cada controle possui os seguintes elementos:

- **Control Identifier** — Codigo unico (ex: AC-2, IA-5).
- **Control Name** — Nome descritivo do controle.
- **Control Text** — Descricao do que o controle requer.
- **Discussion** — Contexto adicional e orientacao de implementacao.
- **Related Controls** — Referencias cruzadas a controles complementares.
- **Control Enhancements** — Extensoes que adicionam funcionalidade ou rigor ao controle base.

## Practical Application

### Selecao e Tailoring de Controles

1. Categorizar o sistema utilizando FIPS 199 (Low, Moderate, High impact).
2. Selecionar o baseline apropriado com base na categorizacao do sistema.
3. Aplicar tailoring para adicionar ou remover controles conforme contexto organizacional.
4. Documentar justificativa para cada desvio do baseline em um Security Plan.
5. Implementar controles priorizando os de maior impacto na reducao de risco.
6. Avaliar eficacia dos controles periodicamente via assessment procedures (SP 800-53A).

### Mapeamento para Compliance

O NIST 800-53 mapeia diretamente para diversos padroes e regulamentacoes:

- **FedRAMP** utiliza baselines do 800-53 com controles adicionais especificos para cloud.
- **FISMA** requer implementacao de controles conforme categorizacao do sistema.
- **ISO 27001** possui mapeamento cruzado publicado pelo NIST para os controles do Annex A.
- **CIS Controls** sao um subconjunto priorizado dos controles do 800-53.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O governance-layer referencia as familias PM e PL para estruturacao de politicas de seguranca.
- O identity-layer implementa controles das familias AC e IA para gestao de acesso e autenticacao.
- O defense-layer mapeia controles das familias AU, SI e SC para monitoramento e protecao.
- O cloudsec-layer utiliza o baseline FedRAMP derivado do 800-53 para avaliacoes de provedores cloud.
- O risk-scoring-model considera o nivel de implementacao dos controles aplicaveis na pontuacao de risco.
- Evidencias de implementacao de controles sao coletadas conforme o evidence-standard do squad.
- O security-kpi-dashboard rastreia a porcentagem de controles implementados por baseline e familia.
- Gaps de controles identificados alimentam o backlog de seguranca priorizado pelo risk-scoring-model.
