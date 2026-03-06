# OWASP ASVS — Application Security Verification Standard

## Overview

O OWASP Application Security Verification Standard (ASVS) fornece uma base para testar controles tecnicos de seguranca em aplicacoes web e estabelece requisitos de desenvolvimento seguro. Na versao 4.0, o ASVS contem 286 requisitos de verificacao organizados em 14 capitulos, com tres niveis de profundidade. E utilizado como referencia para definir escopo de pentests, requisitos de seguranca para fornecedores e criterios de aceitacao em programas de AppSec.

## Core Concepts

### Niveis de Verificacao

- **Level 1 (Opportunistic)** — Defesas contra vulnerabilidades facilmente descobertas. Adequado para aplicacoes de baixo risco. Pode ser verificado via pentest externo sem acesso ao codigo.
- **Level 2 (Standard)** — Defesas contra a maioria dos riscos em aplicacoes que processam dados sensiveis. Requer acesso ao codigo fonte e ambiente de teste. Recomendado para a maioria das aplicacoes.
- **Level 3 (Advanced)** — Nivel mais alto para aplicacoes criticas que processam dados altamente sensiveis como saude, financeiro e infraestrutura critica. Requer design review, threat modeling e code review profundo.

### Capitulos de Requisitos

| Cap | Titulo | Foco |
|-----|--------|------|
| V1 | Architecture, Design and Threat Modeling | Arquitetura segura e modelagem de ameacas |
| V2 | Authentication | Verificacao de identidade e gestao de credenciais |
| V3 | Session Management | Gerenciamento seguro de sessoes |
| V4 | Access Control | Controle de acesso e autorizacao |
| V5 | Validation, Sanitization and Encoding | Tratamento de entrada e saida de dados |
| V6 | Stored Cryptography | Criptografia em repouso |
| V7 | Error Handling and Logging | Tratamento de erros e registro de eventos |
| V8 | Data Protection | Protecao de dados em transito e classificacao |
| V9 | Communication | Seguranca de comunicacoes e TLS |
| V10 | Malicious Code | Deteccao de codigo malicioso e backdoors |
| V11 | Business Logic | Seguranca de logica de negocio |
| V12 | Files and Resources | Upload de arquivos e gestao de recursos |
| V13 | API and Web Service | Seguranca de APIs REST, SOAP e GraphQL |
| V14 | Configuration | Configuracao segura de build e deploy |

### Estrutura de um Requisito

Cada requisito possui identificador unico, descricao, nivel aplicavel e mapeamento CWE:

- **Identificador** — Formato V{capitulo}.{secao}.{numero} (ex: V2.1.1).
- **Descricao** — Requisito verificavel em linguagem clara e objetiva.
- **L1/L2/L3** — Indicacao de em quais niveis o requisito e obrigatorio.
- **CWE** — Mapeamento para Common Weakness Enumeration correspondente.

## Practical Application

### Uso como Requisitos de Seguranca

1. Selecionar o nivel adequado baseado na classificacao de risco da aplicacao.
2. Extrair requisitos aplicaveis como user stories de seguranca para o backlog.
3. Incluir requisitos ASVS como criterio de aceitacao em features que envolvam autenticacao, autorizacao e tratamento de dados.
4. Validar conformidade durante code review com checklists derivados do ASVS.
5. Utilizar requisitos como escopo tecnico em contratos com fornecedores de pentest.

### Uso como Escopo de Pentest

- **Pentest Level 1** — Teste black-box focado em vulnerabilidades exploraveis externamente.
- **Pentest Level 2** — Teste grey-box com acesso a documentacao e credenciais de teste.
- **Pentest Level 3** — Teste white-box com acesso completo ao codigo fonte e arquitetura.

### Mapeamento de Ferramentas

| Capitulo | Teste Automatizado | Teste Manual |
|----------|--------------------|--------------|
| V2-V4 | Burp Suite, OWASP ZAP | Authentication testing manual |
| V5 | SAST (Semgrep, CodeQL) | Input validation review |
| V6 | Secret scanning, crypto linters | Cryptographic design review |
| V7 | Log analysis tools | Error handling audit |
| V13 | API fuzzing (RESTler) | Business logic testing |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer adota ASVS Level 2 como padrao minimo para aplicacoes que processam dados de clientes.
- O offense-layer utiliza o ASVS como escopo tecnico detalhado em engagements de pentest.
- O finding-structure-standard referencia requisitos ASVS especificos em cada finding para facilitar remediacao.
- O security-champion-program inclui treinamento nos capitulos ASVS mais relevantes para cada squad de desenvolvimento.
- O owasp-top-10 e coberto integralmente pelos requisitos ASVS, que expandem cada categoria com verificacoes granulares.
- O retest-method valida remediacao contra o requisito ASVS especifico violado no finding original.
- Dashboards de conformidade ASVS por aplicacao sao exibidos no security-kpi-dashboard.
- O bug-bounty-framework referencia requisitos ASVS para definir escopo tecnico detalhado.
