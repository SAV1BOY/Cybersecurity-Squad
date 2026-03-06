# Adversary Mindset Training

## Purpose

Guide for developing adversarial thinking capabilities in security professionals. Covers red team psychology, assumption challenging techniques, creative attack ideation methods, and structured approaches to thinking like an attacker while defending.

## The Adversary Mindset

### Core Cognitive Shifts

| Defender Thinking | Adversary Thinking |
|-------------------|-------------------|
| "How do I protect this?" | "How do I break this?" |
| "What controls are in place?" | "What controls are missing or bypassable?" |
| "Is this compliant?" | "Does compliance equal security?" |
| "The firewall blocks this" | "What does the firewall NOT block?" |
| "Users are trained" | "Which user is the weakest link?" |
| "We patched that" | "What about the patch we missed?" |
| "Our policy prohibits this" | "Policy is not enforcement" |

### Adversary Advantage

Attackers have structural advantages that defenders must internalize:

1. **Asymmetry**: Attacker needs one path in; defender must cover all paths
2. **Initiative**: Attacker chooses when, where, and how to attack
3. **Persistence**: Attacker can try indefinitely; each failed attempt costs little
4. **Surprise**: Attacker knows the plan; defender discovers it reactively
5. **Creativity**: Attacker combines techniques in novel ways; defender follows playbooks

Understanding these advantages is the first step to countering them.

## Assumption Challenging Framework

### The Five Whys of Security Assumptions

For every security control or assumption, ask:

1. **Why do we believe this works?** (Evidence vs. faith)
2. **Why hasn't it been tested?** (Test frequency and realism)
3. **Why would an attacker care about this control?** (Would they just go around it?)
4. **Why is this our priority?** (Based on actual threat landscape or compliance checkbox?)
5. **Why would this fail?** (Single points of failure, edge cases, race conditions)

### Common Dangerous Assumptions

| Assumption | Reality Check |
|-----------|---------------|
| "Our network is segmented" | Verify with actual traffic analysis, not just firewall rules |
| "MFA protects us" | MFA fatigue, SIM swap, adversary-in-the-middle all bypass MFA |
| "We'd detect that" | Run the specific TTP in a lab and verify detection fires |
| "That's not in scope" | Attackers don't respect scope boundaries |
| "No one would do that" | If it's technically possible, someone will try it |
| "Our employees wouldn't fall for that" | Test it. They will. |
| "We use encryption" | Encryption of what, at which layer, with what key management? |
| "The vendor handles security" | Review their controls. Trust but verify. |

### Red Team Assumption Busting Exercise

```
Exercise: "Break Our Story"
Duration: 2 hours
Participants: Mixed red/blue team

1. Blue team presents their security architecture narrative
   "Here's how we defend against ransomware..."
2. Red team identifies every assumption in the narrative
3. For each assumption, red team proposes:
   - A technique that invalidates the assumption
   - Evidence needed to validate the assumption
4. Prioritize assumptions by risk if invalidated
5. Create testing plan for top 5 assumptions
```

## Creative Attack Ideation

### STRIDE Threat Modeling

| Category | Question | Attack Ideation |
|----------|----------|----------------|
| Spoofing | Who can I pretend to be? | Credential theft, certificate forgery, IP spoofing |
| Tampering | What can I modify? | Data in transit, logs, configuration, code |
| Repudiation | What actions can't be traced? | Log gap exploitation, shared accounts |
| Information Disclosure | What can I read? | Error messages, metadata, side channels |
| Denial of Service | What can I disrupt? | Resource exhaustion, dependency attacks |
| Elevation of Privilege | How do I gain more access? | Misconfigurations, vulnerabilities, trust abuse |

### Attack Tree Construction

```
Root Goal: Exfiltrate customer database

Branch 1: Direct database access
  1.1: SQL injection in web app
  1.2: Stolen database credentials
  1.3: Database backup file exposed

Branch 2: Application-layer access
  2.1: API enumeration (BOLA)
  2.2: Export function abuse
  2.3: GraphQL introspection + query

Branch 3: Infrastructure access
  3.1: Compromise app server -> pivot to DB
  3.2: Cloud metadata SSRF -> DB credentials
  3.3: Backup system access -> restore elsewhere

Branch 4: Supply chain
  4.1: Compromise data pipeline tool
  4.2: Third-party integration with DB access
  4.3: Insider with legitimate access
```

### Lateral Thinking Techniques

1. **Inversion**: Instead of "How do we prevent X?" ask "How do we guarantee X happens?"
2. **Analogy**: How did similar attacks succeed against similar organizations?
3. **Combination**: What happens when two low-severity issues are chained?
4. **Constraint removal**: If there were no security controls, what would the easiest path be?
5. **Time shift**: What if the attack started 6 months ago and we're just finding it now?
6. **Scale shift**: What if the attack targets 1 user? 1,000 users? All users?

## Training Exercises

### Purple Team Drills

| Drill Type | Duration | Objective |
|-----------|----------|-----------|
| Atomic Red Team | 30 min | Execute single TTP, verify detection |
| Kill Chain Walk | 2 hours | Walk through full attack chain on whiteboard |
| Capture the Flag | 4-8 hours | Competitive offensive challenge |
| Adversary Emulation | 1-5 days | Simulate specific threat actor TTPs |
| Assumed Breach | 1-3 days | Start from internal foothold, test detection |

### Daily Adversary Thinking Habits

1. **Morning threat brief**: Review overnight threat intel for 10 minutes
2. **"What would I attack?"**: Pick one system daily and sketch an attack path
3. **Detection validation**: Choose one detection rule and verify it fires correctly
4. **News analysis**: When breaches are reported, analyze TTPs before reading the full report
5. **Peer challenge**: Present a security assumption to a colleague and ask them to break it

### Recommended Reading for Adversary Mindset

- "The Art of War" by Sun Tzu (strategic thinking)
- "Red Team" by Micah Zenko (organizational red teaming)
- "The Hacker Playbook" series by Peter Kim (practical offensive)
- "Thinking, Fast and Slow" by Daniel Kahneman (cognitive biases)
- MITRE ATT&CK framework documentation (TTP library)

## Cross-References

- See `reference/psychology/social-engineering-psychology.md` for human attack vectors
- See `reference/psychology/decision-making-under-pressure.md` for cognitive biases
- See `frameworks/offense-layer.md` for offensive methodology
- See `frameworks/red-team-maturity-model.md` for red team capability development
- See `frameworks/detection-coverage-matrix.md` for coverage gap identification
