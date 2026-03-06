# Public Incident Reports and Postmortems

## Purpose

This collection catalogs notable public incident reports and postmortems that offer genuine lessons for security practitioners. Studying real incidents — how they happened, how they were detected (or not), and how organizations responded — is the most effective way to improve defensive capabilities. Each entry includes the key lessons the squad should internalize.

## Selection Criteria

Incidents included here meet at least one of these criteria:
- Novel attack technique or attack chain
- Exemplary (or cautionary) incident response
- Significant industry impact or regulatory consequence
- Well-documented public report with actionable technical detail
- Systemic lesson applicable beyond the specific victim organization

## Major Supply Chain Incidents

### SolarWinds / SUNBURST (2020)
- **What Happened**: Nation-state actor (attributed to Russia/SVR) compromised the SolarWinds Orion build system, inserting a backdoor into signed software updates distributed to approximately 18,000 organizations.
- **Report Sources**: Mandiant, Microsoft, CISA
- **Key Lessons**:
  - Build system integrity is a critical security boundary
  - Signed software from a trusted vendor is not inherently safe
  - Detection required identifying anomalous DNS patterns (DGA-like subdomains to avsvmcloud.com)
  - Dwell time was measured in months — the adversary was patient and disciplined
  - Incident response required coordinated multi-vendor effort
- **Squad Application**: Review build pipeline security, implement software composition analysis, establish detection for anomalous DNS patterns from trusted software

### Kaseya VSA / REvil (2021)
- **What Happened**: REvil ransomware group exploited zero-day vulnerabilities in Kaseya VSA remote management software to deploy ransomware to MSP customers downstream.
- **Key Lessons**:
  - MSP/RMM tools are high-value targets due to downstream access
  - Supply chain ransomware can scale to thousands of victims simultaneously
  - Zero-day exploitation in enterprise software is not limited to nation-states
- **Squad Application**: Assess supply chain risk from remote management tools, ensure RMM software is segmented and monitored

### Log4Shell / CVE-2021-44228 (2021)
- **What Happened**: Critical RCE vulnerability in Apache Log4j, a ubiquitous Java logging library. Trivially exploitable via crafted log messages. Affected virtually every Java application.
- **Key Lessons**:
  - Transitive dependency risk — most affected organizations did not know they used Log4j
  - Software Bill of Materials (SBOM) is not optional for vulnerability response
  - Exploitation began within hours of public disclosure
  - Patching took months due to the library's ubiquity in deeply embedded components
- **Squad Application**: Maintain SBOM for all applications, establish rapid response capability for library-level vulnerabilities

### 3CX Supply Chain Compromise (2023)
- **What Happened**: North Korean threat actors compromised 3CX desktop application through a cascading supply chain attack (first compromising Trading Technologies software, then using that access to compromise 3CX's build environment).
- **Key Lessons**:
  - Supply chain attacks can be multi-stage: one compromised vendor leads to another
  - Build environment monitoring is essential
  - EDR detection of anomalous behavior from signed, trusted applications is a critical detection layer
- **Squad Application**: Map supply chain dependencies, monitor for anomalous behavior from trusted applications regardless of code signing status

## Major Ransomware Incidents

### Colonial Pipeline (2021)
- **What Happened**: DarkSide ransomware group compromised Colonial Pipeline via a legacy VPN account without MFA, leading to shutdown of the largest fuel pipeline in the US.
- **Key Lessons**:
  - Legacy/orphan accounts with VPN access are a persistent entry vector
  - MFA on all remote access is non-negotiable
  - OT/IT segmentation (or lack thereof) determines blast radius
  - Business decision to pay ransom ($4.4M) was driven by operational impact assessment
- **Squad Application**: Audit all VPN accounts, enforce MFA universally, verify OT/IT segmentation

### Change Healthcare / UnitedHealth (2024)
- **What Happened**: ALPHV/BlackCat ransomware group compromised Change Healthcare, disrupting healthcare payment processing across the US for weeks.
- **Key Lessons**:
  - Single points of failure in critical infrastructure create systemic risk
  - Healthcare sector interdependencies amplify incident impact
  - Ransomware impact extends far beyond the directly compromised organization
- **Squad Application**: Identify single points of failure, develop contingency plans for critical vendor outages

## Major Data Breaches

### Equifax (2017)
- **What Happened**: Exploitation of CVE-2017-5638 (Apache Struts) on an internet-facing web application led to exfiltration of 147 million consumer records.
- **Report Source**: US House Committee report, GAO report, Equifax post-incident report
- **Key Lessons**:
  - Known vulnerability, patch available for months before exploitation
  - Expired SSL certificate on a network inspection device prevented detection of exfiltration
  - Asset inventory gaps meant the vulnerable application was not identified for patching
  - Organizational failures (expired certs, poor asset management) compounded the technical vulnerability
- **Squad Application**: Vulnerability management SLA enforcement, certificate lifecycle management, comprehensive asset inventory

### Capital One (2019)
- **What Happened**: Misconfigured WAF on AWS allowed SSRF attack to access EC2 metadata service and retrieve IAM credentials, leading to exfiltration of 100+ million customer records.
- **Key Lessons**:
  - Cloud misconfigurations are the new perimeter vulnerabilities
  - SSRF to cloud metadata is a well-known and preventable attack path (IMDSv2)
  - Insider threat vector — attacker was a former cloud service provider employee
- **Squad Application**: Enforce IMDSv2 on all EC2 instances, WAF configuration review, cloud security posture management

### MOVEit Transfer (2023)
- **What Happened**: Cl0p ransomware group exploited zero-day SQL injection in MOVEit Transfer file transfer software, compromising thousands of organizations.
- **Key Lessons**:
  - Managed file transfer applications are high-value targets (recurring pattern: GoAnywhere, Accellion, MOVEit)
  - Zero-day exploitation at scale by ransomware groups is now routine
  - Data exfiltration without encryption is an evolving ransomware tactic
- **Squad Application**: Inventory all file transfer solutions, minimize internet exposure, implement application-level monitoring

## Exemplary Postmortem Reports

### Cloudflare — Thanksgiving 2023 Incident
- **URL**: https://blog.cloudflare.com/thanksgiving-2023-security-incident
- **Why Exemplary**: Transparent, detailed timeline. Honest about what went wrong (credentials from Okta breach not rotated). Clear remediation actions.

### GitLab — Database Incident (2017)
- **URL**: https://about.gitlab.com/blog/2017/02/10/postmortem-of-database-outage-of-january-31/
- **Why Exemplary**: Radically transparent. Live-streamed the recovery. Documented every contributing factor without blame.

### Uber — 2016 Breach Disclosure
- **Why Cautionary**: Covered up the breach, paid the attackers, fired the CISO (who was later criminally charged). Demonstrates the consequences of concealment vs. transparency.

## How to Use This Resource

1. **Onboarding**: New team members should study at least 5 incidents from this list in their first month
2. **Tabletop Exercises**: Use these incidents as the basis for IR tabletop scenarios — "what would we do if this happened here?"
3. **Control Validation**: For each incident, ask "would our current controls detect/prevent this?" and document the answer
4. **Postmortem Standards**: Use the exemplary postmortems as templates for the squad's own incident reviews
5. **Threat Modeling**: Reference these incidents when building threat models for similar systems or architectures

## Cross-References

- See `voice/language-guides/incident-communication-language.md` for incident communication standards
- See `voice/tone-profiles/incident-commander.md` for IC communication during incidents
- See `swipe-sources/threat-intel-feeds.md` for sources that track emerging incidents
- See `swipe-sources/security-blogs-and-research.md` for detailed analysis of these and other incidents
