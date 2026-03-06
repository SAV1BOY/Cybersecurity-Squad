# New Security Engineer Onboarding Guide

## Purpose

Provide a structured onboarding program for security engineers joining the team. Security engineers build, integrate, and maintain the security infrastructure, detection systems, and automation that protect the organization. This guide covers the first 90 days with emphasis on codebase orientation, CI/CD security, detection engineering, and initial project assignments.

## Audience
Security engineers, detection engineers, DevSecOps engineers, and security automation engineers.

---

## Day 1: Orientation and Access

### 1.1 Administrative and Security Setup
- [ ] Workstation provisioned with approved security tools
- [ ] Hardware security key issued for MFA (YubiKey or equivalent)
- [ ] Signed acceptable use policy, NDA, and code of conduct
- [ ] Reviewed data handling and classification requirements
- [ ] Completed mandatory security awareness training

### 1.2 Development Environment Setup
- [ ] Git client configured with SSH keys (GPG signing required for commits)
- [ ] IDE/editor installed with security linting plugins
- [ ] Access to code repositories (GitHub/GitLab/Bitbucket)
- [ ] Docker and container runtime installed
- [ ] Cloud CLI tools configured (AWS CLI, Azure CLI, gcloud)
- [ ] VPN configured for infrastructure access
- [ ] Local development environment tested

### 1.3 System Access Requests

| System | Purpose | Access Level |
|--------|---------|-------------|
| Source Code Repositories | Security tooling code | Read (week 1); write (after review) |
| SIEM Administration | Detection rule deployment | Engineer (admin after 30 days) |
| EDR Administration | Policy and rule management | Engineer access |
| CI/CD Platform | Pipeline configuration | Developer access |
| Cloud Security Accounts | CSPM, security tooling | Engineer access |
| Infrastructure-as-Code Repos | Terraform/CloudFormation | Read (week 1); write (after review) |
| Secrets Management | Vault/Secrets Manager | Application role only |
| Container Registry | Image scanning and management | Push/pull access |
| Security Orchestration (SOAR) | Automation playbooks | Developer access |
| Monitoring/Alerting | Grafana/Datadog/PagerDuty | Engineer access |

## Week 1: Architecture and Codebase Orientation

### 2.1 Security Architecture Review
- [ ] Review organizational network architecture diagram
- [ ] Understand security tool deployment topology (SIEM, EDR, NDR, WAF, proxy)
- [ ] Review cloud security architecture (accounts, VPCs, IAM structure)
- [ ] Understand logging pipeline: sources -> collection -> SIEM -> alerting
- [ ] Review detection engineering infrastructure and workflow
- [ ] Understand incident response tooling and integration

### 2.2 Codebase Orientation
- [ ] Clone and review security team's primary repositories
- [ ] Understand repo structure and coding standards
- [ ] Review existing detection rules (Sigma, YARA, custom)
- [ ] Review SOAR playbooks and automation scripts
- [ ] Understand deployment processes and environments (dev/staging/prod)
- [ ] Review documentation and ADRs (Architecture Decision Records)

### 2.3 Key Documentation Review
- [ ] `workflows/devsecops-pipeline-setup.md` — Pipeline security integration
- [ ] `workflows/detection-engineering-workflow.md` — Detection rule lifecycle
- [ ] `frameworks/detection-coverage-matrix.md` — ATT&CK coverage tracking
- [ ] `scripts/detection-rule-templates.md` — Detection rule formats
- [ ] `workflows/security-architecture-review.md` — Architecture review process
- [ ] Team runbooks for common operational tasks

## Weeks 2-3: CI/CD and DevSecOps

### 3.1 Pipeline Security Understanding
- [ ] Review all CI/CD pipelines with security scanning stages
- [ ] Understand SAST tool configuration and rule sets
- [ ] Review SCA/dependency scanning setup and policies
- [ ] Understand container scanning pipeline and image policies
- [ ] Review IaC scanning configuration (Checkov, tfsec)
- [ ] Understand secret detection pipeline (Gitleaks, TruffleHog)
- [ ] Review policy-as-code implementation and exception process

### 3.2 First Pipeline Task
- [ ] Pick up a pipeline improvement ticket from the backlog
- [ ] Examples: tune a false positive, add scanning to a new repo, update rule set
- [ ] Submit PR following team code review process
- [ ] Deploy change to staging and validate
- [ ] Promote to production with team approval

