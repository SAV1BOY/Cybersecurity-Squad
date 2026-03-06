# Framework Selection Guide

Guia para selecionar o framework de seguranca adequado para cada contexto e necessidade.

## Frameworks de Referencia

### MITRE ATT&CK
- **Quando usar**: Mapeamento de tecnicas de ataque, detection engineering, threat hunting, purple team
- **Foco**: Taticas, tecnicas e procedimentos (TTPs) de adversarios
- **Aplicacao no squad**: Base para medir cobertura de deteccao e priorizar development de rules

### NIST Cybersecurity Framework (CSF)
- **Quando usar**: Avaliacao geral de maturidade, comunicacao com executivos, roadmap estrategico
- **Foco**: Identify, Protect, Detect, Respond, Recover
- **Aplicacao no squad**: Estrutura para o quarterly security operating review

### NIST 800-53
- **Quando usar**: Definicao detalhada de controles, compliance governamental, ambientes regulados
- **Foco**: Controles de seguranca e privacidade abrangentes
- **Aplicacao no squad**: Referencia para security architecture reviews

### CIS Controls
- **Quando usar**: Priorizacao pratica de controles, ambientes com maturidade inicial
- **Foco**: Controles priorizados por eficacia e facilidade de implementacao
- **Aplicacao no squad**: Baseline de seguranca para novos sistemas

### ISO 27001/27002
- **Quando usar**: Certificacao, compliance internacional, gestao de seguranca da informacao
- **Foco**: Sistema de gestao de seguranca da informacao (SGSI)
- **Aplicacao no squad**: Base para compliance audits

### OWASP Top 10
- **Quando usar**: Seguranca de aplicacoes web, AppSec reviews, treinamento de desenvolvedores
- **Foco**: Vulnerabilidades mais criticas em aplicacoes web
- **Aplicacao no squad**: Referencia para DAST e code review

### STRIDE
- **Quando usar**: Threat modeling de aplicacoes e sistemas
- **Foco**: Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege
- **Aplicacao no squad**: Modelo principal para threat modeling sessions

## Matriz de Selecao

| Necessidade | Framework Recomendado |
|-------------|----------------------|
| Melhorar deteccao de ameacas | MITRE ATT&CK |
| Avaliar maturidade geral | NIST CSF |
| Definir controles detalhados | NIST 800-53 ou CIS Controls |
| Certificacao internacional | ISO 27001 |
| Seguranca de aplicacoes | OWASP Top 10 |
| Threat modeling | STRIDE ou PASTA |
| Cloud security | CIS Benchmarks + CSA CCM |
| Compliance regulatorio | Framework exigido pelo regulador |

## Combinacao de Frameworks

Na pratica, o squad utiliza multiplos frameworks de forma complementar:
- MITRE ATT&CK para operacoes de deteccao e hunting
- CIS Controls como baseline pratico
- NIST CSF para comunicacao estrategica
- OWASP para seguranca de aplicacoes
- ISO 27001 quando certificacao e requerida

## Criterios de Selecao

Ao escolher um framework, considere:
1. Requisitos regulatorios e contratuais aplicaveis
2. Maturidade atual do programa de seguranca
3. Audiencia e proposito da avaliacao
4. Recursos disponiveis para implementacao
5. Alinhamento com a industria e benchmarks do setor
