# AppSec - ASVS Gate

Checklist de quality gate baseado no OWASP ASVS (Application Security Verification Standard).

## V1 - Architecture e Design
- [ ] Threat model atualizado para a aplicacao
- [ ] Security architecture documentada e revisada
- [ ] Trust boundaries identificados e documentados
- [ ] Input validation strategy definida centralmente
- [ ] Output encoding strategy definida centralmente
- [ ] Cryptographic strategy documentada

## V2 - Authentication
- [ ] Password storage com approved hash (Argon2id, bcrypt, scrypt)
- [ ] MFA disponivel para usuarios
- [ ] Brute force protection implementada
- [ ] Session fixation prevention implementada
- [ ] Credential recovery seguro (no security questions)
- [ ] Default credentials nao existem em nenhum componente

## V3 - Session Management
- [ ] Session IDs gerados com CSPRNG (128+ bits entropy)
- [ ] Session invalidation no logout funcional
- [ ] Idle timeout implementado (max 30 min)
- [ ] Absolute timeout implementado
- [ ] Cookie flags corretos (Secure, HttpOnly, SameSite)

## V4 - Access Control
- [ ] Access control enforced server-side
- [ ] Default deny policy implementada
- [ ] IDOR protection em todos os object references
- [ ] Directory traversal prevenido
- [ ] Rate limiting em funcoes sensiveis

## V5 - Input Validation
- [ ] Server-side validation para toda entrada
- [ ] Parameterized queries para database access
- [ ] Output encoding context-aware implementado
- [ ] File upload validation robusto
- [ ] HTTP header injection prevenida

## V7 - Error Handling e Logging
- [ ] Generic error messages para usuarios
- [ ] Security events logados adequadamente
- [ ] Sensitive data nao logada
- [ ] Log injection prevenido
- [ ] Centralized logging implementado

## V8 - Data Protection
- [ ] Sensitive data classificada e protegida
- [ ] PII handling conforme regulamentacao
- [ ] Cache-control headers para dados sensiveis
- [ ] HTTP security headers implementados
- [ ] Sensitive data cleared da memoria quando possivel

## V9 - Communications
- [ ] TLS 1.2+ enforced para todas as conexoes
- [ ] Certificate validation implementada
- [ ] HSTS habilitado com max-age adequado
- [ ] Mixed content prevenido

## ASVS Level Assessment
- [ ] ASVS Level 1 requirements verificados (baseline)
- [ ] ASVS Level 2 requirements verificados (standard apps)
- [ ] ASVS Level 3 requirements verificados (high-security apps)
- [ ] Coverage score calculado por capitulo
- [ ] Gaps documentados com remediation plan
- [ ] Report de compliance ASVS entregue
