# Secure Cloud Architecture Framework

## Purpose

Define secure cloud architecture patterns for multi-cloud and hybrid environments. Covers landing zone design, guardrails, service control policies, network topology, and encryption strategy.

## Landing Zone Architecture

### Core Components

| Component | Purpose | Implementation |
|-----------|---------|---------------|
| Account/Project structure | Blast radius isolation | Multi-account (AWS), multi-subscription (Azure), multi-project (GCP) |
| Identity foundation | Centralized authentication | AWS SSO/IAM Identity Center, Azure AD, Google Workspace/Cloud Identity |
| Network foundation | Connectivity and isolation | Hub-spoke or transit gateway topology |
| Logging foundation | Centralized audit and security logs | Organization-level log aggregation |
| Security foundation | Guardrails and monitoring | Organization-wide security policies |
| Governance foundation | Tagging, cost, compliance | Tag policies, budget alerts, compliance frameworks |

### Account/Subscription Strategy

```
Organization Root
├── Security OU
│   ├── Log Archive Account (immutable log storage)
│   ├── Security Tooling Account (GuardDuty, SIEM, forensics)
│   └── Audit Account (read-only cross-account access)
├── Infrastructure OU
│   ├── Network Hub Account (transit gateway, DNS, shared VPC)
│   ├── Shared Services Account (CI/CD, artifact registry, secrets)
│   └── Identity Account (directory, SSO, certificate authority)
├── Workload OU
│   ├── Production OU
│   │   ├── App-A Production Account
│   │   └── App-B Production Account
│   ├── Staging OU
│   │   └── Shared Staging Account
│   └── Development OU
│       └── Shared Development Account
└── Sandbox OU
    └── Developer Sandbox Accounts (auto-nuke after 7 days)
```

## Guardrails

### Preventive Guardrails (Service Control Policies / Organization Policies)

| Guardrail | Purpose | Implementation |
|-----------|---------|---------------|
| Deny root account usage | Prevent root credential use | SCP denying all actions except billing |
| Restrict regions | Limit resource deployment to approved regions | SCP region deny list |
| Require encryption | Enforce encryption on storage services | SCP condition key enforcement |
| Deny public S3/storage | Prevent public bucket creation | S3 Block Public Access at org level |
| Require tagging | Enforce mandatory resource tags | Tag policies with enforcement |
| Deny privilege escalation | Prevent IAM policy self-modification | SCP boundary on IAM actions |
| Protect log integrity | Prevent log deletion/modification | SCP deny on CloudTrail/log actions |
| Restrict instance types | Control compute costs and security | SCP allow-list for instance families |

### Detective Guardrails

| Guardrail | Detection Method | Response |
|-----------|-----------------|----------|
| Unencrypted resources | Config Rules / Policy | Auto-remediate or alert |
| Public network exposure | Cloud security posture management | Alert + auto-remediate |
| Unused credentials | IAM access analysis | Automated disable after 90 days |
| Compliance drift | Continuous compliance scanning | Alert + remediation ticket |
| Anomalous API calls | Cloud threat detection service | SOC alert |
| Cost anomalies | Budget alerts + anomaly detection | Alert + investigation |

## Network Topology

### Hub-Spoke Design

```
                    Internet
                       |
                  [WAF / CDN]
                       |
               ┌───────────────┐
               │  Network Hub  │
               │  - Transit GW │
               │  - Firewall   │
               │  - DNS        │
               │  - Proxy      │
               └───┬───┬───┬───┘
                   |   |   |
          ┌────────┘   |   └────────┐
          |            |            |
    ┌─────┴─────┐ ┌───┴────┐ ┌────┴─────┐
    │ Prod VPC  │ │Stg VPC │ │ Dev VPC  │
    │ 10.1.0/16 │ │10.2/16 │ │10.3.0/16 │
    └───────────┘ └────────┘ └──────────┘
```

### Subnet Strategy

