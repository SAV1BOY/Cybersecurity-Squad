# Attack Tree Construction Guide

## Purpose

Provide a systematic methodology for building attack trees that decompose complex attack objectives into structured hierarchies of sub-goals, identifying all feasible attack paths and their relative difficulty. Attack trees transform intuitive security thinking into rigorous, analyzable models that reveal non-obvious attack paths and prioritize defenses.

## When to Use
- Threat modeling for new systems and major changes
- Analyzing specific attack scenarios during architecture review
- Red team operation planning
- Evaluating control effectiveness against multi-step attacks
- Communicating complex threats to non-technical stakeholders

---

## Attack Tree Fundamentals

### Structure
An attack tree is a directed acyclic graph where:
- **Root Node**: The attacker's ultimate objective (what they want to achieve)
- **Leaf Nodes**: Atomic attack steps (individual actions an attacker performs)
- **Intermediate Nodes**: Sub-goals that combine to achieve higher-level goals
- **AND Gates**: All child nodes must succeed for the parent to succeed
- **OR Gates**: Any child node succeeding is sufficient for the parent

### Notation
```
[ROOT] Attacker Objective
  |
  +-- [OR] Sub-goal A (any path works)
  |     |
  |     +-- [AND] Both required
  |     |     +-- Step A.1
  |     |     +-- Step A.2
  |     |
  |     +-- Step A.3 (standalone alternative)
  |
  +-- [OR] Sub-goal B
        +-- Step B.1
        +-- Step B.2
```

## Construction Process

### Step 1: Define the Root Goal
State the attacker's objective clearly and specifically:
- Bad: "Compromise the system" (too vague)
- Good: "Exfiltrate customer PII database" (specific, measurable)
- Good: "Achieve persistent domain administrator access" (specific)
- Good: "Disrupt payment processing for > 4 hours" (specific, measurable)

### Step 2: Decompose into Sub-Goals
Break the root goal into major approaches an attacker could take:
```
[ROOT] Exfiltrate Customer PII Database
  |
  +-- [OR] Gain Direct Database Access
  +-- [OR] Compromise Application with DB Access
  +-- [OR] Obtain Database Backup Files
  +-- [OR] Compromise Third Party with Data Access
  +-- [OR] Social Engineer Employee with DB Access
```

### Step 3: Recursive Decomposition
Continue decomposing each sub-goal until you reach atomic actions:
```
[ROOT] Exfiltrate Customer PII Database
  |
  +-- [OR] Gain Direct Database Access
  |     |
  |     +-- [AND] Network Access + Database Credentials
  |     |     +-- [OR] Network Access
  |     |     |     +-- Exploit VPN vulnerability
  |     |     |     +-- Compromise employee workstation (phishing)
  |     |     |     +-- Exploit internet-facing application
  |     |     |
  |     |     +-- [OR] Database Credentials
  |     |           +-- Find credentials in source code repo
  |     |           +-- Extract from application config files
  |     |           +-- Dump from compromised application server memory
  |     |           +-- Brute force database authentication
  |     |
  |     +-- [AND] SQL Injection + Data Exfiltration Path
  |           +-- [OR] Find SQL Injection
  |           |     +-- Automated SQLi scanning
  |           |     +-- Manual parameter testing
  |           |     +-- Second-order SQLi via stored data
  |           |
  |           +-- [OR] Exfiltrate Data
  |                 +-- Direct data retrieval via UNION queries
  |                 +-- Out-of-band exfiltration (DNS, HTTP)
  |                 +-- Time-based blind extraction
  |
  +-- [OR] Compromise Application with DB Access
  |     +-- ... (continue decomposition)
  |
  +-- [OR] Obtain Database Backup Files
        +-- [OR] Access Backup Storage
        |     +-- Compromise backup server credentials
        |     +-- Access unprotected cloud storage (S3 bucket)
        |     +-- Intercept backup in transit
        |
        +-- [OR] Decrypt Backup (if encrypted)
              +-- Find encryption key in config
              +-- Brute force weak encryption
              +-- Backup stored without encryption (no decryption needed)
```

### Step 4: Annotate Leaf Nodes

For each leaf node (atomic attack step), annotate with:

| Attribute | Description | Values |
|-----------|------------|--------|
| Difficulty | Technical skill required | Low / Medium / High / Expert |
| Cost | Resources needed (time, money, tools) | $ / $$ / $$$ / $$$$ |
| Detection Risk | Likelihood of detection | Low / Medium / High |
| Prerequisites | What must be true for this step | List conditions |
| Controls | Existing mitigations | List controls |
| Probability | Estimated success probability | 0-100% |

