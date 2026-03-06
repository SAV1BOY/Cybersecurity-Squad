# Adversary Simulation Framework

## Purpose

Structured approach to objective-based adversary simulation (red teaming) that tests detection and response capabilities against realistic threat scenarios. Differs from penetration testing in scope, methodology, and objectives.

## Adversary Simulation vs. Penetration Testing

| Dimension | Penetration Testing | Adversary Simulation |
|-----------|-------------------|---------------------|
| Objective | Find vulnerabilities | Test detection and response |
| Scope | Defined target set | Full environment (objective-based) |
| Methodology | Systematic vulnerability assessment | Emulate specific threat actor TTPs |
| Stealth | Limited concern | Critical -- avoid detection as long as possible |
| Duration | 1-4 weeks | 4-12 weeks |
| Knowledge | Often white/gray box | Black box (limited knowledge) |
| Success metric | Vulnerabilities found | Objectives achieved, detections missed |
| Notification | IT/security teams aware | Limited awareness (need-to-know) |

## Engagement Lifecycle

### Phase 1: Objective Development

**Objective Categories:**

| Category | Example Objectives |
|----------|-------------------|
| Data exfiltration | Exfiltrate customer database, steal source code |
| Business disruption | Achieve capability to disrupt payment processing |
| Physical access | Gain unauthorized physical access to data center |
| Privilege escalation | Achieve domain admin from external starting point |
| Detection validation | Execute specific ATT&CK techniques, measure detection |
| Supply chain | Compromise CI/CD pipeline, inject code into production |

**Objective SMART Criteria:**
- **Specific:** "Exfiltrate 1,000+ customer records from production database"
- **Measurable:** Clear success/failure criteria
- **Achievable:** Realistic given constraints and timeframe
- **Relevant:** Tied to actual threat scenarios for the organization
- **Time-bound:** Defined engagement window

### Phase 2: Scenario Development

**Threat-Informed Scenarios:**

1. Select relevant threat actor profile (from threat intelligence)
2. Map actor's known TTPs to MITRE ATT&CK
3. Develop attack chain emulating actor's tradecraft
4. Identify required tools, infrastructure, and capabilities
5. Define success criteria for each phase

**Scenario Template:**

```
Scenario: [Name]
Emulated Actor: [APT group or archetype]
Motivation: [Espionage/Financial/Disruption]
Initial Access: [Technique]
Execution Chain:
  1. [Tactic] -> [Technique] -> [Procedure]
  2. [Tactic] -> [Technique] -> [Procedure]
  ...
Objective: [End goal]
Expected Defenses: [Known controls to test]
Success Criteria: [Measurable outcomes]
```

### Phase 3: Rules of Engagement (ROE)

**ROE Components:**

| Component | Details |
|-----------|---------|
| Scope | In-scope systems, networks, personnel |
| Exclusions | Systems that must not be tested (safety-critical, fragile) |
| Authorized techniques | Approved TTPs (with restrictions) |
| Prohibited actions | DoS against production, data destruction, social engineering limits |
| Time windows | Operating hours, blackout periods |
| Credential use | Rules for credential harvesting and use |
| Data handling | How to handle any sensitive data encountered |
| Communication | Trusted agent contacts, emergency stop procedures |
| Legal authority | Authorization letter, signed by appropriate executive |

**Technique Restrictions:**

| Technique | Restriction Level | Notes |
|-----------|-------------------|-------|
| Phishing | Approved with guardrails | Pre-approved pretexts, no targeting of personal accounts |
| Physical access | Case-by-case | Facility list, no tailgating of visitors |
| Social engineering | Limited | No impersonation of law enforcement, no coercion |
| Exploitation | Approved | No zero-day without explicit approval |
| Lateral movement | Approved | Avoid safety-critical systems |
| Persistence | Approved | Must document all implants for cleanup |
| Data exfiltration | Simulated | Exfiltrate synthetic data or proof tokens only |
| Denial of service | Prohibited | Unless explicitly authorized for specific test |

