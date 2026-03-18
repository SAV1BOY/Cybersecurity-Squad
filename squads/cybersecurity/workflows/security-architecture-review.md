# Security Architecture Review Workflow

## Purpose

Define a repeatable process for reviewing the security architecture of new systems, major changes, and existing infrastructure. This workflow ensures that security is designed in from the start rather than bolted on after deployment. Every system reaching production must pass through this review gate.

## Scope

Applies to all new system deployments, major architectural changes, cloud migrations, third-party integrations, and periodic reviews of existing critical systems.

---

## Phase 1: Intake and Scoping (Days 1-3)

### 1.1 Review Triggers
Architecture review is required when:
- New application or service is being developed
- Existing system undergoes major redesign (>30% change)
- Cloud migration or provider change
- New third-party integration with data exchange
- Merger/acquisition technology integration
- Regulatory change requiring architectural controls

### 1.2 Information Gathering
Request from the system owner / engineering lead:
- [ ] System purpose and business context
- [ ] Architecture diagram (logical and physical/deployment)
- [ ] Data flow diagram showing all data types and classifications
- [ ] Technology stack (languages, frameworks, databases, infrastructure)
- [ ] Authentication and authorization mechanisms
- [ ] Network connectivity requirements (internal, external, VPN)
- [ ] Compliance requirements (PCI, HIPAA, SOX, GDPR)
- [ ] Deployment model (on-prem, IaaS, PaaS, SaaS, hybrid)
- [ ] Expected user base and access patterns
- [ ] SLA and availability requirements

### 1.3 Assign Review Team
Based on system characteristics, assign reviewers with relevant expertise:
- Application security engineer (for custom code)
- Cloud security engineer (for cloud-native architectures)
- Network security engineer (for infrastructure changes)
- Identity/access management specialist (for auth flows)
- Compliance analyst (for regulated systems)

## Phase 2: Threat Modeling (Days 4-7)

### 2.1 STRIDE Analysis
For each component and data flow, evaluate:
- **S**poofing: Can identities be forged? Are authentication mechanisms adequate?
- **T**ampering: Can data be modified in transit or at rest? Is integrity verified?
- **R**epudiation: Are actions logged and attributable? Can users deny actions?
- **I**nformation Disclosure: Can data leak through side channels, errors, or logs?
- **D**enial of Service: Can the system be overwhelmed? Are rate limits in place?
- **E**levation of Privilege: Can users escalate beyond intended access levels?

### 2.2 Attack Surface Mapping
- [ ] Enumerate all entry points (APIs, UIs, message queues, file uploads)
- [ ] Identify trust boundaries between components
- [ ] Map data classification at each storage and transit point
- [ ] Document external dependencies and their trust level
- [ ] Identify privileged operations and their access controls

### 2.3 Threat Scenarios
Develop specific attack scenarios relevant to the system:
- [ ] External attacker exploiting internet-facing components
- [ ] Compromised insider with legitimate access
- [ ] Supply chain compromise of a dependency
- [ ] Data exfiltration through authorized channels
- [ ] Lateral movement from adjacent compromised system

Reference: `tasks/discovery/threat-modeling.md` for detailed methodology.

## Phase 3: Control Mapping (Days 8-12)

### 3.1 Security Control Requirements
Map required controls based on data classification and threat model:

| Domain | Controls | Validation Method |
|--------|----------|------------------|
| Authentication | MFA, session management, credential storage | Configuration review, pentest |
| Authorization | RBAC/ABAC, least privilege, separation of duties | Access matrix review |
| Encryption | TLS 1.2+, AES-256 at rest, key management | Configuration scan, certificate review |
| Logging | Audit logs, security events, retention | Log review, SIEM integration test |
| Input Validation | Server-side validation, parameterized queries | Code review, SAST |
| Network Security | Segmentation, WAF, DDoS protection | Network diagram review, scan |
| Secrets Management | No hardcoded secrets, vault integration | SAST, configuration review |
| Resilience | HA, DR, backup, circuit breakers | Architecture review, DR test |

### 3.2 Gap Analysis
- [ ] Compare required controls against proposed architecture
- [ ] Identify missing controls and their associated risk
- [ ] Classify gaps as: must-fix before production, accept with timeline, risk accept
- [ ] Document compensating controls for accepted gaps

### 3.3 Compliance Mapping
- [ ] Map architecture to applicable compliance controls
- [ ] Identify audit evidence generation points
- [ ] Ensure logging meets regulatory retention requirements
- [ ] Validate data residency constraints are satisfied

## Phase 4: Design Review Session (Day 13-14)

### 4.1 Review Meeting
Conduct a structured review meeting with:
- System architects and lead engineers
- Security review team
- Compliance representative (if applicable)
- Infrastructure/platform team representative

### 4.2 Review Agenda
1. Architecture walkthrough by system owner (30 min)
2. Threat model presentation and discussion (30 min)
3. Control gap review and remediation discussion (30 min)
4. Risk acceptance discussion for remaining gaps (15 min)
5. Action items and timeline agreement (15 min)

## Phase 5: Risk Acceptance and Sign-Off (Days 15-17)

### 5.1 Risk Documentation
For each identified risk:
- [ ] Risk description and potential impact
- [ ] Likelihood assessment (with threat model justification)
- [ ] Recommended control and estimated implementation effort
- [ ] Risk owner assignment
- [ ] Remediation timeline or risk acceptance justification

### 5.2 Review Verdicts

| Verdict | Criteria | Action |
|---------|----------|--------|
| Approved | No critical/high gaps; all medium gaps have remediation timeline | Proceed to production |
| Conditionally Approved | High gaps with compensating controls and 30-day remediation commitment | Proceed with monitoring |
| Requires Remediation | Critical gaps or unmitigated high risks | Block production until resolved |
| Rejected | Fundamental architecture flaws requiring redesign | Return to design phase |

### 5.3 Sign-Off
- Security architecture lead signs review findings
- System owner signs risk acceptance for any accepted risks
- CISO approval required for critical risk acceptance
- Document archived in `data/registries/risk-register.md`

## Phase 6: Post-Deployment Validation (Day 30+)

- [ ] Verify controls are implemented as designed (not just documented)
- [ ] Conduct targeted security testing of high-risk components
- [ ] Validate logging and monitoring integration with SIEM
- [ ] Schedule follow-up review for conditionally approved systems
- [ ] Update architecture review registry with completion status

## Cross-References

- `tasks/discovery/threat-modeling.md` — Detailed threat modeling methodology
- `tasks/discovery/data-flow-mapping.md` — Data flow analysis
- `workflows/cloud-migration-security.md` — Cloud-specific architecture concerns
- `workflows/devsecops-pipeline-setup.md` — CI/CD security integration
- `frameworks/nist-800-53-controls.md` — Control framework reference
- `data/registries/risk-register.md` — Risk documentation

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
