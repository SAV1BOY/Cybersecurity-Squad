# Zero Trust Architecture Implementation Workflow

## Purpose

Define a repeatable, phased workflow for implementing zero trust architecture (ZTA) across enterprise environments. This workflow operationalizes the principle of "never trust, always verify" by systematically eliminating implicit trust from network architectures, identity systems, and data access patterns.

## Scope

Applies to all greenfield ZTA deployments and brownfield migrations from perimeter-based security models. Covers identity, device, network, application, and data pillars.

## Prerequisites

- Executive sponsorship and budget allocation confirmed
- Current network architecture documentation (see `tasks/discovery/data-flow-mapping.md`)
- Identity provider inventory complete (see `tasks/discovery/identity-and-privilege-mapping.md`)
- Asset registry populated (see `data/registries/asset-registry.md`)

---

## Phase 1: Assessment and Strategy (Weeks 1-4)

### 1.1 Define Protect Surfaces
- [ ] Identify critical data, assets, applications, and services (DAAS)
- [ ] Map each protect surface to business process owners
- [ ] Classify sensitivity: top secret, confidential, internal, public
- [ ] Document regulatory requirements per protect surface (GDPR, HIPAA, PCI DSS)

### 1.2 Map Transaction Flows
- [ ] Capture all legitimate traffic flows to/from each protect surface
- [ ] Document user-to-application, application-to-application, and service-to-service flows
- [ ] Identify data dependencies and integration points
- [ ] Record protocols, ports, and authentication mechanisms in use

### 1.3 Maturity Assessment
- [ ] Evaluate current state against CISA Zero Trust Maturity Model
- [ ] Score each pillar: Identity, Devices, Networks, Applications, Data
- [ ] Identify quick wins vs. multi-quarter initiatives
- [ ] Produce gap analysis report with prioritized recommendations

## Phase 2: Identity Verification Foundation (Weeks 5-10)

### 2.1 Identity Provider Consolidation
- [ ] Consolidate to a single authoritative identity provider where feasible
- [ ] Implement MFA for all user accounts (phishing-resistant preferred: FIDO2/WebAuthn)
- [ ] Deploy conditional access policies based on user risk, device health, and location
- [ ] Establish just-in-time (JIT) and just-enough-access (JEA) provisioning

### 2.2 Device Trust Establishment
- [ ] Deploy device certificate or compliance-based trust (MDM/EDR integration)
- [ ] Define device health baselines: OS version, patch level, encryption status
- [ ] Implement device posture checks at authentication time
- [ ] Create policy for unmanaged/BYOD device access tiers

### 2.3 Service Identity
- [ ] Implement mutual TLS (mTLS) for service-to-service communication
- [ ] Deploy workload identity frameworks (SPIFFE/SPIRE or cloud-native equivalents)
- [ ] Rotate service credentials automatically; eliminate static secrets
- [ ] Integrate secrets management (HashiCorp Vault, AWS Secrets Manager)

## Phase 3: Microsegmentation (Weeks 11-18)

### 3.1 Segmentation Design
- [ ] Design microsegmentation policy around protect surfaces, not network zones
- [ ] Define allow-list policies: deny all, permit by exception
- [ ] Map policies to Kipling Method: who, what, when, where, why, how
- [ ] Document east-west traffic policies for each segment

### 3.2 Implementation
- [ ] Deploy software-defined perimeter (SDP) or next-gen firewall microsegmentation
- [ ] Implement host-based firewalls as enforcement points on endpoints
- [ ] Configure identity-aware proxies for application access (BeyondCorp model)
- [ ] Enable encrypted tunnels between segments (WireGuard, IPsec)

### 3.3 Validation
- [ ] Test segmentation with controlled lateral movement attempts
- [ ] Verify that policy violations generate alerts
- [ ] Conduct red team validation of segment isolation (see `workflows/red-team-purple-team-cycle.md`)
- [ ] Document exceptions and compensating controls

## Phase 4: Continuous Monitoring and Analytics (Weeks 19-24)

### 4.1 Telemetry Collection
- [ ] Aggregate identity, network, endpoint, and application logs to SIEM
- [ ] Implement UEBA for anomalous access pattern detection
- [ ] Deploy network detection and response (NDR) for encrypted traffic analysis
- [ ] Enable cloud access security broker (CASB) for SaaS visibility

### 4.2 Policy Engine
- [ ] Deploy policy decision point (PDP) and policy enforcement points (PEP)
- [ ] Integrate real-time risk scoring into access decisions
- [ ] Implement step-up authentication for high-risk transactions
- [ ] Configure automated session termination on risk signal change

### 4.3 Continuous Verification
- [ ] Re-evaluate trust on every access request (not just at session start)
- [ ] Implement session timeouts and re-authentication triggers
- [ ] Monitor for credential theft indicators and force re-auth
- [ ] Validate device posture continuously, not just at login

## Phase 5: Optimization and Expansion (Ongoing)

- [ ] Review access logs monthly for policy refinement
- [ ] Expand ZTA to additional protect surfaces quarterly
- [ ] Conduct tabletop exercises simulating zero trust bypass scenarios
- [ ] Track metrics: policy violations, access denials, mean time to detect lateral movement
- [ ] Report ZTA maturity progression to executive leadership

## Key Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| MFA coverage | 100% of users | IdP dashboard |
| Microsegment policy violations | < 5/week after tuning | Firewall/SDP logs |
| Mean time to detect lateral movement | < 15 minutes | SIEM correlation |
| Implicit trust zones remaining | 0 | Architecture review |
| Phishing-resistant MFA adoption | > 90% | IdP reports |

## Cross-References

- `workflows/security-architecture-review.md` — Architecture review integration
- `frameworks/nist-csf.md` — NIST CSF alignment
- `tasks/discovery/identity-and-privilege-mapping.md` — Identity mapping prerequisite
- `frameworks/cis-controls-v8.md` — CIS Controls mapping

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
