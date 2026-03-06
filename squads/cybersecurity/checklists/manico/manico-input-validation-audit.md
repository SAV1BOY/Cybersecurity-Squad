# Manico - Input Validation Audit

Checklist para auditoria de validacao de entrada em aplicacoes.

## Inventario de Entry Points
- [ ] Todos os form fields catalogados com tipo de dado esperado
- [ ] URL parameters mapeados por endpoint
- [ ] HTTP headers processados pela aplicacao identificados
- [ ] Cookie values utilizados em logica de negocio listados
- [ ] File upload endpoints catalogados
- [ ] API request body schemas documentados
- [ ] WebSocket message formats identificados

## Validacao Server-Side
- [ ] Toda validacao ocorre no server-side (client-side e complementar)
- [ ] Whitelist validation aplicada onde possivel (allow-list)
- [ ] Data type validation enforced (string, integer, email, URL)
- [ ] Length limits definidos e enforced para cada campo
- [ ] Range validation para valores numericos
- [ ] Format validation para campos estruturados (date, phone, CPF)
- [ ] Canonicalization aplicada antes de validation (Unicode, encoding)

## Injection Prevention
- [ ] SQL injection: parameterized queries em todo database access
- [ ] XSS: output encoding context-aware implementado
- [ ] Command injection: exec/system calls com input sanitizado
- [ ] LDAP injection: escape de caracteres especiais LDAP
- [ ] XML injection: DTD processing desabilitado (XXE prevention)
- [ ] Path traversal: canonicalization + whitelist de paths
- [ ] SSTI: template injection prevenida com safe rendering

## File Upload Validation
- [ ] File type verificado por magic bytes (nao apenas extensao)
- [ ] File size limits enforced no server
- [ ] Filename sanitizado (caracteres especiais, path traversal)
- [ ] Upload directory fora do webroot
- [ ] Anti-virus scanning em uploads (se aplicavel)
- [ ] Content-Type do response configurado corretamente para downloads
- [ ] Image re-rendering para prevenir polyglot attacks

## Encoding e Serialization
- [ ] Character encoding definido explicitamente (UTF-8)
- [ ] Double encoding attacks prevenidos
- [ ] JSON deserialization segura (sem type gadgets)
- [ ] XML parsing segura (DTD/XXE desabilitado)
- [ ] YAML safe loading utilizado
- [ ] Protobuf/MessagePack validation implementada (se aplicavel)

## Testes e Validacao
- [ ] Fuzzing executado em inputs criticos
- [ ] Boundary testing realizado (min, max, empty, null, special chars)
- [ ] Unicode edge cases testados (homoglyphs, RTL, zero-width)
- [ ] Large payload testing executado (buffer overflow, DoS)
- [ ] Encoding bypass techniques testadas

## Documentacao
- [ ] Cada input sem validacao adequada documentado como finding
- [ ] Root cause identificado (missing validation, wrong validation)
- [ ] Code fix recommendation com exemplo funcional
- [ ] Input validation matrix criada (field x validation rules)
