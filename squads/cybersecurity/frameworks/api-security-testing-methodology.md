# API Security Testing Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de seguranca de APIs REST, GraphQL e gRPC. Cobre as
vulnerabilidades mais criticas segundo OWASP API Security Top 10, incluindo broken
authorization, injection e mass assignment. Testes somente em APIs autorizadas.

## Requisitos de Autorizacao
- Documentacao da API (OpenAPI/Swagger) e endpoints autorizados para teste
- Credenciais de teste com diferentes niveis de acesso fornecidas
- Rate limits temporariamente ajustados ou ambiente de staging dedicado
- Contato tecnico disponivel para suporte durante os testes
- Acordo sobre dados de teste (nunca usar dados reais de producao)

## Etapas da Metodologia

### 1. BOLA (Broken Object Level Authorization)
- Manipulacao de object IDs em requests para acessar recursos de outros usuarios
- Teste com IDs sequenciais, UUIDs previsíveis e encoded references
- Verificacao de authorization checks em cada endpoint individualmente
- Teste de horizontal privilege escalation entre contas de mesmo nivel

### 2. BFLA (Broken Function Level Authorization)
- Acesso a endpoints administrativos com credenciais de usuario regular
- Manipulacao de HTTP methods (GET para PUT/DELETE) em recursos restritos
- Teste de funcoes privilegiadas via parameter tampering
- Verificacao de role-based access control consistency

### 3. Authentication e Session Management
- Teste de brute force protection e account lockout policies
- Avaliacao de JWT implementation (algorithm confusion, weak signing)
- Verificacao de token expiration, refresh flow e revocation
- Teste de OAuth/OIDC flows para authorization code interception
- Analise de API key management e rotation policies

### 4. Rate Limiting e Resource Consumption
- Teste de rate limiting por endpoint, usuario e IP
- Avaliacao de proteção contra resource exhaustion (large payloads)
- GraphQL: teste de query depth limiting e complexity analysis
- Verificacao de pagination limits e batch operation controls

### 5. Schema Validation e Injection
- SQL injection via parametros de API (query, body, headers)
- NoSQL injection em APIs com backend MongoDB/DynamoDB
- Server-Side Request Forgery (SSRF) via parametros de URL
- XML External Entity (XXE) em APIs que aceitam XML
- GraphQL injection e introspection query abuse

### 6. Mass Assignment e Data Exposure
- Envio de campos nao documentados para modificar atributos protegidos
- Teste de excessive data exposure em responses da API
- Verificacao de campos sensiveis em error messages e debug info
- Analise de filtering e field selection em endpoints de listagem

### 7. Business Logic Testing
- Teste de fluxos de negocio para bypass de validacoes
- Race conditions em operacoes criticas (pagamentos, transferencias)
- Manipulacao de sequencia de chamadas em multi-step operations
- Teste de idempotency em operacoes que devem ser atomicas

## Ferramentas de Referencia
- Burp Suite, Postman, OWASP ZAP, Nuclei, ffuf, GraphQL Voyager
- Dredd (API contract testing), Schemathesis (property-based testing)

## Contrapartida de Deteccao (Blue Team)
- WAF rules especificas para API abuse patterns
- Monitoramento de anomalias em API call patterns e volumes
- Logging estruturado de todas as API requests com correlation IDs
- Alertas para tentativas de BOLA/BFLA baseados em access denied rates

## Integracao com Outros Frameworks
- Correlaciona com: credential-attack-methodology.md (API authentication)
- Correlaciona com: supply-chain-attack-defense.md (API dependencies)
- Alimenta: exfiltration-detection-methodology.md (data exposure via API)
- Reporta para: vulnerability management e API governance platform
