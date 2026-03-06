# API Security Architecture

## Purpose

Comprehensive API security architecture covering authentication, authorization, rate limiting, input validation, encryption, monitoring, and gateway patterns. Addresses REST, GraphQL, gRPC, and WebSocket APIs.

## API Security Threat Landscape

| OWASP API Top 10 (2023) | Description | Primary Control |
|--------------------------|-------------|----------------|
| API1: Broken Object-Level Authorization | Accessing other users' objects by manipulating IDs | Object-level authorization checks |
| API2: Broken Authentication | Weak auth mechanisms, credential stuffing | Strong authentication, MFA for sensitive ops |
| API3: Broken Object Property-Level Authorization | Exposing sensitive properties, mass assignment | Response filtering, input allow-listing |
| API4: Unrestricted Resource Consumption | No rate limiting, query complexity limits | Rate limiting, resource quotas |
| API5: Broken Function-Level Authorization | Accessing admin functions as regular user | Role-based function authorization |
| API6: Unrestricted Access to Sensitive Business Flows | Automated abuse of business logic | Business logic rate limiting, bot detection |
| API7: Server-Side Request Forgery | API fetches attacker-controlled URLs | URL validation, allowlists, network segmentation |
| API8: Security Misconfiguration | Verbose errors, missing headers, open CORS | Hardened defaults, configuration scanning |
| API9: Improper Inventory Management | Shadow APIs, deprecated endpoints | API inventory, lifecycle management |
| API10: Unsafe Consumption of APIs | Trusting third-party API responses | Input validation on consumed APIs |

## Authentication Architecture

### Authentication Methods by Use Case

| Use Case | Method | Token Type | Lifetime |
|----------|--------|-----------|----------|
| User-facing API | OAuth 2.0 + PKCE | JWT access token | 15-60 minutes |
| Service-to-service | OAuth 2.0 client credentials | JWT access token | 5-15 minutes |
| Third-party integration | OAuth 2.0 authorization code | JWT access + refresh token | Access: 1hr, Refresh: 24hr |
| Webhook receiver | HMAC signature verification | N/A (signature per request) | N/A |
| Public API (read-only) | API key | Opaque key | Until rotated |
| Internal microservices | mTLS + service mesh | Certificate | Certificate validity |

### JWT Best Practices

| Requirement | Implementation |
|-------------|---------------|
| Algorithm | RS256 or ES256 (never HS256 with shared secrets for multi-party) |
| Expiration | Short-lived (15 min for access tokens) |
| Audience (aud) | Must validate against expected API identifier |
| Issuer (iss) | Must validate against trusted identity provider |
| Not Before (nbf) | Set to issuance time |
| JTI (token ID) | Include for revocation support |
| Signing key rotation | Support multiple keys via JWKS, rotate quarterly |
| Token storage (client) | HttpOnly, Secure, SameSite cookies (web) or secure storage (mobile) |

## Authorization Architecture

### Authorization Models

| Model | Granularity | Use Case | Implementation |
|-------|------------|----------|---------------|
| RBAC | Role-based | Standard user access | Role claims in JWT |
| ABAC | Attribute-based | Complex policies, multi-tenant | Policy engine (OPA, Cedar) |
| ReBAC | Relationship-based | Social, hierarchical data | Graph-based (Zanzibar, SpiceDB) |
| Scope-based | OAuth scopes | Third-party API access | Scope validation at gateway |

### Authorization Enforcement Points

```
Client -> API Gateway (scope/role check) -> Service (business logic auth) -> Data Layer (row-level)

Layer 1: Gateway - Validate token, check scopes, enforce rate limits
Layer 2: Service - Object-level authorization, business rules
Layer 3: Data - Row-level security, column-level filtering
```

### Object-Level Authorization Pattern

```
# WRONG: Trust client-provided ID without authorization check
GET /api/users/12345/records

# RIGHT: Verify requesting identity has access to the object
def get_records(user_id, requesting_identity):
    if not authz_service.can_access(requesting_identity, "records", user_id):
        return 403 Forbidden
    return records_service.get(user_id)
```

## Rate Limiting Strategy

### Rate Limit Tiers

| Tier | Applies To | Rate Limit | Burst | Response |
|------|-----------|-----------|-------|----------|
| Global | All requests | 10,000 req/min per IP | 200 req/sec | 429 Too Many Requests |
| Authenticated | Per user/API key | 1,000 req/min | 50 req/sec | 429 + Retry-After header |
| Sensitive endpoints | Login, password reset | 10 req/min per IP | 5 req/sec | 429 + progressive backoff |
| Write operations | POST, PUT, DELETE | 100 req/min | 20 req/sec | 429 + Retry-After |
| Search/query | Search endpoints | 30 req/min | 10 req/sec | 429 + Retry-After |