### Step 5: Calculate Path Costs

**For OR gates:** The overall probability is the maximum of child probabilities (attacker chooses easiest path).

**For AND gates:** The overall probability is the product of child probabilities (all must succeed).

```
Example Calculation:
[AND] Network Access (80%) + Database Credentials (40%) = 32% overall
[AND] SQL Injection (60%) + Data Exfiltration (90%) = 54% overall

[OR] between the two paths = max(32%, 54%) = 54% most likely path
```

## Practical Example: Domain Administrator Compromise

```
[ROOT] Achieve Domain Admin Access
  |
  +-- [OR] Direct Credential Theft (High probability path)
  |     |
  |     +-- [AND] Initial Access + Credential Harvesting + Privilege Escalation
  |           |
  |           +-- [OR] Initial Access
  |           |     +-- Phishing with macro document [Med difficulty, Med detection]
  |           |     +-- Exploit public web application [High difficulty, Low detection]
  |           |     +-- Compromise VPN credentials [Med difficulty, Low detection]
  |           |
  |           +-- [OR] Credential Harvesting
  |           |     +-- Mimikatz on compromised host [Low difficulty, High detection]
  |           |     +-- LSASS dump via comsvcs.dll [Low difficulty, Med detection]
  |           |     +-- Kerberoasting service accounts [Med difficulty, Med detection]
  |           |     +-- NTLM relay attack [Med difficulty, Low detection]
  |           |
  |           +-- [OR] Privilege Escalation
  |                 +-- Pass-the-hash to admin account [Low difficulty, Med detection]
  |                 +-- Abuse Group Policy Preferences [Low difficulty, Low detection]
  |                 +-- Exploit weak ACLs on AD objects [Med difficulty, Low detection]
  |                 +-- DCSync with compromised account [Med difficulty, High detection]
  |
  +-- [OR] Active Directory Exploitation
  |     |
  |     +-- [AND] Identify Weakness + Exploit Path
  |           +-- [OR] AD Misconfiguration
  |           |     +-- Unconstrained delegation [Med, Low detection]
  |           |     +-- Weak ACLs on domain objects [Med, Low detection]
  |           |     +-- ADCS misconfiguration (ESC1-ESC8) [High, Low detection]
  |           |
  |           +-- Escalate to Domain Admin via identified path
  |
  +-- [OR] Compromise Existing Domain Admin
        +-- Password spray against admin accounts [Low, High detection]
        +-- Phish a known domain admin [Med, Med detection]
        +-- Compromise admin workstation physically [High, Med detection]
```

## Analysis and Prioritization

### Identifying Critical Paths
The critical path is the attack sequence with the highest probability of success and lowest cost to the attacker. Prioritize defenses along critical paths.

### Defense Mapping
For each leaf node, map existing and needed controls:
```
Attack Step: Mimikatz credential harvesting
  Existing Controls:
    - EDR with Mimikatz detection (High detection)
    - Credential Guard on workstations (Partial deployment - 60%)
  Gaps:
    - Credential Guard not on servers
    - No LAPS for local admin accounts
  Recommended:
    - Complete Credential Guard deployment
    - Deploy LAPS organization-wide
    - Implement Protected Users group for sensitive accounts
```

### Cost-Benefit Analysis
For each recommended control:
- How many attack paths does it block or impede?
- What is the implementation cost?
- What is the risk reduction achieved?
- Priority = (Number of paths blocked x Risk reduction) / Implementation cost

## Tools for Attack Tree Visualization
- Draw.io / diagrams.net (free, collaborative)
- Microsoft Visio or Lucidchart
- PlantUML (text-based, version-controllable)
- ATT&CK Navigator (for ATT&CK-mapped trees)
- SeaSponge (OWASP threat modeling tool)
- Dedicated tools: AttackTree+, Isograph

## Cross-References

- `lib/components/threat-model-canvas.md` — Canvas integration
- `tasks/discovery/threat-modeling.md` — Threat modeling methodology
- `workflows/security-architecture-review.md` — Architecture review process
- `workflows/red-team-purple-team-cycle.md` — Red team scenario planning
- `frameworks/credential-attack-methodology.md` — Credential attack paths
- `frameworks/privilege-escalation-methodology.md` — Escalation paths
