# Container Security Tools

## Visao Geral
Ferramentas para seguranca de containers e orquestracao (Docker, Kubernetes).
Area critica dado a adocao crescente de containers em producao.

## Container Image Scanning

### Trivy
- **Tipo**: comprehensive security scanner
- **Uso**: scan de images, filesystems, git repos, IaC
- **Cobertura**: CVEs, misconfigurations, secrets
- **Integracao**: CI/CD, registries, Kubernetes
- **Diferencial**: rapido, abrangente, open-source

### Grype
- **Tipo**: vulnerability scanner para container images
- **Uso**: identificar CVEs em images
- **Companion**: Syft para SBOM generation
- **Diferencial**: rapido e integravel em pipelines

### Snyk Container
- **Tipo**: commercial container security
- **Uso**: scan de images com recomendacoes de fix
- **Diferencial**: base image upgrade recommendations

## Kubernetes Security

### kube-bench
- **Tipo**: CIS Kubernetes Benchmark checker
- **Uso**: verificar conformidade com CIS benchmarks
- **Output**: pass/fail por cada recomendacao
- **Dica**: executar em cada cluster periodicamente

### kube-hunter
- **Tipo**: Kubernetes penetration testing tool
- **Uso**: descobrir vulnerabilidades em clusters K8s
- **Modos**: remote, internal, network scan

### Kubescape
- **Tipo**: Kubernetes security platform
- **Uso**: compliance, misconfiguration, vulnerability scanning
- **Frameworks**: NSA-CISA, MITRE ATT&CK for K8s, CIS

### Falco
- **Tipo**: runtime security monitor
- **Uso**: deteccao de comportamento anomalo em containers
- **Regras**: syscall monitoring, file access, network activity
- **Diferencial**: deteccao em runtime, nao apenas em build

## Docker Security

### Docker Bench for Security
- **Tipo**: CIS Docker Benchmark checker
- **Uso**: verificar hardening do Docker host e daemon
- **Script**: shell script baseado no CIS benchmark

### Hadolint
- **Tipo**: Dockerfile linter
- **Uso**: best practices para Dockerfiles
- **Regras**: seguranca, performance, maintainability

### Dockle
- **Tipo**: container image linter
- **Uso**: verificar best practices em images construidas
- **CIS**: alinhado com CIS Docker Benchmark

## Supply Chain Security

### Cosign (Sigstore)
- **Tipo**: container image signing
- **Uso**: assinar e verificar images de container
- **Diferencial**: keyless signing com OIDC

### in-toto
- **Tipo**: supply chain integrity framework
- **Uso**: verificar integridade do build pipeline

## Network Policies e Service Mesh

### Cilium
- **Tipo**: eBPF-based networking e security
- **Uso**: network policies, observability, security
- **Diferencial**: performance e visibilidade granular

### Istio
- **Tipo**: service mesh
- **Uso**: mTLS, access control, observability
- **Security**: zero-trust networking entre services

## Pipeline de Container Security
1. **Build**: Hadolint (Dockerfile) + Trivy (image scan)
2. **Registry**: Cosign (signing) + admission control
3. **Deploy**: kube-bench + Kubescape (cluster compliance)
4. **Runtime**: Falco (anomaly detection) + network policies
5. **Continuous**: periodic scanning e policy enforcement

## Notas do Squad
Container security e uma das areas de maior demanda no mercado brasileiro.
Manter expertise atualizada em Kubernetes security e fundamental.