### Phase 4: Infrastructure Setup

**Red Team Infrastructure:**

```
Operator Workstation
    |
    ├── Redirectors (cloud-hosted, multi-region)
    │   ├── HTTPS redirector (domain-fronted or categorized domain)
    │   ├── DNS redirector (legitimate-looking domain)
    │   └── SMTP redirector (for phishing)
    |
    ├── C2 Servers (behind redirectors)
    │   ├── Primary C2 (Cobalt Strike, Mythic, Sliver)
    │   └── Backup C2 (different protocol/channel)
    |
    ├── Phishing Infrastructure
    │   ├── Mail server (authenticated, DKIM/SPF configured)
    │   └── Landing pages (cloned portals)
    |
    └── Payload Staging
        ├── Payload hosting (categorized domains)
        └── Exfiltration endpoint (cloud storage)
```

**OPSEC Requirements:**
- Separate infrastructure per engagement
- No reuse of domains, IPs, or certificates
- Traffic blends with normal organizational patterns
- Timestamps aligned with target timezone business hours
- Tool signatures modified to evade static detection

### Phase 5: Execution

**Execution Phases:**

| Phase | Activities | ATT&CK Tactics |
|-------|-----------|----------------|
| Reconnaissance | OSINT, infrastructure mapping, employee enumeration | Reconnaissance |
| Initial Access | Phishing, exploiting external services, supply chain | Initial Access |
| Establish Foothold | Deploy implant, establish C2, persistence | Execution, Persistence, C2 |
| Internal Recon | AD enumeration, network mapping, credential harvesting | Discovery, Credential Access |
| Lateral Movement | Move toward objective, escalate privileges | Lateral Movement, Privilege Escalation |
| Objective Completion | Access target data/system, demonstrate impact | Collection, Exfiltration, Impact |

**Logging Requirements:**
- Timestamped log of every command executed
- Screenshot evidence of each objective milestone
- Record of all credentials obtained
- Network connections and C2 sessions documented
- Artifacts dropped on target systems (for cleanup)

### Phase 6: Deconfliction

**Deconfliction Protocol:**

| Situation | Action |
|-----------|--------|
| SOC detects red team activity | Trusted agent confirms or denies (without revealing scope) |
| Red team discovers real threat | Immediate pause, notify trusted agent and SOC |
| System instability caused | Immediate cease, notify trusted agent, assist remediation |
| Scope boundary approached | Pause, confirm with engagement lead before proceeding |
| Law enforcement contact | Engagement lead provides authorization letter |

**Deconfliction Code System:**
- Code word to confirm red team activity (known only to trusted agents)
- Separate code word for real emergency stop
- Out-of-band communication channel (not monitored by SOC)

### Phase 7: Reporting

**Report Structure:**

1. **Executive Summary** -- Objectives, success/failure, key risks identified
2. **Scenario Overview** -- Emulated threat, attack narrative
3. **Attack Path** -- Step-by-step walkthrough with evidence
4. **Detection Assessment** -- What was detected, what was missed, time to detect
5. **Findings** -- Vulnerabilities and weaknesses exploited
6. **Detection Gap Analysis** -- Mapped to ATT&CK with coverage heat map
7. **Recommendations** -- Detection improvements, architecture changes, process improvements
8. **Cleanup Confirmation** -- All implants removed, credentials rotated

**Purple Team Debrief:**
- Walk through attack path with blue team
- Review detection logs at each step
- Identify tuning opportunities for existing detections
- Develop new detection rules for gaps
- Update threat models based on findings

## Cross-References

- [Red Team Maturity Model](red-team-maturity-model.md) -- program maturity
- [Detection Coverage Matrix](detection-coverage-matrix.md) -- ATT&CK coverage
- [Red Team Engagement Brief](../templates/briefs/red-team-engagement-brief.md) -- engagement template
- [Attack Technique Taxonomy](../lib/taxonomies/attack-technique-taxonomy.md) -- TTP classification
