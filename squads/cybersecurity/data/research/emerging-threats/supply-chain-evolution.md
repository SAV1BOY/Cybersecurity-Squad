# Supply Chain Attack Evolution

## Purpose

Research reference on the evolution of software supply chain attacks. Covers dependency confusion, typosquatting, build pipeline compromise, and defensive strategies for securing the software supply chain from source to deployment.

## Attack Taxonomy

### Supply Chain Attack Categories

| Category | Description | Notable Example |
|----------|-------------|----------------|
| Dependency confusion | Exploit package manager priority resolution | Alex Birsan (2021) research |
| Typosquatting | Register packages with similar names | PyPI malicious packages |
| Compromised upstream | Legitimate package maintainer compromised | event-stream (2018) |
| Build system compromise | Inject malicious code during build | SolarWinds Orion (2020) |
| Source code repository attack | Compromise VCS or CI/CD pipeline | Codecov bash uploader (2021) |
| Distribution compromise | Tamper with delivery mechanism | NotPetya via M.E.Doc update (2017) |
| Hardware supply chain | Tampered chips, firmware, or devices | Theoretical/classified |
| Certificate compromise | Stolen or fraudulent code signing keys | ShadowPad, Stuxnet |

## Dependency Confusion

### Attack Mechanism

```
1. Attacker identifies private/internal package name (via:
   - Error messages, public documentation
   - JavaScript source maps
   - Public config files referencing internal packages)

2. Attacker publishes public package with same name and higher version

3. Package manager (npm, pip, NuGet) resolves public package
   due to version priority or misconfigured resolution order

4. Malicious code executes during install (pre/post-install scripts)
```

### Prevention

| Control | Implementation |
|---------|---------------|
| Namespace scoping | Use organization scope: `@company/package` (npm), org index (PyPI) |
| Registry configuration | Configure private registry as sole source; proxy public packages |
| Version pinning | Pin exact versions with integrity hashes |
| Lockfiles | Commit lockfiles, verify integrity hashes |
| Reserved names | Publish placeholder packages on public registries |
| Network monitoring | Alert on unexpected outbound package downloads during builds |

## Typosquatting

### Common Techniques

| Technique | Example |
|-----------|---------|
| Character omission | `reqests` instead of `requests` |
| Character swap | `requsets` instead of `requests` |
| Homoglyph | `reque5ts` (5 instead of s) |
| Hyphenation | `python-requests` vs `requests` |
| Pluralization | `colors` vs `colour` |
| Scope confusion | `@types/lodash` vs `@tyeps/lodash` |

### Detection

```bash
# Monitor for packages similar to your dependencies
# Tools: socket.dev, Snyk, npm audit signatures
# Custom: Levenshtein distance check against known dependencies

# Verify package authenticity
npm audit signatures          # npm provenance verification
pip-audit                     # pip vulnerability + provenance
```

## Build Pipeline Compromise

### SolarWinds-Style Attack Chain

```
1. Attacker gains access to build environment
2. Modifies build process to inject malicious code
3. Code passes code review (injected at build, not source)
4. Legitimate signing process signs compromised binary
5. Distributed via normal update channel
6. Customers install "legitimate" signed update
7. Malicious code activates post-deployment
```

### Build Pipeline Security Controls

| Layer | Control | Implementation |
|-------|---------|---------------|
| Source | Signed commits | GPG-signed commits required on protected branches |
| Source | Branch protection | Require reviews, prevent force push, CODEOWNERS |
| Source | Pre-commit hooks | Secret scanning, linting, license checks |
| Build | Hermetic builds | No network access during build, reproducible |
| Build | Build provenance | SLSA framework, in-toto attestations |
| Build | Ephemeral runners | Fresh build environment per job, no state |
| Artifact | Signing | Sigstore/Cosign for container images, code signing |
| Artifact | SBOM generation | CycloneDX or SPDX format per build |
| Deployment | Verification | Verify signatures and provenance before deployment |
| Deployment | Admission control | Only allow signed, scanned images in production |

### SLSA (Supply-chain Levels for Software Artifacts)

| Level | Requirements | Security Guarantee |
|-------|-------------|-------------------|
| SLSA 1 | Build process documented | Basic provenance |
| SLSA 2 | Hosted build service, version control | Tamper-resistant provenance |
| SLSA 3 | Hardened build platform, source verified | Protection against tampering |
| SLSA 4 | Hermetic, reproducible builds, 2-party review | High assurance |

## Software Bill of Materials (SBOM)

### SBOM Standards

| Standard | Format | Ecosystem |
|----------|--------|-----------|
| CycloneDX | JSON/XML | OWASP, broad adoption |
| SPDX | JSON/XML/RDF | Linux Foundation, ISO/IEC 5962 |

### SBOM Generation

```bash
# Generate CycloneDX SBOM
cdxgen -o sbom.json .

# Syft (from Anchore)
syft packages dir:. -o cyclonedx-json > sbom.json
syft packages registry:myimage:latest -o spdx-json > sbom.json

# Trivy
trivy fs --format cyclonedx --output sbom.json .
```

### SBOM Analysis

```bash
# Scan SBOM for vulnerabilities
grype sbom:sbom.json
trivy sbom sbom.json

# Track dependency freshness
# Compare SBOM against known vulnerable versions
```

## Dependency Management Best Practices

### Lockfile Strategy

```
1. ALWAYS commit lockfiles to version control
   - package-lock.json (npm)
   - yarn.lock (Yarn)
   - Pipfile.lock (Pipenv)
   - go.sum (Go)
   - Cargo.lock (Rust)

2. Verify integrity hashes in lockfiles during CI

3. Use --frozen-lockfile / --ci in CI builds
   npm ci          # NOT npm install
   yarn --frozen-lockfile
   pip install --require-hashes
```

### Vulnerability Monitoring

| Tool | Ecosystem | Features |
|------|-----------|----------|
| Dependabot (GitHub) | Multi-language | Automated PRs for updates |
| Snyk | Multi-language | Deep vulnerability analysis |
| Socket | npm, PyPI | Behavior analysis of packages |
| Renovate | Multi-language | Automated dependency updates |
| pip-audit | Python | Vulnerability auditing |
| npm audit | Node.js | Built-in vulnerability check |
| cargo-audit | Rust | Built-in vulnerability check |

## Organizational Strategy

1. **Maintain SBOM for all production software**
2. **Pin dependencies and use lockfiles everywhere**
3. **Scan dependencies in CI/CD before every merge**
4. **Monitor for new vulnerabilities in deployed dependencies continuously**
5. **Have a rapid patching process for critical dependency vulnerabilities**
6. **Evaluate new dependencies before adoption** (maintainer reputation, activity, security posture)
7. **Minimize dependency count** where feasible

## Cross-References

- See `data/research/emerging-threats/cloud-native-threats.md` for container supply chain
- See `frameworks/appsec-layer.md` for secure development lifecycle
- See `reference/tools/terraform-security-reference.md` for IaC supply chain
- See `frameworks/nist-ssdf.md` for secure software development framework
- See `reference/industries/government-security.md` for CMMC supply chain requirements
