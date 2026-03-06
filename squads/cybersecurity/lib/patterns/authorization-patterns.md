# Authorization Patterns

## Purpose

Reference patterns for implementing secure authorization. Covers RBAC, ABAC, ReBAC models, policy engine integration, least privilege implementation, and common authorization vulnerabilities for security architects and application developers.

## Authorization Models

### Role-Based Access Control (RBAC)

**Concept**: Permissions assigned to roles; users assigned to roles.

```
User -> Role -> Permission -> Resource

Example:
  User: alice@corp.com
  Role: content-editor
  Permissions: [read:articles, write:articles, publish:articles]
  Denied: [delete:articles, manage:users]
```

**Best Practices**:
- Define roles based on job functions, not individuals
- Avoid role explosion (if roles > users, model is wrong)
- Regular role attestation (quarterly: does this user still need this role?)
- Separate duty roles (cannot be both approver and requester)
- Default deny: no role = no access

**Limitations**:
- Struggles with context-dependent access (time, location, data sensitivity)
- Role explosion in complex organizations
- Difficulty with cross-cutting concerns

### Attribute-Based Access Control (ABAC)

**Concept**: Access decisions based on attributes of subject, resource, action, and environment.

```
Policy: ALLOW if
  subject.department == resource.department AND
  subject.clearance >= resource.classification AND
  environment.time BETWEEN 08:00 AND 18:00 AND
  action IN [read, update]
```

**Attributes**:

| Category | Example Attributes |
|----------|-------------------|
| Subject | Role, department, clearance, location, device type |
| Resource | Owner, classification, type, sensitivity level |
| Action | Read, write, delete, approve, export |
| Environment | Time of day, IP address, risk score, auth method |

**Best Practices**:
- Centralized Policy Decision Point (PDP)
- Audit all attribute sources for integrity
- Cache decisions with appropriate TTL
- Default deny when attributes cannot be resolved

### Relationship-Based Access Control (ReBAC)

**Concept**: Access derived from relationships between entities in a graph.

```
# Google Zanzibar / SpiceDB / OpenFGA model
user:alice is editor of document:report-2024
team:engineering is parent of user:alice
document:report-2024 is in folder:team-docs
folder:team-docs has viewer relation to group:all-staff

# Access check: can user:bob view document:report-2024?
# Traverse graph: bob -> group:all-staff -> viewer -> folder:team-docs -> contains -> document:report-2024
# Result: ALLOW
```

**Best For**:
- Multi-tenant SaaS applications
- Document/resource sharing models
- Organizational hierarchy-based access
- Social graph permissions

## Policy Engine Integration

### Open Policy Agent (OPA)

```rego
# Rego policy example
package authz

default allow = false

# Allow users to read their own profile
allow {
    input.action == "read"
    input.resource.type == "profile"
    input.resource.owner == input.subject.id
}

# Allow managers to read reports of their team
allow {
    input.action == "read"
    input.resource.type == "report"
    input.resource.department == input.subject.department
    input.subject.role == "manager"
}

# Deny access outside business hours for non-admins
deny {
    not input.subject.role == "admin"
    time.hour(time.now_ns()) < 6
}
deny {
    not input.subject.role == "admin"
    time.hour(time.now_ns()) > 22
}
```

### Policy Decision Architecture

```
Application Code
      |
      v
Policy Enforcement Point (PEP)
      |
      v
Policy Decision Point (PDP)  <-- Policy Store
      |                       <-- Attribute Sources (IdP, CMDB, etc.)
      v
ALLOW / DENY + audit log
```

## Least Privilege Implementation

### Checklist

- [ ] All access denied by default (explicit allow required)
- [ ] Permissions scoped to minimum necessary resources
- [ ] Time-limited access for elevated privileges (JIT access)
- [ ] Regular access reviews with automated revocation
- [ ] Break-glass procedures for emergency access (audited)
- [ ] Service accounts have minimal, scoped permissions
- [ ] API keys scoped to specific endpoints and operations

### Just-In-Time (JIT) Access Pattern

```
1. User requests elevated access with justification
2. Request routed to approver (manager/security team)
3. Access granted for limited duration (1-8 hours)
4. All actions during elevated access are logged
5. Access automatically revoked at expiration
6. Audit trail available for review
```

## Common Authorization Vulnerabilities

### BOLA/IDOR (Broken Object Level Authorization)

```
Vulnerable:
  GET /api/users/123/profile  -> returns profile for user 123
  GET /api/users/456/profile  -> returns profile for user 456 (unauthorized!)

Secure:
  GET /api/users/me/profile   -> server resolves "me" from session
  # OR
  GET /api/users/123/profile  -> server verifies session.user_id == 123
```

### Broken Function Level Authorization

```
Vulnerable:
  Regular user discovers admin endpoint:
  POST /api/admin/create-user  -> succeeds without admin role check

Secure:
  Every endpoint checks authorization before processing
  Admin functions require admin role verification server-side
```

### Mass Assignment

```
Vulnerable:
  POST /api/users/update
  Body: { "name": "Alice", "role": "admin" }  -> role updated!

Secure:
  Allowlist updateable fields: only ["name", "email", "avatar"]
  Silently ignore or reject undeclared fields
```

### Privilege Escalation Patterns

| Pattern | Description | Prevention |
|---------|-------------|-----------|
| Horizontal | Access other users' resources at same privilege | Object-level authorization checks |
| Vertical | Gain higher privileges than assigned | Function-level authorization, role validation |
| Context | Change context to bypass restrictions | Validate context on server, not client |

## Testing Authorization

```
1. Map all endpoints and required permissions
2. For each endpoint, test as:
   - Unauthenticated user
   - Authenticated, unauthorized user
   - User from different tenant/organization
   - User with adjacent role (viewer trying editor actions)
   - User with expired/revoked access
3. Test parameter manipulation (change IDs, tenant markers)
4. Test HTTP method tampering (GET vs POST vs PUT vs DELETE)
5. Verify authorization is enforced server-side (not just UI)
```

## Cross-References

- See `lib/patterns/authentication-patterns.md` for authentication before authorization
- See `reference/tools/burp-suite-reference.md` for Autorize extension (IDOR testing)
- See `frameworks/identity-layer.md` for identity and access management
- See `frameworks/appsec-layer.md` for application security methodology
- See `checklists/api-security-assessment-quality.md` for API authorization testing
