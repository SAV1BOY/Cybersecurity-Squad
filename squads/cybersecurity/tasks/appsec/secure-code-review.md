# Task: Secure Code Review

## Objetivo
Realizar revisao de seguranca do codigo-fonte de aplicacoes in-scope, identificando vulnerabilidades, padroes inseguros e violacoes de secure coding standards.

## Agents
- **jim-manico** (lead) — Conduz revisao de seguranca de codigo
- **command-generator** (support) — Gera comandos para analise automatizada

## Inputs
- Repositorios de codigo-fonte autorizados
- Threat model da aplicacao
- OWASP ASVS e secure coding guidelines aplicaveis
- Historico de vulnerabilidades da aplicacao

## Steps
1. Definir escopo do code review (modulos criticos, auth, crypto)
2. Executar SAST (Static Application Security Testing) automatizado
3. Revisar manualmente authentication e authorization logic
4. Auditar input validation e output encoding
5. Verificar implementacao de criptografia e key management
6. Analisar error handling e logging de seguranca
7. Verificar protecoes contra OWASP Top 10
8. Identificar hardcoded secrets e credenciais em codigo
9. Documentar findings com code snippets e recomendacoes
10. Registrar findings no `findings-registry`

## Output
- Relatorio de code review com findings classificados
- Lista de padroes inseguros identificados com exemplos
- Recomendacoes de remediacao com secure code examples
- Registro no `findings-registry`

## Quality Gates
- [ ] SAST executado e resultados triados
- [ ] Auth e authz logic revisados manualmente
- [ ] OWASP Top 10 verificado contra o codigo
- [ ] Hardcoded secrets identificados e reportados
- [ ] Findings tem code snippets e recomendacoes de fix
- [ ] Checklist `code-review-security-quality` atendido
- [ ] Checklist `manico-secure-coding-review` validado

## Routing & Escalation
- **frameworks**: owasp-asvs, appsec-layer, nist-ssdf
- **checklists**: code-review-security-quality, manico/manico-secure-coding-review, manico/manico-authn-authz-audit
- **templates**: reports/finding-template, reports/technical-report-template
- **registry**: data/registries/findings-registry
- **receives_from**: dev squad code review request
- **delivers_to**: findings-review
