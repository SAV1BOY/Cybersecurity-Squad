# Cloud Migration Security Workflow

## Purpose

Ensure security is embedded throughout cloud migration initiatives, from initial assessment through post-migration validation. Cloud migrations introduce new attack surfaces, shared responsibility gaps, and configuration risks that must be systematically addressed.

## Scope

Migrations to AWS, Azure, and GCP including lift-and-shift (IaaS), re-platforming (PaaS), and re-architecting (cloud-native). Covers infrastructure, application, data, and identity migration security concerns.

---

## Phase 1: Pre-Migration Security Assessment (Weeks 1-4)

### 1.1 Current State Security Baseline
- [ ] Document existing security controls and their cloud equivalents
- [ ] Inventory all data classifications and regulatory requirements
- [ ] Map current network security architecture and segmentation
- [ ] Catalog existing identity and access management systems
- [ ] Identify security tooling that needs cloud equivalents (SIEM, EDR, DLP)

### 1.2 Cloud Provider Security Assessment
- [ ] Review cloud provider shared responsibility model documentation
- [ ] Identify security controls that shift from organization to provider
- [ ] Evaluate provider compliance certifications (SOC 2, ISO 27001, FedRAMP)
- [ ] Assess provider's incident response and breach notification procedures
- [ ] Review data residency options and sovereign cloud availability

### 1.3 Regulatory and Compliance Mapping
- [ ] Map compliance requirements to cloud control equivalents
- [ ] Identify data residency restrictions (GDPR, data sovereignty laws)
- [ ] Determine audit logging and retention requirements in cloud
- [ ] Validate that cloud deployment meets industry-specific standards (HIPAA BAA, PCI)
- [ ] Engage compliance team for cloud-specific risk assessment

### 1.4 Risk Assessment
- [ ] Identify migration-specific risks (data exposure during transfer, downtime)
- [ ] Assess cloud-specific threats (misconfiguration, over-permissive IAM, public exposure)
- [ ] Evaluate vendor lock-in risks and exit strategy security implications
- [ ] Document risk acceptance criteria for migration go/no-go decision

## Phase 2: Cloud Security Architecture Design (Weeks 5-10)

### 2.1 Identity and Access Management
- [ ] Design cloud IAM hierarchy (organizations, accounts, projects, subscriptions)
- [ ] Implement account/project isolation per environment (dev, staging, prod)
- [ ] Configure federated identity with existing IdP (SAML/OIDC)
- [ ] Enforce MFA for all cloud console and CLI access
- [ ] Design break-glass account procedures
- [ ] Implement service account governance with minimal permissions
- [ ] Deploy just-in-time access for privileged operations

### 2.2 Network Security Architecture
- [ ] Design VPC/VNet topology with proper segmentation
- [ ] Configure private subnets for backend services (no public IPs)
- [ ] Implement centralized internet egress with inspection
- [ ] Deploy cloud-native WAF for internet-facing applications
- [ ] Configure VPN or private connectivity (Direct Connect, ExpressRoute)
- [ ] Implement DNS security and private DNS zones
- [ ] Design network security groups with deny-all-default posture

### 2.3 Data Protection
- [ ] Enable encryption at rest with customer-managed keys (CMK) for sensitive data
- [ ] Enforce TLS 1.2+ for all data in transit
- [ ] Configure cloud key management service with rotation policies
- [ ] Implement data loss prevention controls for cloud storage
- [ ] Design backup strategy with cross-region replication for DR
- [ ] Configure object storage access policies (no public buckets by default)

### 2.4 Logging and Monitoring
- [ ] Enable cloud audit logging (CloudTrail, Azure Activity Log, GCP Audit Logs)
- [ ] Configure log aggregation to centralized SIEM
- [ ] Deploy cloud-native security services (GuardDuty, Defender for Cloud, SCC)
- [ ] Implement resource configuration monitoring (AWS Config, Azure Policy)
- [ ] Set up alerting for security-critical events
- [ ] Ensure log storage is immutable and retained per policy

## Phase 3: Migration Execution Security (Weeks 11-16)

