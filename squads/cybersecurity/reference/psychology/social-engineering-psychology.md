# Psychology of Social Engineering

## Purpose

Reference for understanding the psychological principles that underpin social engineering attacks. Covers Cialdini's influence principles as applied to security, pretexting framework construction, trust exploitation mechanics, and defensive awareness training design.

## Cialdini's Six Principles of Influence in Social Engineering

### 1. Reciprocity

**Principle**: People feel obligated to return favors.

**Attack Application**:
- Attacker provides "help" (e.g., IT support call) before requesting credentials
- Free gifts or services precede information requests
- Sharing "insider information" creates sense of obligation

**Example Pretext**: "I just cleared that ticket for you ahead of the queue. Could you verify your account details so I can close it out properly?"

**Defense**: Train staff to recognize unsolicited help as a potential manipulation vector. Verify identity regardless of perceived debt.

### 2. Commitment and Consistency

**Principle**: Once people commit to something, they tend to follow through to remain consistent.

**Attack Application**:
- Start with small, harmless requests, then escalate (foot-in-the-door technique)
- Get verbal agreement before asking for action
- Reference previous interactions to build continuity

**Example Pretext**: "Last time we spoke, you agreed to help test the new login system. I just need you to click this link and enter your current password to complete setup."

**Defense**: Teach that prior agreement does not obligate compliance with new, unverified requests. Every request must stand on its own authorization.

### 3. Social Proof

**Principle**: People follow what others are doing, especially under uncertainty.

**Attack Application**:
- "Everyone in your department has already completed this" (phishing)
- Name-dropping colleagues who already complied
- Fake testimonials or endorsements in phishing pages

**Example Pretext**: "Hi, this is IT. We're migrating email accounts. Sarah, Tom, and David from your team have already updated their credentials. You're one of the last ones."

**Defense**: Establish independent verification channels. "Everyone else did it" is never valid authorization.

### 4. Authority

**Principle**: People comply with perceived authority figures.

**Attack Application**:
- Impersonating executives, IT administrators, law enforcement
- Using official-sounding titles, jargon, and reference numbers
- Creating urgency tied to authority consequences

**Example Pretext**: "This is the CISO's office. We've detected a compromise on your account. I need you to reset your password immediately using this secure link."

**Defense**: Establish that authority must be verified, not assumed. Create culture where challenging authority on security matters is expected.

### 5. Liking

**Principle**: People are more easily influenced by those they like.

**Attack Application**:
- Building rapport before attack (long-con social engineering)
- Mirroring communication style, interests, background
- Expressing shared frustration ("I know these security policies are annoying, but...")

**Defense**: Awareness that rapport does not equal trustworthiness. Maintain verification procedures regardless of relationship perception.

### 6. Scarcity

**Principle**: Perceived scarcity increases perceived value and urgency.

**Attack Application**:
- "Your account will be locked in 2 hours if you don't verify"
- "This offer/access expires today"
- Limited-time urgency to bypass critical thinking

**Defense**: Any message creating artificial urgency should trigger suspicion. Legitimate processes have reasonable timelines.

## Pretexting Framework

### Pretext Construction Methodology

1. **Research Phase**: OSINT on target organization, culture, processes, personnel
2. **Persona Development**: Create believable identity with backstory, motivation, authority level
3. **Scenario Design**: Construct situation that justifies the information request
4. **Prop Development**: Email addresses, phone numbers, badges, uniforms, websites
5. **Rehearsal**: Practice delivery, anticipate questions, prepare fallback stories
6. **Execution**: Deliver pretext with confidence, adapt to responses
7. **Escalation Path**: Plan for challenges or verification attempts

### Effective Pretext Characteristics

| Element | Requirement |
|---------|-------------|
| Plausibility | Must fit within target's normal experience |
| Verifiability | Includes details that check out if investigated superficially |
| Urgency | Time pressure reduces critical analysis |
| Authority | Leverages power dynamics |
| Emotional hook | Triggers emotional response (fear, curiosity, helpfulness) |
| Minimal ask | Requests seem reasonable relative to context |

## Trust Exploitation Mechanics

### Trust Building Timeline

| Phase | Duration | Technique |
|-------|----------|-----------|
| Introduction | Minutes | Authority signals, shared context |
| Validation | Minutes-Hours | Demonstrate knowledge, provide value |
| Rapport | Hours-Days | Personal connection, consistency |
| Exploitation | Seconds | Pivot from trust to request |
| Maintenance | Ongoing | Post-exploitation access preservation |

### Cognitive Biases Exploited

| Bias | Description | Attack Use |
|------|-------------|-----------|
| Anchoring | First information disproportionately influences | Set context before the ask |
| Confirmation bias | Seek info confirming beliefs | Align pretext with expectations |
| Optimism bias | "It won't happen to me" | Exploit complacency |
| Dunning-Kruger | Overconfidence in abilities | Target users confident they "can't be fooled" |
| Halo effect | Positive impression generalizes | Professional appearance = trustworthy |
| Authority bias | Automatic deference to perceived authority | Impersonate executives or regulators |

## Defensive Training Design

### Effective Security Awareness Elements

1. **Scenario-based training**: Real-world attack simulations, not just slides
2. **Emotional engagement**: Show impact of successful attacks on real people
3. **Positive reinforcement**: Reward reporting, never punish victimization
4. **Spaced repetition**: Regular micro-training, not annual marathon
5. **Role-specific content**: Tailor to job function and risk level
6. **Metrics that matter**: Track reporting rates, not just click rates

### Attack Vector Psychology Mapping

| Vector | Primary Psychological Triggers |
|--------|-------------------------------|
| Phishing | Urgency, authority, fear of loss |
| Vishing | Authority, real-time pressure, empathy |
| Pretexting | Trust, liking, reciprocity |
| Tailgating | Courtesy, social norms, conflict avoidance |
| Baiting | Curiosity, greed, scarcity |
| Quid pro quo | Reciprocity, helpfulness |

### Reporting Culture

The goal is not zero clicks but 100% reporting. A phishing email that is clicked AND reported within minutes is a success of the security program. Punishing victims drives concealment, not prevention.

## Cross-References

- See `reference/psychology/security-culture-psychology.md` for culture building
- See `reference/psychology/adversary-mindset-training.md` for offensive thinking
- See `frameworks/phishing-simulation-methodology.md` for simulation design
- See `reference/psychology/decision-making-under-pressure.md` for cognitive bias awareness
- See `templates/runbooks/phishing-response-runbook.md` for response procedures
