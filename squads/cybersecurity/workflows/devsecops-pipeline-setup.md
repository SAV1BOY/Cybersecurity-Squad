# DevSecOps Pipeline Setup Workflow

## Purpose

Integrate security tooling and gates into CI/CD pipelines so that vulnerabilities are identified and remediated during development rather than in production. This workflow covers tool selection, pipeline configuration, policy definition, and developer enablement to shift security left without creating friction that developers bypass.

## Scope

All application CI/CD pipelines including web applications, APIs, microservices, infrastructure-as-code, container builds, and mobile applications.

---

## Phase 1: Pipeline Assessment and Tool Selection (Weeks 1-3)

### 1.1 Current State Assessment
- [ ] Inventory all CI/CD platforms in use (GitHub Actions, GitLab CI, Jenkins, Azure DevOps)
- [ ] Document current pipeline stages (build, test, deploy)
- [ ] Identify existing security tooling and coverage gaps
- [ ] Survey developer teams on pain points with current security processes
- [ ] Measure current mean time from code commit to vulnerability discovery

### 1.2 Tool Selection Matrix

| Category | Purpose | Tool Options | Pipeline Stage |
|----------|---------|-------------|----------------|
| SAST | Static code analysis | Semgrep, SonarQube, CodeQL, Checkmarx | Build |
| SCA | Dependency vulnerability scanning | Snyk, Dependabot, Grype, Trivy | Build |
| Secret Detection | Hardcoded secret identification | Gitleaks, TruffleHog, git-secrets | Pre-commit + Build |
| Container Scanning | Image vulnerability scanning | Trivy, Grype, Snyk Container | Build |
| IaC Scanning | Infrastructure misconfig detection | Checkov, tfsec, KICS, Bridgecrew | Build |
| DAST | Dynamic application testing | ZAP, Nuclei, Burp Suite Enterprise | Deploy (staging) |
| API Security | API-specific testing | 42Crunch, APIsec, Postman security | Deploy (staging) |
| License Compliance | OSS license risk | FOSSA, Black Duck, Snyk | Build |

### 1.3 Selection Criteria
Evaluate each tool against:
- [ ] Language and framework coverage for our stack
- [ ] False positive rate (developer trust depends on signal quality)
- [ ] CI/CD integration support (native plugins, CLI, API)
- [ ] Fix guidance quality (does it tell developers HOW to fix?)
- [ ] Performance impact on pipeline duration
- [ ] Licensing cost and scaling model
- [ ] Centralized policy management capability

Reference: `docs/tool-evaluation-criteria.md` for detailed scoring framework.

## Phase 2: Pipeline Configuration (Weeks 4-7)

### 2.1 Pre-Commit Hooks
Local developer environment gates (non-blocking, advisory):
```
Pre-commit hooks:
  - Secret detection (gitleaks)
  - Linting for security anti-patterns
  - Commit message validation
```
- [ ] Package pre-commit configuration and distribute to teams
- [ ] Provide installation documentation and IDE integration guides
- [ ] Make pre-commit hooks recommended, not mandatory (avoid bypass culture)

### 2.2 Build Stage Security Gates
Integrated into CI pipeline (blocking for critical/high):

**SAST Scan:**
- [ ] Configure SAST tool with organization-specific rule sets
- [ ] Tune rules to reduce false positives (start strict, loosen per feedback)
- [ ] Set severity thresholds: block on critical, warn on high, info on medium
- [ ] Configure incremental scanning (scan changed files only for speed)

**SCA / Dependency Scan:**
- [ ] Scan manifest files (package.json, requirements.txt, go.mod, pom.xml)
- [ ] Block on known exploited vulnerabilities (CISA KEV catalog match)
- [ ] Warn on critical CVEs without known exploits
- [ ] Configure license policy (block GPL in proprietary code, etc.)

**Secret Detection:**
- [ ] Scan all committed files for API keys, passwords, tokens, certificates
- [ ] Block pipeline on any secret detection (zero tolerance policy)
- [ ] Configure allowlist for false positives (test fixtures, documentation)
- [ ] Alert security team on detection for credential rotation

