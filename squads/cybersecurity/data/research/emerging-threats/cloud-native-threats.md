# Cloud-Native Attack Vectors

## Purpose

Research reference on attack vectors targeting cloud-native architectures. Covers serverless abuse, container escape techniques, service mesh exploitation, cloud control plane attacks, and defensive strategies for protecting modern cloud-native deployments.

## Serverless Attack Vectors

### Function Abuse Patterns

| Attack | Description | Impact |
|--------|-------------|--------|
| Event injection | Malicious data in event triggers (S3, API Gateway, SQS) | Code execution in function context |
| Dependency poisoning | Compromised libraries in function packages | Persistent supply chain compromise |
| Over-privileged functions | Excessive IAM permissions on Lambda/Cloud Functions | Lateral movement to other services |
| Resource exhaustion | Trigger infinite invocations or max memory allocation | Financial denial of service |
| Data leakage via /tmp | Shared /tmp directory between warm invocations | Cross-invocation data exposure |
| Environment variable exposure | Secrets in env vars readable by malicious code | Credential theft |
| Cold start exploitation | Inject during initialization phase | Runtime manipulation |

### Serverless Security Controls

```
1. Least privilege IAM per function (NOT shared roles)
2. Input validation on ALL event sources (not just API Gateway)
3. Ephemeral storage cleanup (clear /tmp after use)
4. Secrets via Secrets Manager (NOT environment variables)
5. Timeout limits to prevent runaway execution
6. Concurrency limits to prevent financial DoS
7. VPC attachment only when needed (limits attack surface)
8. Function-level monitoring and anomaly detection
```

## Container Escape Techniques

### Known Escape Vectors

| Vector | Description | Requirement |
|--------|-------------|-------------|
| Privileged container | Full host capabilities | `--privileged` flag |
| Host namespace sharing | Access host PID/network/IPC | `hostPID: true` etc. |
| Writable hostPath mount | Write to host filesystem | `hostPath` volume |
| Docker socket mount | Control Docker daemon | `/var/run/docker.sock` mounted |
| Kernel exploit | Exploit kernel vulnerability from container | Shared kernel + vuln |
| CAP_SYS_ADMIN | Broad capability enabling escape | `SYS_ADMIN` capability |
| cgroup escape | Escape via cgroup manipulation (CVE-2022-0492) | Specific kernel conditions |
| runc vulnerability | Container runtime bugs (CVE-2024-21626) | Outdated runtime |

### Container Hardening

```yaml
# Kubernetes pod security context (hardened)
securityContext:
  runAsNonRoot: true
  runAsUser: 65534
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop: ["ALL"]
  seccompProfile:
    type: RuntimeDefault
```

### Runtime Detection

| Indicator | Detection Method |
|-----------|-----------------|
| Container escape attempt | Falco rule: write to host filesystem from container |
| Cryptomining | CPU usage anomaly, connection to mining pools |
| Reverse shell | Unexpected outbound connections on unusual ports |
| Kubernetes API abuse | Audit log: pod creation, secret access from workload |
| Privilege escalation | Process running as root after starting as non-root |

## Service Mesh Exploitation

### Attack Surface

| Component | Attack | Mitigation |
|-----------|--------|-----------|
| Sidecar proxy | Proxy configuration manipulation | Strict sidecar injection policies |
| mTLS certificates | Certificate theft or impersonation | Short-lived certs, SPIFFE identities |
| Control plane | Istiod/Envoy config poisoning | RBAC on control plane APIs |
| Observability data | Trace/log injection for confusion | Signed telemetry, integrity checks |
| Policy bypass | Circumvent authorization policies | Default deny, regular policy audit |

### Service Mesh Security Benefits

When properly configured, service meshes provide:
- Automatic mTLS between all services
- Fine-grained authorization policies
- Traffic encryption without application changes
- Observability for anomaly detection
- Rate limiting and circuit breaking

## Cloud Control Plane Attacks

### Identity and Access Exploitation

| Attack | Description |
|--------|-------------|
| Metadata service SSRF | Access 169.254.169.254 to steal instance credentials |
| IAM privilege escalation | Exploit overly permissive policies to gain admin |
| Cross-account assume role | Abuse trust relationships between accounts |
| Service account impersonation | GCP: impersonate SA with iam.serviceAccounts.actAs |
| Federated identity abuse | Exploit OIDC/SAML federation misconfigurations |

### IMDSv2 Enforcement (AWS)

```bash
# Enforce IMDSv2 (token-required) to prevent SSRF-based credential theft
aws ec2 modify-instance-metadata-options \
  --instance-id i-1234567890abcdef0 \
  --http-tokens required \
  --http-endpoint enabled
```

### Cloud Attack Paths

```
Common attack chain:
1. SSRF in web application -> cloud metadata -> temporary credentials
2. Temporary credentials -> enumerate permissions (enumerate-iam)
3. Find overprivileged access -> access S3 buckets, databases
4. Create new access key or assume role -> persistent access
5. Lateral movement to other services and accounts
```

## Kubernetes-Specific Threats

| Threat | Description | Detection |
|--------|-------------|-----------|
| Malicious admission | Bypass admission controllers | Audit log: webhook failures |
| etcd exposure | Direct access to Kubernetes state store | Network policy, encryption at rest |
| Kubelet exploit | Access kubelet API on nodes | Authentication required, port restrictions |
| Helm chart poisoning | Malicious charts from untrusted repos | Chart signing, verified repos only |
| Secrets in etcd | Unencrypted secret storage | Enable encryption provider |
| Namespace escape | Cross-namespace access via RBAC misconfiguration | Regular RBAC audit |

## Defensive Architecture

### Cloud-Native Security Stack

```
Layer 1: Code Security
  - SAST/DAST in CI/CD
  - Dependency scanning
  - SBOM generation

Layer 2: Build Security
  - Image scanning (Trivy, Grype)
  - Image signing (Cosign)
  - Base image management

Layer 3: Deploy Security
  - Admission controllers (OPA/Kyverno)
  - Image policy enforcement
  - Configuration validation

Layer 4: Runtime Security
  - Runtime detection (Falco, Sysdig)
  - Network policy enforcement
  - Workload identity

Layer 5: Cloud Posture
  - CSPM (Prisma Cloud, Wiz, Orca)
  - IAM analysis
  - Configuration compliance
```

## Cross-References

- See `reference/tools/kubernetes-security-reference.md` for K8s hardening
- See `reference/tools/terraform-security-reference.md` for IaC security
- See `data/research/emerging-threats/supply-chain-evolution.md` for supply chain attacks
- See `frameworks/container-security-methodology.md` for container security methodology
- See `reference/industries/saas-cloud-security.md` for cloud security posture
