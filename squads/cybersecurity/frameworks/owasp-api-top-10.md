# OWASP API Security Top 10

## Overview

O OWASP API Security Top 10 e um documento de conscientizacao focado exclusivamente nos riscos de seguranca mais criticos em APIs (Application Programming Interfaces). Com a adocao massiva de arquiteturas baseadas em microservicos e APIs REST/GraphQL, a superficie de ataque migrou significativamente para endpoints de API. A versao 2023 revisou completamente a lista, substituindo cinco categorias e refinando as demais para refletir o cenario atual de ameacas em APIs.

## Core Concepts

### As 10 Categorias de Risco (2023)

#### API1:2023 — Broken Object Level Authorization (BOLA)

Falha mais prevalente em APIs onde endpoints que recebem IDs de objetos nao verificam se o usuario autenticado possui permissao para acessar o recurso solicitado. Atacantes manipulam IDs em requests para acessar dados de outros usuarios. Equivalente a IDOR no contexto de APIs.

#### API2:2023 — Broken Authentication

Mecanismos de autenticacao implementados incorretamente em APIs. Inclui tokens sem expiracao, ausencia de rate limiting em login, JWT sem validacao de assinatura e credenciais trafegadas sem TLS.

#### API3:2023 — Broken Object Property Level Authorization

Combinacao dos antigos Excessive Data Exposure e Mass Assignment. A API expoe propriedades de objetos que o usuario nao deveria visualizar ou permite modificacao de propriedades que deveriam ser somente leitura.

#### API4:2023 — Unrestricted Resource Consumption

Ausencia de limites no consumo de recursos da API. Inclui falta de rate limiting, limites de paginacao, upload de arquivos sem restricao de tamanho e operacoes computacionalmente caras sem throttling.

#### API5:2023 — Broken Function Level Authorization

Falhas na autorizacao em nivel de funcao onde usuarios regulares conseguem acessar endpoints administrativos. Frequente quando a separacao entre funcoes regulares e privilegiadas e feita apenas no client-side.

#### API6:2023 — Unrestricted Access to Sensitive Business Flows

Categoria nova que aborda automacao excessiva de fluxos de negocio sensiveis como compra de ingressos, criacao de contas em massa ou scraping sistematico. A API nao implementa mecanismos anti-automacao adequados.

#### API7:2023 — Server Side Request Forgery (SSRF)

Ocorre quando a API busca recursos remotos com base em URLs fornecidas pelo usuario sem validacao adequada. Pode permitir acesso a servicos internos, metadata de cloud providers e recursos de rede privada.

#### API8:2023 — Security Misconfiguration

Configuracoes inseguras no stack da API incluindo CORS permissivo, headers de seguranca ausentes, mensagens de erro detalhadas, TLS desatualizado e permissoes excessivas em cloud resources.

#### API9:2023 — Improper Inventory Management

Falta de inventario atualizado de APIs expostas. Inclui versoes antigas ainda ativas, endpoints de debug em producao, documentacao desatualizada e shadow APIs nao catalogadas.

#### API10:2023 — Unsafe Consumption of APIs

Categoria nova focada no risco de consumir APIs de terceiros sem validacao adequada. Dados recebidos de APIs externas sao tratados como confiaveis sem sanitizacao, podendo introduzir vulnerabilidades como injection.

## Practical Application

### Controles de Seguranca por Categoria

| Risco | Controle Primario | Implementacao |
|-------|-------------------|---------------|
| API1 | Object-level authorization checks | Verificar ownership em cada request no server-side |
| API2 | Strong authentication | OAuth 2.0 com PKCE, token rotation, MFA |
| API3 | Schema-based response filtering | Definir allow-list de campos por role |
| API4 | Rate limiting e quotas | API Gateway com throttling por consumer |
| API5 | RBAC consistente | Middleware de autorizacao centralizado |
| API6 | Anti-automation | CAPTCHA, device fingerprinting, anomaly detection |
| API7 | URL validation | Allow-list de destinos, bloquear metadata endpoints |
| API8 | Hardening | Security headers, CORS restritivo, error handling |
| API9 | API inventory | Service mesh, API Gateway catalog, deprecation policy |
| API10 | Input validation | Tratar dados de APIs externas como untrusted input |

### Testes de Seguranca em APIs

1. Mapear todos os endpoints e metodos HTTP com ferramentas de API discovery.
2. Testar BOLA sistematicamente alternando tokens de autorizacao entre usuarios.
3. Validar autenticacao com tokens expirados, malformados e de outros contextos.
4. Verificar mass assignment enviando propriedades adicionais em requests PUT/PATCH.
5. Testar rate limiting com requests automatizados em alta velocidade.
6. Verificar autorizacao horizontal e vertical em todos os endpoints privilegiados.
7. Testar SSRF com URLs internas e metadata endpoints de cloud providers.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer inclui testes especificos do API Top 10 em todo assessment de API.
- O offense-layer utiliza a lista como checklist obrigatorio em pentests de microservicos.
- O finding-structure-standard mapeia categorias do API Top 10 para classificacao de findings em APIs.
- O discovery-layer mantem inventario de APIs expostas conforme recomendacao de API9.
- O defense-layer configura API Gateways com controles de rate limiting e autenticacao centralizados.
- O bug-bounty-framework define recompensas especificas para vulnerabilidades BOLA e authentication bypass.
- O owasp-asvs complementa com requisitos detalhados de verificacao para APIs em cada nivel.
