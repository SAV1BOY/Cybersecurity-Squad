# Secure Coding Guides

Exemplos de guias de secure coding adaptados para times de desenvolvimento.

## Principios Fundamentais

1. **Input Validation** - Toda entrada externa e hostil ate prova contraria
2. **Output Encoding** - Encode dados antes de renderizar em qualquer contexto
3. **Authentication** - Implementar MFA e session management robusto
4. **Authorization** - Verificar permissoes em cada request server-side
5. **Cryptography** - Usar bibliotecas estabelecidas, nunca implementar propria

## Cheatsheet: Prevencao de Injection

```python
# ERRADO - SQL Injection vulneravel
query = f"SELECT * FROM users WHERE id = {user_input}"

# CORRETO - Parameterized query
cursor.execute("SELECT * FROM users WHERE id = %s", (user_input,))
```

```javascript
// ERRADO - XSS vulneravel
element.innerHTML = userInput;

// CORRETO - Safe DOM manipulation
element.textContent = userInput;
```

## Checklist por Linguagem

### Java/Spring
- Usar Prepared Statements para database queries
- Habilitar CSRF protection (Spring Security default)
- Configurar Content-Security-Policy headers
- Implementar rate limiting com bucket4j ou similar

### Python/Django
- ALLOWED_HOSTS configurado em producao
- Django ORM para queries (evitar raw SQL)
- SESSION_COOKIE_SECURE e CSRF_COOKIE_SECURE = True

## Integracao com CI/CD

- SAST scanning em cada pull request (Semgrep, SonarQube)
- Dependency scanning para vulnerabilidades conhecidas (Dependabot, Snyk)
- Secret scanning para prevenir commit de credentials
- Container image scanning antes de deploy
