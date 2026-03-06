# Secrets Management Patterns

## Purpose

Reference patterns for secure secrets management. Covers vault integration, rotation automation, injection patterns, zero-knowledge architectures, and emergency access procedures for managing credentials, API keys, certificates, and encryption keys.

## Secrets Classification

| Category | Examples | Rotation Frequency | Storage |
|----------|---------|-------------------|---------|
| Infrastructure credentials | Database passwords, service accounts | 90 days or dynamic | Vault with dynamic generation |
| API keys | Third-party service keys | 90-180 days | Vault, environment injection |
| Encryption keys | AES/RSA keys, TLS certificates | Annual or on compromise | HSM or KMS |
| User credentials | Passwords, MFA seeds | On compromise only | Password hash in auth database |
| Signing keys | Code signing, JWT signing | Annual | HSM, air-gapped for critical |
| Session secrets | Cookie signing keys, CSRF tokens | On deployment | Vault, environment variables |

## Anti-Patterns (Never Do These)

| Anti-Pattern | Risk | Correct Approach |
|-------------|------|-----------------|
| Secrets in source code | Permanent exposure via git history | External secret injection |
| Secrets in environment variables (visible) | Process listing, crash dumps | Vault injection or mounted files |
| Shared credentials | No accountability, no rotation | Per-service, per-environment credentials |
| Long-lived static credentials | Extended compromise window | Dynamic/short-lived credentials |
| Secrets in container images | Image registry compromise = all secrets | Runtime injection via secrets manager |
| Secrets in CI/CD logs | Accidental logging | Masking + external secret references |
| Email/Slack shared secrets | Permanent record in third-party system | One-time share links with expiration |

## Vault Integration (HashiCorp Vault)

### Dynamic Secrets Pattern

```hcl
# Vault generates short-lived database credentials on demand
# Database secrets engine configuration
vault write database/config/mydb \
  plugin_name=mysql-database-plugin \
  connection_url="{{username}}:{{password}}@tcp(db.internal:3306)/" \
  allowed_roles="app-role" \
  username="vault-admin" \
  password="admin-password"

vault write database/roles/app-role \
  db_name=mydb \
  creation_statements="CREATE USER '{{name}}'@'%' IDENTIFIED BY '{{password}}'; \
    GRANT SELECT, INSERT, UPDATE ON myapp.* TO '{{name}}'@'%';" \
  default_ttl="1h" \
  max_ttl="24h"
```

```bash
# Application requests credential (lives for 1 hour)
vault read database/creds/app-role
# Returns: username=v-app-role-xyz, password=random, lease_id=xxx, ttl=1h
```

### AppRole Authentication

```bash
# Service authentication without human credentials
vault write auth/approle/role/myapp \
  token_policies="myapp-policy" \
  token_ttl=1h \
  token_max_ttl=4h \
  secret_id_ttl=24h \
  secret_id_num_uses=1  # One-time use secret ID

# Application authenticates
vault write auth/approle/login \
  role_id="$ROLE_ID" \
  secret_id="$SECRET_ID"
```

### Transit Secrets Engine (Encryption-as-a-Service)

```bash
# Encrypt data without exposing key to application
vault write transit/encrypt/my-key plaintext=$(base64 <<< "sensitive data")
# Returns: ciphertext=vault:v1:abc123...

# Decrypt
vault write transit/decrypt/my-key ciphertext="vault:v1:abc123..."
# Returns: plaintext (base64 encoded)

# Key rotation (transparent to application)
vault write -f transit/keys/my-key/rotate
# Previous versions still decrypt; new encryptions use latest version
```

## Cloud-Native Secrets Management

### AWS Secrets Manager

```python
import boto3
client = boto3.client('secretsmanager')

# Retrieve secret
response = client.get_secret_value(SecretId='prod/database/password')
secret = response['SecretString']

# Automatic rotation (Lambda-based)
client.rotate_secret(
    SecretId='prod/database/password',
    RotationLambdaARN='arn:aws:lambda:...',
    RotationRules={'AutomaticallyAfterDays': 30}
)
```

### Kubernetes External Secrets

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: app-db-creds
spec:
  refreshInterval: 15m
  secretStoreRef:
    name: vault-backend
    kind: ClusterSecretStore
  target:
    name: app-db-creds
    creationPolicy: Owner
  data:
  - secretKey: username
    remoteRef:
      key: secret/data/prod/database
      property: username
  - secretKey: password
    remoteRef:
      key: secret/data/prod/database
      property: password
```

## Rotation Automation

### Rotation Workflow

```
1. Generate new credential
2. Update secret store with new credential
3. Verify new credential works
4. Update all consumers (rolling deployment)
5. Verify application health with new credential
6. Revoke old credential
7. Audit log rotation event

CRITICAL: Steps 3-5 must succeed before step 6
Keep old credential valid during transition (dual-credential window)
```

### Emergency Rotation (Compromise Response)

```
1. Immediately generate new credential
2. Revoke compromised credential (accept brief outage if necessary)
3. Deploy new credential to all consumers (emergency push)
4. Verify application recovery
5. Investigate scope of compromise
6. Rotate all secrets that may have been co-located or accessible
7. Document in incident record
```

## Secret Detection and Prevention

### Pre-Commit Scanning

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.18.0
    hooks:
      - id: gitleaks

  - repo: https://github.com/trufflesecurity/trufflehog
    rev: main
    hooks:
      - id: trufflehog
```

### CI/CD Pipeline Scanning

```yaml
# Scan for secrets in CI pipeline
- name: Secret Scan
  run: |
    gitleaks detect --source . --verbose --report-path gitleaks-report.json
    if [ $? -ne 0 ]; then
      echo "SECRETS DETECTED - blocking merge"
      exit 1
    fi
```

### Git History Remediation

```bash
# If secret was committed, MUST assume compromised
# 1. Rotate the secret immediately
# 2. Then clean history (optional, does not undo exposure)
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch path/to/secret" \
  --prune-empty --tag-name-filter cat -- --all
```

## Zero-Knowledge Patterns

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Client-side encryption | Data encrypted before reaching server | End-to-end encrypted messaging |
| Split knowledge | No single party holds complete secret | M-of-N key ceremonies |
| Envelope encryption | Data key encrypts data; master key encrypts data key | Scalable encryption at rest |
| Hardware security module | Keys never leave tamper-resistant hardware | Root CA, signing keys |

## Cross-References

- See `lib/patterns/authentication-patterns.md` for credential usage patterns
- See `reference/tools/terraform-security-reference.md` for IaC secrets handling
- See `reference/tools/kubernetes-security-reference.md` for K8s secrets
- See `frameworks/cloudsec-layer.md` for cloud secrets management
- See `lib/patterns/logging-security-patterns.md` for secrets in logs prevention