### Rate Limiting Headers

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 842
X-RateLimit-Reset: 1609459200
Retry-After: 30
```

## Input Validation

### Validation Layers

| Layer | Validation Type | Examples |
|-------|----------------|---------|
| Transport | Protocol compliance | TLS version, content-type, content-length |
| Schema | Structural validation | JSON Schema, OpenAPI spec validation, protobuf |
| Business | Semantic validation | Value ranges, enum values, cross-field consistency |
| Output | Response filtering | Remove sensitive fields, apply view-based projection |

### Validation Rules

| Input Type | Validation | Example |
|-----------|------------|---------|
| String | Length limits, character allowlist, encoding | name: maxLength 100, pattern: ^[a-zA-Z\s]+$ |
| Numeric | Range, type, precision | age: min 0, max 150, integer |
| Email | RFC 5322 format + domain validation | Standard email regex + MX check |
| URL | Scheme allowlist, SSRF prevention | Only https://, no internal IPs |
| Date | Format, range, logical consistency | ISO 8601, not in future (for DOB) |
| File upload | Type, size, content inspection | Allowed MIME types, max 10MB, magic byte check |
| Query parameters | Pagination limits, sort field allowlist | page_size: max 100, sort: enum values |
| GraphQL | Query depth, complexity, introspection control | Max depth 5, complexity score < 1000 |

## API Gateway Patterns

### Gateway Architecture

```
                     ┌──────────────────┐
  Client ──────────> │   API Gateway    │
                     │  ┌────────────┐  │
                     │  │ Auth       │  │  ──> Identity Provider
                     │  │ Rate Limit │  │
                     │  │ Validation │  │
                     │  │ Routing    │  │
                     │  │ Logging    │  │
                     │  └────────────┘  │
                     └──────┬───────────┘
                            │
              ┌─────────────┼─────────────┐
              v             v             v
         Service A     Service B     Service C
```

### Gateway Security Controls

| Control | Purpose | Configuration |
|---------|---------|---------------|
| TLS termination | Encrypt client traffic | TLS 1.2+ only, strong cipher suites |
| Authentication | Validate tokens | JWT validation with JWKS endpoint |
| Rate limiting | Prevent abuse | Per-client, per-endpoint limits |
| Request validation | Block malformed requests | OpenAPI spec enforcement |
| IP filtering | Block known-bad sources | Threat intelligence IP blocklists |
| CORS policy | Control cross-origin access | Explicit origin allowlist |
| Request/response logging | Audit trail | Structured logs, PII masking |
| WAF integration | Application-layer protection | OWASP CRS, custom rules |

## Monitoring and Observability

### API Security Monitoring

| Signal | Detection | Alert Threshold |
|--------|-----------|----------------|
| Authentication failures | Count per IP/user | >10 failures in 5 minutes |
| Authorization failures (403s) | Count per user | >5 per minute (BOLA attempt) |
| Rate limit violations (429s) | Count per client | Sustained hitting limits |
| Request size anomalies | Statistical deviation | >3 standard deviations |
| Response time anomalies | P99 latency spike | >2x baseline P99 |
| Error rate spike (5xx) | Percentage of requests | >5% error rate |
| New/unknown endpoints | Unseen URL patterns | Any hit to undocumented path |
| Sensitive data in response | DLP scanning | Any PII/secrets in non-designated endpoints |

### API Inventory Management

| Requirement | Implementation |
|-------------|---------------|
| API catalog | Central registry of all APIs (internal, external, partner) |
| Version tracking | Track all active versions, deprecation dates |
| Ownership | Every API has a designated owner and security contact |
| Classification | Data sensitivity classification per endpoint |
| Lifecycle status | Active, deprecated, retired, shadow |
| Dependency mapping | Upstream and downstream API dependencies |

## Cross-References

- [Application Threat Modeling](application-threat-modeling.md) -- API threat modeling
- [API Security Assessment Checklist](../checklists/api-security-assessment-quality.md) -- assessment quality
- [Web App Assessment Checklist](../checklists/web-app-assessment-quality.md) -- web application testing
- [Snort/Suricata Rules](../swipe/detection/snort-suricata-rules.md) -- network-level API monitoring