### 3.3 Security Tool Administration
Become familiar with the operational aspects:
- [ ] SIEM: how to create and deploy detection rules
- [ ] EDR: how to modify detection policies
- [ ] WAF: how to create and test custom rules
- [ ] SOAR: how to build and modify automation playbooks
- [ ] CSPM: how to create custom compliance policies

## Weeks 3-4: Detection Engineering

### 4.1 Detection Rule Development
- [ ] Study existing detection rule library and naming conventions
- [ ] Understand detection rule lifecycle: draft -> test -> deploy -> tune -> retire
- [ ] Learn to write Sigma rules (see `scripts/detection-rule-templates.md`)
- [ ] Understand SIEM-specific query languages for rule implementation
- [ ] Learn to test detection rules using atomic red team or simulation data

### 4.2 First Detection Rule
- [ ] Select an ATT&CK technique with no current detection (from coverage matrix)
- [ ] Research the technique: how it manifests, what logs are generated
- [ ] Write detection rule following team standards
- [ ] Test against historical data for false positives
- [ ] Deploy to staging environment and validate with simulation
- [ ] Present rule to team for peer review
- [ ] Deploy to production and document in `data/registries/detection-rules-registry.md`

### 4.3 Log Source Familiarization
Understand the primary log sources and what they reveal:
- [ ] Windows Security Event Log (common Event IDs: 4624, 4625, 4688, 4672, 7045)
- [ ] Sysmon (process creation, network, file, registry events)
- [ ] PowerShell Script Block Logging
- [ ] Linux auditd / syslog
- [ ] Cloud audit logs (CloudTrail, Activity Log, Audit Log)
- [ ] DNS query logs
- [ ] Proxy/web filter logs
- [ ] Email gateway logs
- [ ] EDR telemetry structure

## Month 2: Project Work

### 5.1 Assigned Project
Take ownership of a scoped project from the team backlog. Examples:
- Implement new SOAR playbook for common alert type
- Build automated IOC ingestion pipeline
- Create cloud security monitoring dashboards
- Develop new CI/CD security scanning integration
- Build detection rule test automation framework
- Implement log source onboarding for new technology

### 5.2 Code Quality Standards
All code contributions must:
- [ ] Follow team coding standards and style guides
- [ ] Include tests (unit tests, integration tests as appropriate)
- [ ] Have documentation (inline comments, README, runbook)
- [ ] Pass CI/CD quality gates
- [ ] Be peer-reviewed by at least one team member
- [ ] Include rollback procedure for infrastructure changes

### 5.3 Operational Responsibility
Begin participating in:
- [ ] On-call rotation for security infrastructure (shadow first, then primary)
- [ ] Security architecture review meetings (observer initially)
- [ ] Detection engineering sprint planning
- [ ] Incident response as technical support role

## Month 3: Integration and Independence

### 6.1 Operational Independence
- [ ] Handle routine security infrastructure tasks independently
- [ ] Deploy detection rules through full lifecycle without supervision
- [ ] Respond to on-call pages for security infrastructure issues
- [ ] Participate in incident response as security engineer
- [ ] Contribute to architecture review discussions

### 6.2 90-Day Review
- [ ] Present completed onboarding project to team
- [ ] Self-assessment of technical skills and knowledge gaps
- [ ] Manager review of progress and goal setting
- [ ] Identify specialization track: detection engineering, DevSecOps, cloud security, automation
- [ ] Set 6-month development plan with certification goals

### 6.3 Certification Path
Recommended certifications based on specialization:
- **Detection Engineering**: GCIA, GCDA, or SpecterOps-certified
- **DevSecOps**: AWS Security Specialty, CKS (Certified Kubernetes Security)
- **Cloud Security**: CCSP, AWS/Azure/GCP security certifications
- **Automation**: GSOM (SANS Security Operations and Monitoring)

## Cross-References

- `docs/onboarding-security-analyst.md` — Analyst onboarding (complementary)
- `workflows/devsecops-pipeline-setup.md` — Pipeline setup workflow
- `workflows/detection-engineering-workflow.md` — Detection engineering process
- `scripts/detection-rule-templates.md` — Rule template reference
- `docs/tool-evaluation-criteria.md` — Tool selection framework
- `frameworks/security-champion-program.md` — Champion program participation
