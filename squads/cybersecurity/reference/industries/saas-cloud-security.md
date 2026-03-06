# SaaS and Cloud-Native Security

## Purpose

Industry-specific security reference for SaaS providers and cloud-native organizations. Covers the shared responsibility model, multi-tenancy isolation, SOC 2 compliance, cloud-native security tooling, and CSA STAR certification for building and operating secure cloud services.

## Shared Responsibility Model

### Responsibility by Service Type

| Security Domain | IaaS (Customer) | PaaS (Shared) | SaaS (Provider) |
|----------------|-----------------|----------------|-----------------|
| Data classification | Customer | Customer | Customer |
| Identity & access | Customer | Shared | Shared |
| Application security | Customer | Customer | Provider |
| Network controls | Shared | Provider | Provider |
| OS patching | Customer | Provider | Provider |
| Physical security | Provider | Provider | Provider |
| Hypervisor | Provider | Provider | Provider |

### Common Misunderstandings

| Myth | Reality |
|------|---------|
| "The cloud provider secures our data" | Provider secures infrastructure; customer secures data and access |
| "Cloud = compliant" | Cloud provides tools for compliance; implementation is your job |
| "Default settings are secure" | Many defaults prioritize ease-of-use over security |
| "Backups are automatic" | Provider ensures infrastructure durability, not application-level backup |

## Multi-Tenancy Security

### Isolation Models

| Model | Isolation Level | Cost | Security |
|-------|----------------|------|----------|
| Separate infrastructure | Highest | Highest | Maximum isolation |
| Separate databases | High | High | Strong data boundary |
| Shared database, separate schemas | Medium | Medium | Logical isolation |
| Shared database, row-level security | Lowest | Lowest | Requires rigorous enforcement |

### Multi-Tenancy Security Controls

```
1. Tenant Context Enforcement
   - Every request must carry verified tenant identifier
   - Middleware validates tenant context before data access
   - Database queries MUST include tenant filter (no exceptions)
   - ORM-level enforcement preferred over application-level

2. Data Isolation Testing
   - Automated tests attempt cross-tenant data access
   - Regular penetration testing focused on tenant boundary
   - Fuzzing tenant identifiers in API requests
   - Verify logs are tenant-scoped

3. Key Management
   - Per-tenant encryption keys where possible
   - Key rotation on tenant offboarding
   - HSM-backed key storage
   - Tenant cannot access other tenants' key material

4. Resource Isolation
   - Rate limiting per tenant (prevent noisy neighbor)
   - Compute isolation for sensitive tenants
   - Network policy enforcement per tenant namespace
   - Storage quota enforcement
```

### BOLA/IDOR Prevention for Multi-Tenant APIs

```
# Every API endpoint must:
1. Extract tenant from authenticated session (NOT from request parameter)
2. Validate object belongs to tenant before returning data
3. Log cross-tenant access attempts as security events
4. Never expose internal IDs that could be enumerated
```

## SOC 2 Compliance

### Trust Service Criteria

| Criteria | Category | Description |
|----------|----------|-------------|
| CC1-CC5 | Common Criteria | Control environment, communication, risk assessment, monitoring, controls |
| A1 | Availability | System availability commitments and performance |
| C1 | Confidentiality | Information designated as confidential is protected |
| PI1 | Processing Integrity | System processing is complete, accurate, timely |
| P1 | Privacy | Personal information handling per privacy notice |

### SOC 2 Type I vs Type II

| Aspect | Type I | Type II |
|--------|--------|---------|
| Scope | Design of controls at a point in time | Operating effectiveness over a period (usually 12 months) |
| Effort | Lower | Higher |
| Assurance | Controls exist | Controls work consistently |
| Market preference | Acceptable for startups | Expected for mature SaaS |

### SOC 2 Evidence Collection

| Control Area | Evidence Examples |
|-------------|-----------------|
| Access control | Access review records, onboarding/offboarding tickets |
| Change management | PR reviews, deployment logs, approval records |
| Monitoring | Alert configurations, incident tickets, on-call schedules |
| Vulnerability management | Scan reports, patching records, SLA metrics |
| Encryption | Certificate inventory, key rotation logs, configuration screenshots |
| Incident response | IR plan, tabletop exercise records, incident postmortems |

## Cloud-Native Security Tools

### AWS Security Services

| Service | Function |
|---------|----------|
| GuardDuty | Threat detection (anomalous API calls, compromised instances) |
| Security Hub | Centralized security findings aggregation |
| IAM Access Analyzer | Identify unintended resource sharing |
| Config | Configuration compliance monitoring |
| CloudTrail | API activity logging |
| Macie | Sensitive data discovery in S3 |
| Inspector | Automated vulnerability assessment |
| KMS | Key management service |

### Azure Security Services

| Service | Function |
|---------|----------|
| Defender for Cloud | CSPM and workload protection |
| Sentinel | Cloud-native SIEM |
| Entra ID Protection | Identity risk detection |
| Key Vault | Secrets and key management |
| Policy | Policy-as-code enforcement |
| Network Watcher | Network monitoring and diagnostics |

### GCP Security Services

| Service | Function |
|---------|----------|
| Security Command Center | Asset inventory and threat detection |
| Chronicle | Security analytics and SIEM |
| BeyondCorp Enterprise | Zero trust access |
| Cloud KMS | Key management |
| VPC Service Controls | Data exfiltration prevention |

## CSA STAR (Security, Trust, Assurance, and Risk)

### STAR Levels

| Level | Assessment Type | Description |
|-------|----------------|-------------|
| Level 1 | Self-Assessment | CAIQ questionnaire (free, public) |
| Level 2 | Third-Party Audit | SOC 2 + CCM, or ISO 27001 + CCM |
| Level 3 | Continuous Monitoring | Automated, near-real-time assessment |

### Cloud Controls Matrix (CCM)

17 domains covering cloud-specific security controls including:
- Application & Interface Security
- Audit Assurance & Compliance
- Business Continuity & Operational Resilience
- Data Security & Privacy
- Governance, Risk & Compliance
- Identity & Access Management
- Infrastructure & Virtualization
- Interoperability & Portability
- Supply Chain Management, Transparency & Accountability
- Threat & Vulnerability Management

## Cross-References

- See `reference/industries/financial-services-security.md` for SaaS in regulated industries
- See `frameworks/cloudsec-layer.md` for cloud security methodology
- See `reference/tools/terraform-security-reference.md` for IaC security
- See `reference/tools/kubernetes-security-reference.md` for container orchestration security
- See `templates/reports/cloud-security-assessment-report.md` for assessment deliverables
