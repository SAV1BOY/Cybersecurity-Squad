# Kubernetes Security Reference

## Purpose

Operational reference for securing Kubernetes clusters and workloads. Covers RBAC configuration, network policies, Pod Security Standards, admission controllers, image scanning, runtime security, and secrets management for container orchestration environments.

## RBAC (Role-Based Access Control)

### Core Concepts

| Object | Scope | Purpose |
|--------|-------|---------|
| Role | Namespace | Grants permissions within a namespace |
| ClusterRole | Cluster-wide | Grants permissions cluster-wide or across namespaces |
| RoleBinding | Namespace | Binds Role/ClusterRole to subjects in a namespace |
| ClusterRoleBinding | Cluster-wide | Binds ClusterRole to subjects cluster-wide |

### Least Privilege RBAC Example

```yaml
# Read-only role for developers in their namespace
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: app-team
  name: developer-readonly
rules:
- apiGroups: [""]
  resources: ["pods", "services", "configmaps"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["apps"]
  resources: ["deployments", "replicasets"]
  verbs: ["get", "list", "watch"]
---
# Bind to developer group
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: app-team
  name: developer-readonly-binding
subjects:
- kind: Group
  name: developers
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer-readonly
  apiGroup: rbac.authorization.k8s.io
```

### Dangerous RBAC Patterns to Detect

```bash
# Find cluster-admin bindings
kubectl get clusterrolebindings -o json | jq '.items[] | select(.roleRef.name=="cluster-admin") | .subjects'

# Find wildcard permissions
kubectl get roles,clusterroles -A -o json | jq '.items[] | select(.rules[]?.resources[]? == "*" or .rules[]?.verbs[]? == "*") | .metadata.name'

# Audit service account tokens
kubectl get serviceaccounts -A -o json | jq '.items[] | select(.automountServiceAccountToken != false) | .metadata | {namespace, name}'
```

### RBAC Hardening Checklist

- [ ] No default service account usage (create dedicated SAs)
- [ ] `automountServiceAccountToken: false` on pods that do not need API access
- [ ] No wildcard (`*`) permissions in production roles
- [ ] Minimize cluster-admin bindings (audit quarterly)
- [ ] Use Groups for RBAC bindings, not individual users

## Network Policies

### Default Deny All

```yaml
# Deny all ingress and egress by default
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
  namespace: production
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

### Allow Specific Traffic

```yaml
# Allow web pods to receive traffic on port 8080 from ingress controller
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-ingress
  namespace: production
spec:
  podSelector:
    matchLabels:
      app: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-system
    ports:
    - protocol: TCP
      port: 8080
---
# Allow web pods to talk to database on port 5432
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-to-db
  namespace: production
spec:
  podSelector:
    matchLabels:
      app: web
  policyTypes:
  - Egress
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: database
    ports:
    - protocol: TCP
      port: 5432
  - to:  # Allow DNS resolution
    - namespaceSelector: {}
    ports:
    - protocol: UDP
      port: 53
```

## Pod Security Standards (PSS)

### Enforcement Levels

| Level | Description | Use Case |
|-------|-------------|----------|
| Privileged | Unrestricted | System components only |
| Baseline | Prevent known escalations | General workloads |
| Restricted | Maximum hardening | Sensitive workloads |

### Namespace-Level Enforcement

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: production
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/audit: restricted
    pod-security.kubernetes.io/warn: restricted
```

### Hardened Pod Spec

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-app
spec:
  automountServiceAccountToken: false
  securityContext:
    runAsNonRoot: true
    runAsUser: 10001
    fsGroup: 10001
    seccompProfile:
      type: RuntimeDefault
  containers:
  - name: app
    image: registry.example.com/app:v1.2.3@sha256:abc123...
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop: ["ALL"]
      runAsNonRoot: true
    resources:
      limits:
        memory: "256Mi"
        cpu: "500m"
      requests:
        memory: "128Mi"
        cpu: "250m"
    volumeMounts:
    - name: tmp
      mountPath: /tmp
  volumes:
  - name: tmp
    emptyDir: {}
```

## Admission Controllers

### Essential Admission Controllers

| Controller | Purpose |
|------------|---------|
| PodSecurity | Enforce Pod Security Standards |
| NodeRestriction | Limit kubelet permissions |
| AlwaysPullImages | Force image pulls (prevent stale/tampered images) |
| ResourceQuota | Prevent resource exhaustion |
| LimitRanger | Default resource constraints |

### Policy Engines

| Engine | Description |
|--------|-------------|
| OPA Gatekeeper | General-purpose policy engine with Rego |
| Kyverno | Kubernetes-native policy management |
| Kubewarden | Wasm-based policy engine |

```yaml
# Kyverno policy: require non-root
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-run-as-non-root
spec:
  validationFailureAction: Enforce
  rules:
  - name: check-containers
    match:
      any:
      - resources:
          kinds: ["Pod"]
    validate:
      message: "Containers must run as non-root"
      pattern:
        spec:
          containers:
          - securityContext:
              runAsNonRoot: true
```

## Image Security

### Image Scanning Pipeline

1. **Build**: Scan during CI with Trivy, Grype, or Snyk
2. **Registry**: Scan on push with Harbor or ECR scanning
3. **Admission**: Block unscanned/vulnerable images at deploy
4. **Runtime**: Continuous monitoring with Falco or Sysdig

### Image Policy

```bash
# Scan with Trivy
trivy image --severity HIGH,CRITICAL registry.example.com/app:v1.2.3

# Enforce image signing (Cosign/Sigstore)
cosign verify --key cosign.pub registry.example.com/app:v1.2.3
```

### Image Hardening

- Use minimal base images (distroless, Alpine, scratch)
- Pin images by digest, not tag
- No secrets in image layers
- Multi-stage builds to exclude build tools
- Run as non-root user in Dockerfile

## Secrets Management

```yaml
# External Secrets Operator (preferred over native K8s secrets)
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: app-secrets
spec:
  refreshInterval: 1h
  secretStoreRef:
    name: vault-backend
    kind: ClusterSecretStore
  target:
    name: app-secrets
  data:
  - secretKey: db-password
    remoteRef:
      key: secret/data/production/database
      property: password
```

## Audit Logging

```yaml
# Audit policy (capture security-relevant events)
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: RequestResponse
  resources:
  - group: ""
    resources: ["secrets", "configmaps"]
- level: Metadata
  resources:
  - group: "rbac.authorization.k8s.io"
    resources: ["clusterroles", "clusterrolebindings", "roles", "rolebindings"]
- level: Metadata
  resources:
  - group: ""
    resources: ["pods/exec", "pods/portforward"]
```

## Cross-References

- See `reference/tools/terraform-security-reference.md` for IaC security
- See `frameworks/container-security-methodology.md` for container methodology
- See `checklists/container-k8s-assessment-quality.md` for assessment quality
- See `frameworks/cloudsec-layer.md` for broader cloud security context
- See `lib/patterns/secrets-management-patterns.md` for secrets patterns