**Container Scanning:**
- [ ] Scan base images and final built images
- [ ] Enforce approved base image registry
- [ ] Block on critical OS-level vulnerabilities
- [ ] Validate image is built from Dockerfile (no arbitrary images)

**IaC Scanning:**
- [ ] Scan Terraform, CloudFormation, Kubernetes manifests
- [ ] Enforce security policies: no public S3 buckets, no overly permissive IAM
- [ ] Block on critical misconfigurations
- [ ] Generate compliance report for audit trail

### 2.3 Deploy Stage Security Gates

**Staging Environment DAST:**
- [ ] Run automated DAST scan against deployed staging environment
- [ ] Cover OWASP Top 10 vulnerability categories
- [ ] Scan authenticated and unauthenticated paths
- [ ] Block promotion to production on critical findings

**Smoke Security Tests:**
- [ ] Verify security headers are present (CSP, HSTS, X-Frame-Options)
- [ ] Validate TLS configuration meets minimum standards
- [ ] Check that debug endpoints are disabled
- [ ] Verify authentication is enforced on protected endpoints

## Phase 3: Policy-as-Code (Weeks 8-10)

### 3.1 Policy Definition
Define security policies as code that can be version-controlled and audited:
- [ ] Vulnerability severity thresholds per environment (dev/staging/prod)
- [ ] Approved and blocked software licenses
- [ ] Container base image allowlist
- [ ] Infrastructure security baselines
- [ ] Exception and waiver process (time-boxed, documented, approved)

### 3.2 Policy Enforcement Modes
Roll out policies progressively:
1. **Audit Mode** (Week 1-2): Log violations, do not block. Collect baseline data.
2. **Warn Mode** (Week 3-4): Display warnings in PR/pipeline. Educate developers.
3. **Enforce Mode** (Week 5+): Block pipeline on policy violations.

### 3.3 Exception Management
- [ ] Implement waiver request workflow (developer requests, security reviews)
- [ ] Time-box all exceptions (30, 60, or 90 days maximum)
- [ ] Require compensating controls documentation for waivers
- [ ] Auto-expire waivers and re-block unless renewed

## Phase 4: Developer Onboarding and Enablement (Weeks 11-14)

### 4.1 Training Program
- [ ] Produce pipeline security documentation with examples
- [ ] Create video walkthrough of pipeline stages and how to interpret results
- [ ] Develop "fixing common vulnerabilities" guides per language
- [ ] Host office hours for developer questions (weekly for first month)
- [ ] Integrate security champions from each team (see `frameworks/security-champion-program.md`)

### 4.2 Developer Experience Optimization
- [ ] Ensure pipeline adds < 5 minutes to build time
- [ ] Provide clear, actionable fix guidance in scan results
- [ ] Enable developers to run scans locally before committing
- [ ] Create PR comment integration showing scan results inline
- [ ] Build dashboard showing team-level vulnerability trends (gamification)

### 4.3 Feedback Loop
- [ ] Collect developer feedback on false positives weekly
- [ ] Tune rules based on feedback within 48 hours
- [ ] Track developer satisfaction with security tooling quarterly
- [ ] Measure mean time to remediate vulnerabilities (goal: < 5 days for critical)

## Key Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Pipeline security scan coverage | 100% of repos | CI/CD platform audit |
| Critical vulns caught pre-production | > 95% | SAST/SCA vs production findings |
| Pipeline duration increase from security | < 5 minutes | CI/CD metrics |
| Developer false positive escalations | < 5% of findings | Waiver/exception tracking |
| Mean time to remediate critical vulns | < 5 days | Vulnerability tracker |

## Cross-References

- `workflows/security-architecture-review.md` — Architecture review for new systems
- `frameworks/nist-ssdf.md` — Secure Software Development Framework
- `docs/onboarding-security-engineer.md` — Engineer onboarding including pipeline setup
- `docs/tool-evaluation-criteria.md` — Tool selection framework
- `frameworks/appsec-layer.md` — Application security framework
