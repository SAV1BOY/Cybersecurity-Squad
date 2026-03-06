# Baseline Config Snapshots

Configuracoes baseline de seguranca para diferentes tipos de ativos e plataformas.

## Linux Server Baseline (CIS Level 1)

```
# Filesystem
- /tmp montado com noexec,nosuid,nodev
- Permissoes de /etc/passwd: 644, owner root
- Permissoes de /etc/shadow: 640, owner root
- SUID bits removidos de binarios nao essenciais

# Authentication
- PasswordAuthentication no (SSH)
- PermitRootLogin no (SSH)
- MaxAuthTries 3
- LoginGraceTime 60
- PAM password quality: minlen=14, minclass=4

# Network
- IP forwarding desabilitado
- ICMP redirects desabilitados
- TCP SYN cookies habilitados
- Firewall iptables/nftables ativo com default deny
```

## Kubernetes Baseline (CIS Benchmark)

```
# Pod Security
- runAsNonRoot: true
- readOnlyRootFilesystem: true
- allowPrivilegeEscalation: false
- capabilities: drop ALL

# Network Policies
- Default deny ingress e egress
- Namespace isolation habilitada

# RBAC
- ClusterAdmin restrito a break-glass accounts
- Service accounts com minimal permissions
- Token automount desabilitado por default
```

## AWS Account Baseline

```
# IAM
- MFA obrigatorio para todos os usuarios console
- Access keys rotacionadas a cada 90 dias
- Root account sem access keys, MFA hardware

# Logging
- CloudTrail habilitado em todas as regioes
- S3 access logging ativo
- VPC Flow Logs habilitados

# Networking
- Security groups com principio de least privilege
- Default VPC security group sem regras permissivas
- S3 Block Public Access habilitado account-level
```

## Processo de Revisao

Baselines revisados trimestralmente contra CIS Benchmarks atualizados.
Desvios identificados via scanning automatizado sao registrados como findings.
Excecoes requerem registro formal no exception registry.
