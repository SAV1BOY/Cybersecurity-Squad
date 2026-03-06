# Security Logging Patterns

## Purpose

Reference patterns for implementing security-focused logging. Covers what to log, what to explicitly exclude, structured logging formats, correlation ID implementation, tamper evidence, and log pipeline security for building auditable, forensic-ready systems.

## What to Log (Security Events)

### Authentication and Authorization

| Event | Required Fields | Severity |
|-------|----------------|----------|
| Successful login | user_id, source_ip, auth_method, timestamp | Info |
| Failed login | username_attempted, source_ip, failure_reason, timestamp | Warning |
| Account lockout | user_id, source_ip, attempt_count, timestamp | Warning |
| Privilege escalation | user_id, old_role, new_role, granted_by, timestamp | Warning |
| Password change | user_id, source_ip, timestamp | Info |
| MFA enrollment/removal | user_id, mfa_type, action, admin_id, timestamp | Warning |
| API key creation/revocation | user_id, key_id (partial), scope, timestamp | Info |
| Session creation/termination | session_id, user_id, source_ip, timestamp | Info |
| Authorization denial | user_id, resource, action, policy_reason, timestamp | Warning |

### Data Access and Modification

| Event | Required Fields | Severity |
|-------|----------------|----------|
| Sensitive data access | user_id, resource_type, record_id, timestamp | Info |
| Bulk data export | user_id, record_count, export_format, timestamp | Warning |
| Data modification | user_id, resource, field_changed, timestamp | Info |
| Data deletion | user_id, resource, record_id, timestamp | Warning |
| Admin action | admin_id, action, target, before_state, after_state, timestamp | Warning |

### System and Infrastructure

| Event | Required Fields | Severity |
|-------|----------------|----------|
| Service start/stop | service_name, action, user_id, timestamp | Info |
| Configuration change | component, change_description, user_id, timestamp | Warning |
| Certificate expiration warning | cert_subject, expiry_date, days_remaining | Warning |
| Firewall rule change | rule_id, action, changed_by, timestamp | Warning |
| Deployment event | version, environment, deployer, timestamp | Info |

## What NOT to Log (Sensitive Data Exclusions)

### Mandatory Exclusions

| Data Type | Risk | Alternative |
|-----------|------|-------------|
| Passwords (plaintext or hashed) | Credential exposure | Log "password changed" event, not the password |
| Session tokens | Session hijacking | Log session_id (opaque reference) |
| API keys/secrets | Credential exposure | Log key_id (partial, e.g., last 4 chars) |
| Credit card numbers | PCI-DSS violation | Log last 4 digits only |
| Social Security Numbers | PII exposure | Log "SSN verified" boolean, not the SSN |
| Authentication tokens (JWT, OAuth) | Token replay | Log token_id or jti claim |
| Encryption keys | Key compromise | Log key_id, never key material |
| Health records (PHI) | HIPAA violation | Log access event, not the data |
| Biometric data | Irrevocable compromise | Log "biometric verified" boolean |

### Scrubbing Pattern

```python
# Middleware to scrub sensitive fields before logging
SENSITIVE_FIELDS = {'password', 'token', 'secret', 'authorization',
                    'cookie', 'ssn', 'credit_card', 'api_key'}

def scrub_for_logging(data, depth=0):
    if depth > 10:
        return "[TRUNCATED]"
    if isinstance(data, dict):
        return {
            k: "[REDACTED]" if k.lower() in SENSITIVE_FIELDS
            else scrub_for_logging(v, depth+1)
            for k, v in data.items()
        }
    if isinstance(data, str) and len(data) > 1000:
        return data[:100] + "...[TRUNCATED]"
    return data
```

## Structured Logging Format

### Recommended Fields

```json
{
  "timestamp": "2026-03-06T14:32:01.123Z",
  "level": "WARNING",
  "service": "auth-api",
  "version": "2.4.1",
  "environment": "production",
  "correlation_id": "req-abc123-def456",
  "trace_id": "4bf92f3577b34da6a3ce929d0e0e4736",
  "span_id": "00f067aa0ba902b7",
  "event_type": "authentication.failed",
  "user_id": "usr_789",
  "source_ip": "203.0.113.50",
  "user_agent": "Mozilla/5.0...",
  "resource": "/api/v2/login",
  "action": "POST",
  "outcome": "failure",
  "reason": "invalid_password",
  "metadata": {
    "attempt_count": 3,
    "account_locked": false
  }
}
```

### Key Principles

1. **Structured, not free-text**: Always JSON or key=value; never prose
2. **Consistent schema**: Same event type always has same fields
3. **UTC timestamps**: ISO 8601 format, always UTC
4. **Correlation IDs**: Thread a unique ID through all related events
5. **Semantic event types**: Hierarchical naming (auth.login.success, auth.login.failure)
6. **Machine-parseable**: Optimized for SIEM ingestion, not human reading

## Correlation IDs

### Implementation Pattern

```python
import uuid

class CorrelationMiddleware:
    def process_request(self, request):
        # Accept incoming correlation ID or generate new one
        correlation_id = request.headers.get('X-Correlation-ID')
        if not correlation_id:
            correlation_id = str(uuid.uuid4())
        request.correlation_id = correlation_id

    def process_response(self, request, response):
        # Propagate to response and downstream services
        response.headers['X-Correlation-ID'] = request.correlation_id
        return response
```

### Cross-Service Tracing

```
Request Flow:
  Client -> API Gateway -> Auth Service -> Database

All services log with same correlation_id:
  correlation_id=req-abc123 in API Gateway log
  correlation_id=req-abc123 in Auth Service log
  correlation_id=req-abc123 in Database audit log

SIEM query: correlation_id="req-abc123" shows complete request lifecycle
```

## Tamper Evidence

### Log Integrity Controls

| Control | Implementation |
|---------|---------------|
| Immutable storage | Write-once storage (S3 Object Lock, Azure Immutable Blob) |
| Hash chaining | Each log entry includes hash of previous entry |
| Digital signatures | Sign log batches with service key |
| Centralized forwarding | Forward to SIEM in real time (attacker cannot modify central store) |
| Access control | Write-only for applications; read-only for analysts |
| Retention locks | Compliance-mandated retention cannot be shortened |
| Gap detection | Alert on missing sequence numbers or time gaps |

### Hash Chain Implementation

```python
import hashlib

class TamperEvidentLogger:
    def __init__(self):
        self.previous_hash = "GENESIS"

    def log(self, event):
        event['previous_hash'] = self.previous_hash
        event_bytes = json.dumps(event, sort_keys=True).encode()
        event['hash'] = hashlib.sha256(event_bytes).hexdigest()
        self.previous_hash = event['hash']
        # Write to log store
        return event
```

## Log Pipeline Security

```
Application -> Log Shipper -> Message Queue -> SIEM
                (Fluentd)     (Kafka)         (Splunk/Elastic)

Security at each stage:
1. Application: Scrub sensitive data before logging
2. Log Shipper: TLS transport, authenticated connections
3. Message Queue: Encryption at rest, access control, retention
4. SIEM: Access control by role, immutable storage, alerting
5. Archive: Encrypted, integrity-verified, compliant retention
```

## Cross-References

- See `lib/patterns/secrets-management-patterns.md` for preventing secrets in logs
- See `reference/tools/splunk-reference.md` for SIEM query patterns
- See `data/registries/windows-event-ids-registry.md` for Windows log sources
- See `data/registries/linux-log-sources-registry.md` for Linux log sources
- See `frameworks/defense-layer.md` for detection strategy
