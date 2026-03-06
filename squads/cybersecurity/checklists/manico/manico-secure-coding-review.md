# Manico - Secure Coding Review

Checklist para revisao de codigo seguro conforme principios de Jim Manico.

## Preparacao da Review
- [ ] Linguagem e framework identificados para regras especificas
- [ ] SAST tool configurado para a linguagem alvo
- [ ] Threat model revisado para focar areas de risco
- [ ] Commit history analisado para mudancas recentes em areas criticas
- [ ] Code coverage do security review definida (full vs targeted)

## Input Handling
- [ ] Toda entrada de usuario validada no server-side
- [ ] Whitelist validation preferida sobre blacklist
- [ ] Input length limits definidos e enforced
- [ ] Content-type validation aplicada em uploads
- [ ] Encoding/decoding tratado consistentemente (UTF-8)
- [ ] Canonicalization aplicada antes de validation
- [ ] Regular expressions revisadas para ReDoS

## Output Encoding
- [ ] Context-aware output encoding implementado (HTML, JS, URL, CSS)
- [ ] Template engine com auto-escaping habilitado
- [ ] Raw/unescaped output justificado e revisado caso a caso
- [ ] API responses sem reflection de input nao sanitizado
- [ ] Log injection prevenido com output sanitization

## Database Interaction
- [ ] Parameterized queries/prepared statements em todo acesso a DB
- [ ] Nenhuma concatenacao de string em queries SQL
- [ ] ORM queries revisadas para injection via raw queries
- [ ] Stored procedures revisadas para dynamic SQL
- [ ] Database error handling sem information disclosure

## Cryptographic Implementation
- [ ] Bibliotecas criptograficas padrao utilizadas (nao custom crypto)
- [ ] Random number generation via CSPRNG
- [ ] Key derivation com funcao adequada (PBKDF2, scrypt, Argon2)
- [ ] IV/nonce generation correto e nao reutilizado
- [ ] Sensitive data cleared da memoria apos uso (se possivel)

## Error Handling e Logging
- [ ] Try/catch blocks em operacoes criticas
- [ ] Generic error messages para usuarios (detailed para logs)
- [ ] Sensitive data nunca logada (passwords, tokens, PII)
- [ ] Security events logados com contexto suficiente
- [ ] Log format estruturado para facil parsing

## Dependency Security
- [ ] Third-party libraries com versoes fixas (pinned)
- [ ] Known vulnerabilities em dependencies verificadas
- [ ] Unused dependencies removidas
- [ ] Lock files (package-lock, Pipfile.lock) commitados

## Documentacao
- [ ] Cada finding com line number e code snippet
- [ ] CWE mapping para cada finding
- [ ] Fix code example fornecido para cada finding
- [ ] Severity baseada em exploitability e impact
- [ ] Review summary com metricas (findings/KLOC)
