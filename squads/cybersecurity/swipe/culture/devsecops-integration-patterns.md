# DevSecOps Integration Patterns — Exemplary Implementations

## Purpose
Reference patterns for embedding security into CI/CD pipelines and developer workflows without creating friction.

## Core Philosophy
Security gates must be **fast, actionable, and developer-friendly**. Every security check that blocks a pipeline must provide a clear remediation path. No security tool should be a black box to developers.

## Integration Patterns

### Pattern 1: Shift-Left Pipeline Security
```
Developer Commit
    │
    ├─→ Pre-commit hooks
    │   ├── Secret scanning (trufflehog/gitleaks) — <5s
    │   ├── SAST quick scan (semgrep rules) — <10s
    │   └── Dependency lock file check — <2s
    │
    ├─→ CI Pipeline (PR stage)
    │   ├── Full SAST scan (CodeQL/Semgrep) — <5min
    │   ├── SCA dependency audit (npm audit/safety) — <2min
    │   ├── Container image scan (Trivy/Grype) — <3min
    │   ├── IaC security scan (Checkov/tfsec) — <2min
    │   └── License compliance check — <1min
    │
    ├─→ PR Review
    │   ├── Security findings as PR comments (inline)
    │   ├── Security team auto-tagged if critical findings
    │   └── Security approval required for sensitive paths
    │
    ├─→ Merge to Main
    │   ├── Full DAST scan against staging — <15min
    │   ├── API fuzzing (if API changes detected)
    │   └── Integration security tests
    │
    └─→ Deploy to Production
        ├── Runtime protection enabled (RASP/WAF rules)
        ├── Canary deployment with security monitoring
        └── Post-deploy security smoke tests
```

### Pattern 2: Security as Code
```yaml
# .security/policy.yaml — Version-controlled security policy
rules:
  critical_vulnerabilities:
    action: block_merge
    exceptions: security-team-approved

  high_vulnerabilities:
    action: warn
    auto_ticket: true
    sla_days: 14

  secrets_detected:
    action: block_merge
    exceptions: none

  outdated_dependencies:
    action: warn
    threshold: 90_days

  container_root:
    action: block_merge
    message: "Containers must not run as root"
```

### Pattern 3: Developer Security Tooling
- **IDE plugins**: Real-time SAST feedback as developers type
- **CLI tools**: `security-check` command developers can run locally
- **Dashboards**: Per-team security posture visible in developer portals
- **Chatbot**: Security Q&A bot in Slack for quick guidance
- **Documentation**: Security patterns library with copy-paste examples

### Pattern 4: Vulnerability Management Pipeline
```
Discovery → Triage → Assignment → Fix → Verify → Close
    │          │         │          │      │
    │          │         │          │      └─ Retest in CI
    │          │         │          └─ Developer PR
    │          │         └─ Auto-assign to code owner
    │          └─ CVSS + context + exploitability
    └─ SAST, SCA, DAST, Bug Bounty, Pentests
```

## Metrics for DevSecOps Success

| Metric | Poor | Good | Elite |
|--------|------|------|-------|
| Mean time to fix critical vuln | >30 days | <14 days | <3 days |
| % PRs with security scan | <50% | >90% | 100% |
| False positive rate | >50% | <20% | <5% |
| Developer security training | Annual | Quarterly | Continuous |
| Security tool adoption | Mandated | Accepted | Championed |

## Anti-Patterns
- **Security theater**: Tools run but findings ignored
- **Alert fatigue**: Too many low-priority findings blocking pipelines
- **Shadow pipelines**: Teams bypassing security checks
- **Blame culture**: Using security findings to punish developers
- **Big bang rollout**: Enabling all checks at once instead of gradual adoption

## Cross-References
- `frameworks/owasp-samm.md` — Software Assurance Maturity Model
- `agents/jim-manico.md` — AppSec and secure SDLC expertise
- `templates/policies/secure-development-policy.md` — Development policy
- `checklists/appsec/secure-code-review-checklist.md` — Code review checklist
