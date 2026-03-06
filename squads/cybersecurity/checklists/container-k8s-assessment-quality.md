# Container & Kubernetes Assessment Quality Gate

Checklist de qualidade para avaliacao de seguranca de containers e Kubernetes.

## Container Image Security
- [ ] Base images auditadas para vulnerabilities conhecidas
- [ ] Image scanning executado (Trivy, Grype, Snyk)
- [ ] Dockerfile best practices verificadas (non-root user, minimal base)
- [ ] Secrets nao hardcoded em images (env vars, config files)
- [ ] Image signing e provenance verificados (Cosign, Notary)
- [ ] Registry access controls auditados
- [ ] Unused packages e layers removidos das images

## Kubernetes Cluster Configuration
- [ ] CIS Kubernetes Benchmark executado (kube-bench)
- [ ] API server configuration auditada (auth, admission controllers)
- [ ] RBAC policies revisadas para least privilege
- [ ] Namespace isolation verificada
- [ ] Network Policies implementadas e testadas
- [ ] Pod Security Standards/Policies enforced
- [ ] etcd encryption at rest habilitada

## Runtime Security
- [ ] Privileged containers identificados e justificados
- [ ] Host namespace sharing (PID, network, IPC) auditado
- [ ] Volume mounts revisados (hostPath, sensitive paths)
- [ ] Resource limits definidos para todos os pods
- [ ] Security contexts verificados (runAsNonRoot, readOnlyRootFs)
- [ ] Capabilities dropped (ALL) e adicionadas minimamente
- [ ] Service mesh security configuration revisada (se aplicavel)

## Secrets e Configuration Management
- [ ] Kubernetes Secrets encryption verificada
- [ ] External secrets management integrado (Vault, KMS)
- [ ] ConfigMaps auditados para dados sensiveis
- [ ] Service account tokens auto-mounted apenas quando necessario
- [ ] OIDC/token rotation configurada

## Supply Chain e CI/CD
- [ ] Image pull policy configurada (Always, digest pinning)
- [ ] Admission controllers para image policy habilitados
- [ ] CI/CD pipeline security para deployments auditada
- [ ] Helm charts e manifests revisados para misconfigurations

## Monitoring e Incident Response
- [ ] Container runtime security monitoring ativo (Falco, Sysdig)
- [ ] Audit logging habilitado no cluster
- [ ] Alerting para eventos anomalos configurado
- [ ] Incident response plan para container compromise definido
- [ ] Findings documentados com remediation steps especificos
