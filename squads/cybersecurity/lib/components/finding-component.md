# Finding Component

Componente reutilizavel para documentacao padronizada de findings de seguranca.

## Estrutura do Finding

```
## [FINDING-ID]: [Title]

### Severity
[Critical | High | Medium | Low | Informational] (CVSS: X.X)

### Affected Asset
[Nome do ativo, URL, IP, recurso cloud]

### Description
[Descricao tecnica da vulnerabilidade em 2-3 paragrafos]

### Evidence
[Screenshots, requests/responses, logs, PoC code]

### Impact
[Impacto tecnico e de negocio se explorada]

### Remediation
[Passos especificos para correcao]

### References
[CVEs, CWEs, links para documentacao relevante]
```

## Campos Obrigatorios

- Finding ID unico seguindo convencao FIND-YYYY-NNN
- Titulo descritivo e conciso
- Severidade com score CVSS justificado
- Ativo afetado com localizacao precisa
- Evidencia reproduzivel
- Recomendacao de remediacao acionavel

## Boas Praticas

- Escrever titulos que comuniquem o risco, nao apenas o sintoma
- Incluir evidencia suficiente para reproducao independente
- Separar impacto tecnico de impacto de negocio
- Fornecer remediacao especifica, nao generica
- Referenciar CWE para categorizacao padronizada
- Incluir CVSS vector string para transparencia no calculo

## Exemplos de Titulos

- Bom: "SQL Injection permite extracao de dados de clientes via /api/search"
- Ruim: "SQL Injection encontrado"
- Bom: "Ausencia de rate limiting permite brute force em /login"
- Ruim: "Problema de autenticacao"
