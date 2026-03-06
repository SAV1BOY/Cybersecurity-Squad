# Great Technical Findings

Exemplos de findings tecnicos bem escritos que equilibram detalhe tecnico com clareza.

## Estrutura de um Finding de Qualidade

1. **Title** - Descritivo e especifico (ex: "SQL Injection in /api/v2/users endpoint")
2. **Severity** - CVSS score com justificativa
3. **Description** - O que foi encontrado e por que importa
4. **Proof of Concept** - Steps to reproduce com evidencias
5. **Impact** - Consequencia tecnica e de negocio
6. **Remediation** - Fix especifico com code samples quando aplicavel
7. **References** - CWE, OWASP, CVE relacionados

## Exemplo: SQL Injection Finding

**Title:** Blind SQL Injection via `sort_by` Parameter
**Severity:** Critical (CVSS 9.1)
**Affected Asset:** api.exemplo.com.br/v2/users

**PoC Request:**
```http
GET /v2/users?sort_by=name'%20AND%20SLEEP(5)-- HTTP/1.1
```

**Impact:** Extracao completa do banco de dados, incluindo credentials e PII.

**Remediation:** Implementar parameterized queries e input validation com allowlist.

## Boas Praticas

- Screenshots e logs como evidencia irrefutavel
- Reprodutibilidade garantida por terceiros
- Vincular cada finding a um MITRE ATT&CK technique
- Distinguir entre validated e potential findings
- Incluir detection guidance para o blue team
