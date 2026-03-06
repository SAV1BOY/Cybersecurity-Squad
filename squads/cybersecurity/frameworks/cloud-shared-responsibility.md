# Cloud Shared Responsibility Framework

## Purpose

Clarify security responsibilities between cloud service providers (CSPs) and customers across AWS, Azure, and GCP. Eliminate ambiguity that leads to security gaps, misconfiguration, and compliance failures.

## Responsibility Matrix by Service Model

### IaaS (EC2, Azure VMs, GCE)

| Domain | Customer | Provider |
|--------|----------|----------|
| Physical security | -- | Full |
| Hypervisor | -- | Full |
| Network infrastructure | -- | Full |
| Operating system | Full | -- |
| Network controls (SG, NACL) | Full | -- |
| Identity & access management | Full | -- |
| Application security | Full | -- |
| Data encryption | Full | -- |
| Patch management (OS) | Full | -- |
| Logging & monitoring | Shared | Shared |

### PaaS (Lambda, Azure Functions, Cloud Run, RDS, App Service)

| Domain | Customer | Provider |
|--------|----------|----------|
| Physical security | -- | Full |
| OS/runtime patching | -- | Full |
| Platform configuration | Shared | Shared |
| Application code security | Full | -- |
| Identity & access management | Full | -- |
| Data encryption (config) | Full | Provider offers capability |
| Network controls | Shared | Shared |
| Logging & monitoring | Shared | Shared |
| Input validation | Full | -- |

### SaaS (Microsoft 365, Google Workspace, Salesforce)

| Domain | Customer | Provider |
|--------|----------|----------|
| Infrastructure | -- | Full |
| Application security | -- | Full |
| Identity configuration | Full | -- |
| Access controls & permissions | Full | -- |
| Data classification | Full | -- |
| Data loss prevention (config) | Full | Provider offers capability |
| User behavior monitoring | Full | Provider offers capability |
| Compliance configuration | Full | -- |

## Provider-Specific Details

### AWS Shared Responsibility

**AWS is responsible for "security OF the cloud":**
- Global infrastructure (Regions, AZs, edge locations)
- Hardware, software, networking, facilities
- Managed services infrastructure (RDS engine, Lambda runtime)

**Customer is responsible for "security IN the cloud":**
- IAM policies, MFA, credential management
- Security group and NACL configuration
- OS patching and hardening (EC2)
- Application-layer security
- Data encryption at rest and in transit
- CloudTrail, GuardDuty, Config enablement

### Azure Shared Responsibility

**Microsoft manages:**
- Physical hosts, network, datacenter
- Hypervisor and host OS
- Managed service infrastructure

**Customer manages:**
- Azure AD configuration, Conditional Access
- NSG rules, Azure Firewall policies
- VM patching (or configure Update Management)
- Key Vault configuration and access policies
- Defender for Cloud enablement and response
- Data classification and protection

### GCP Shared Responsibility

**Google manages:**
- Hardware, firmware, infrastructure
- Network backbone and DDoS protection
- Managed service infrastructure

**Customer manages:**
- IAM policies, Workload Identity Federation
- VPC firewall rules, Private Google Access
- GKE node and workload security
- Cloud KMS key management
- Security Command Center configuration
- Audit logging enablement

## Common Misunderstandings

| Misconception | Reality |
|---------------|---------|
| "The cloud provider secures everything" | Provider secures infrastructure; customer secures configurations, identities, and data |
| "Default settings are secure" | Most CSP defaults are permissive; hardening is customer responsibility |
| "Managed services need no security" | Customer must configure access, encryption, logging, and network controls |
| "Cloud provider handles compliance" | Provider provides compliant infrastructure; customer must configure and evidence compliance |
| "Backups are automatic" | Customer must configure backup policies, retention, and test recovery |
| "Encryption is enabled by default" | Varies by service; customer must verify and manage keys |
| "Network isolation is built in" | Customer must design VPCs, subnets, peering, and enforce segmentation |
| "The provider monitors for threats" | Provider offers tools; customer must enable, configure, and respond |

## Shared Responsibility Gaps Checklist

1. [ ] IAM: Root/global admin accounts secured with hardware MFA
2. [ ] IAM: Service accounts use least privilege, keys rotated
3. [ ] Network: Default security groups reviewed and tightened
4. [ ] Network: Public access restricted to intended services only
5. [ ] Encryption: At-rest encryption enabled with customer-managed keys where required
6. [ ] Encryption: TLS 1.2+ enforced for all in-transit communication
7. [ ] Logging: Cloud audit logs enabled and forwarded to SIEM
8. [ ] Logging: Flow logs enabled for network visibility
9. [ ] Patching: OS and middleware patching automated where possible
10. [ ] Backup: Backup policies configured, tested, and stored in separate region/account
11. [ ] Compliance: CSP compliance reports (SOC 2, ISO 27001) reviewed annually
12. [ ] Monitoring: Cloud-native threat detection enabled (GuardDuty, Defender, SCC)

## Cross-References

- [Secure Cloud Architecture](secure-cloud-architecture.md) -- architectural patterns
- [Cloud Security Assessment Checklist](../checklists/cloud-security-assessment-quality.md) -- assessment quality gates
- [Cloud Security Assessment Report Examples](../swipe/reports/cloud-security-assessment-examples.md) -- report templates
- [Cloud Compromise Runbook](../swipe/runbooks/cloud-compromise-runbook.md) -- incident response