| Subnet Type | Internet Access | Use Case | Example CIDR |
|-------------|----------------|----------|-------------|
| Public | Direct (IGW) | Load balancers, NAT gateways, bastion | /24 per AZ |
| Private (app) | Outbound via NAT | Application servers, containers | /22 per AZ |
| Private (data) | None | Databases, caches, storage endpoints | /24 per AZ |
| Private (mgmt) | Outbound via NAT | Management, monitoring, CI/CD agents | /24 per AZ |

### Network Security Controls

| Layer | Control | Purpose |
|-------|---------|---------|
| Edge | WAF, DDoS protection (Shield/Armor) | L7 filtering, volumetric attack mitigation |
| Perimeter | Cloud firewall (Network Firewall, Azure FW) | Stateful inspection, IDS/IPS |
| VPC/VNet | Security groups, NACLs, NSGs | Instance/subnet-level filtering |
| Service | VPC endpoints, Private Link | Eliminate internet traversal for cloud APIs |
| DNS | Route 53 Resolver / Private DNS | DNS resolution control, logging |
| Egress | NAT gateway + proxy | Outbound traffic control and inspection |

## Encryption Strategy

### Encryption at Rest

| Data Type | Encryption Method | Key Management |
|-----------|------------------|----------------|
| Block storage (EBS, managed disks) | AES-256 | CMK in cloud KMS |
| Object storage (S3, Blob, GCS) | AES-256 SSE | CMK with rotation |
| Database (RDS, Cloud SQL) | TDE or storage encryption | CMK in cloud KMS |
| Secrets | Vault encryption | HSM-backed keys |
| Backups | Encrypted at source | Same CMK or dedicated backup key |

### Encryption in Transit

| Communication Path | Minimum Standard | Implementation |
|-------------------|-----------------|---------------|
| Client to service | TLS 1.2+ | ALB/CLB TLS termination, managed certificates |
| Service to service | TLS 1.2+ or mTLS | Service mesh, internal certificates |
| VPC to VPC | IPSec or cloud-native encryption | Transit gateway encryption, VPN |
| Cloud to on-premises | IPSec VPN or Direct Connect + MACsec | Managed VPN, dedicated connectivity |
| Management plane | TLS 1.2+ | Cloud API default, SDK enforcement |

### Key Management Architecture

```
Root Key (HSM-backed, cloud KMS)
├── Infrastructure Key
│   ├── Storage encryption keys
│   ├── Database encryption keys
│   └── Backup encryption keys
├── Application Key
│   ├── Service-specific encryption keys
│   └── API signing keys
└── Security Key
    ├── Log encryption key
    ├── Secret encryption key
    └── Certificate signing key
```

**Key Rotation Policy:**

| Key Type | Rotation Frequency | Method |
|----------|-------------------|--------|
| KMS master keys | Annual (automatic) | Cloud KMS auto-rotation |
| Data encryption keys | Per-object or daily | Envelope encryption |
| TLS certificates | 90 days | Automated via ACME/managed service |
| API keys | 90 days | Automated rotation + deployment |
| Service account keys | 90 days or eliminate | Workload identity preferred |

## Monitoring and Detection

| Capability | AWS | Azure | GCP |
|-----------|-----|-------|-----|
| Audit logging | CloudTrail | Activity Log | Cloud Audit Logs |
| Threat detection | GuardDuty | Defender for Cloud | Security Command Center |
| Config compliance | AWS Config | Azure Policy | Security Health Analytics |
| Network monitoring | VPC Flow Logs | NSG Flow Logs | VPC Flow Logs |
| Secret scanning | Macie | Purview | DLP API |
| Vulnerability scanning | Inspector | Defender Vulnerability | Web Security Scanner |

## Cross-References

- [Cloud Shared Responsibility](cloud-shared-responsibility.md) -- responsibility boundaries
- [Cloud Security Assessment Checklist](../checklists/cloud-security-assessment-quality.md) -- assessment quality
- [Cloud Compromise Runbook](../swipe/runbooks/cloud-compromise-runbook.md) -- incident response
- [Cloud Security Assessment Report](../swipe/reports/cloud-security-assessment-examples.md) -- reporting templates
