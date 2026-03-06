# Template Usage Guide

Guia para utilizar os templates padronizados do Cybersecurity Squad em entregas e documentacao.

## Principios de Uso

- Templates existem para garantir consistencia e qualidade
- Adapte o conteudo ao contexto, mas mantenha a estrutura
- Nao remova secoes obrigatorias, mesmo que o conteudo seja breve
- Use as phrases padronizadas sempre que aplicavel

## Templates Disponiveis

### Relatorio de Pentest
- **Uso**: Entrega final de penetration test
- **Secoes obrigatorias**: Executive summary, scope, methodology, findings, recommendations
- **Dica**: Cada finding deve ter severity, description, evidence e remediation

### Incident Report
- **Uso**: Documentacao pos-incidente
- **Secoes obrigatorias**: Timeline, impact, root cause, actions taken, lessons learned
- **Dica**: A timeline deve ser precisa com timestamps em UTC

### Security Architecture Review
- **Uso**: Resultado de review de arquitetura
- **Secoes obrigatorias**: System description, threat model, findings, decision
- **Dica**: Incluir diagramas atualizados do sistema revisado

### Risk Assessment
- **Uso**: Avaliacao formal de risco
- **Secoes obrigatorias**: Asset identification, threats, vulnerabilities, risk calculation
- **Dica**: Usar a matriz de risco padrao da organizacao

### Compliance Report
- **Uso**: Resultado de avaliacao de compliance
- **Secoes obrigatorias**: Scope, framework, control assessment, gaps, evidence
- **Dica**: Referenciar evidencias por ID no repositorio de evidencias

## Regras de Preenchimento

### Findings
Todo finding deve conter:
1. **Titulo** - Descritivo e unico
2. **Severidade** - Critical, High, Medium, Low, Informational
3. **Descricao** - O que foi encontrado e por que e um problema
4. **Evidencia** - Screenshots, logs ou outputs que comprovam o finding
5. **Impacto** - Consequencia potencial da exploracao
6. **Recomendacao** - Acao sugerida para correcao

### Executive Summary
- Maximo de uma pagina
- Linguagem acessivel para audiencia nao-tecnica
- Destacar os 3-5 pontos mais importantes
- Incluir recomendacao estrategica

### Metricas
- Sempre incluir periodo de referencia
- Comparar com periodo anterior quando disponivel
- Contextualizar numeros com narrativa explicativa

## Versionamento

- Templates sao versionados no repositorio do squad
- Sempre use a versao mais recente
- Mudancas em templates devem ser aprovadas pelo squad lead
- Versao do template deve constar no rodape do documento