### 3.1 Pre-Migration Checklist
- [ ] Validate landing zone security controls are deployed and tested
- [ ] Confirm IAM roles and policies are configured correctly
- [ ] Verify network segmentation and firewall rules
- [ ] Test logging pipeline end-to-end
- [ ] Conduct security review of migration tools and their access requirements
- [ ] Encrypt data in transit during migration

### 3.2 During Migration
- [ ] Monitor for unauthorized access to migration pipelines
- [ ] Validate data integrity with checksums post-transfer
- [ ] Ensure temporary migration credentials are time-limited
- [ ] Monitor source systems for anomalous activity during migration window
- [ ] Maintain rollback capability throughout migration

### 3.3 Application-Specific Security
- [ ] Update application configurations for cloud-native secrets management
- [ ] Remove hardcoded credentials and migrate to secrets manager
- [ ] Update TLS certificates for cloud endpoints
- [ ] Reconfigure application logging for cloud log aggregation
- [ ] Validate authentication flows work with cloud identity

## Phase 4: Post-Migration Validation (Weeks 17-20)

### 4.1 Security Validation Testing
- [ ] Run cloud security posture management (CSPM) scan
- [ ] Conduct external attack surface assessment
- [ ] Perform penetration test of cloud environment
- [ ] Validate all data encryption configurations
- [ ] Test IAM permissions against principle of least privilege
- [ ] Verify network segmentation with port scanning

### 4.2 Compliance Validation
- [ ] Run compliance framework scans (CIS Benchmarks for cloud)
- [ ] Validate audit logging completeness and retention
- [ ] Confirm data residency requirements are met
- [ ] Generate compliance evidence for auditors
- [ ] Update risk register with cloud-specific residual risks

### 4.3 Decommission Source Systems
- [ ] Securely wipe data from decommissioned on-premises systems
- [ ] Revoke all migration-specific credentials and access
- [ ] Remove temporary network connectivity (VPN tunnels, firewall rules)
- [ ] Update asset inventory to reflect new cloud hosting
- [ ] Archive migration documentation

## Phase 5: Continuous Cloud Security Operations (Ongoing)

- [ ] Deploy CSPM for continuous misconfiguration detection
- [ ] Implement cloud workload protection platform (CWPP) for runtime security
- [ ] Schedule quarterly cloud security posture reviews
- [ ] Monitor cloud spending for anomalous usage (cryptomining indicator)
- [ ] Maintain cloud security training for engineering teams
- [ ] Track CIS Benchmark compliance score monthly

## Cross-References

- `workflows/security-architecture-review.md` — Architecture review for cloud designs
- `workflows/zero-trust-implementation.md` — Zero trust in cloud environments
- `scripts/cloud-security-audit.md` — Cloud audit automation scripts
- `frameworks/cloudsec-layer.md` — Cloud security framework
- `checklists/cloud-security-assessment-quality.md` — Cloud assessment checklist
- `archive/notable-breaches/capital-one-2019.md` — Cloud misconfiguration case study

## Quality Gates & Rework

### Per-Stage Gates
Cada stage deste workflow deve passar pelo quality gate aplicavel antes de avancar:
- Gate checklist: definido no `config.yaml` routing para a task correspondente
- Threshold de passagem: >= 80% (ver `docs/quality-gate-system.md`)
- Se score < 80%: retornar ao stage anterior com feedback especifico (ver `docs/rework-loop-protocol.md`)
- Se score < 60%: escalacao imediata para cyber-chief

### Rework Loop
- Max 3 iteracoes por stage antes de escalacao
- Feedback deve ser especifico (items falhados, expected vs actual)
- Todas as iteracoes logadas no `data/registries/decisions-log.md`

### Registry Updates
- Cada stage completo atualiza o registry correspondente (ver config.yaml routing)
- Workflow completion registrado no `data/registries/decisions-log.md`

### Cross-References
- Quality gate system: `docs/quality-gate-system.md`
- Rework protocol: `docs/rework-loop-protocol.md`
- Delegation protocol: `docs/delegation-protocol.md`
- Config routing: `config.yaml`
