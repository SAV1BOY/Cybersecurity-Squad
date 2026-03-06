# Decision-Making Under Pressure

## Purpose

Guide for improving decision quality during security incidents and high-stress operations. Covers cognitive biases that degrade decisions, stress inoculation techniques, structured decision frameworks, and crisis leadership principles for incident commanders and SOC analysts.

## Cognitive Threats to Decision Quality

### Stress-Induced Cognitive Degradation

| Factor | Effect on Decisions | Mitigation |
|--------|-------------------|------------|
| Tunnel vision | Focus narrows, miss peripheral indicators | Assign dedicated scope monitor |
| Premature closure | Lock onto first plausible hypothesis | Force generation of 3 alternatives |
| Anchoring | Over-weight initial information | Rotate lead analyst mid-incident |
| Confirmation bias | Seek evidence supporting current theory | Assign devil's advocate role |
| Sunk cost fallacy | Continue failing approach due to investment | Time-box all containment actions |
| Groupthink | Team converges without challenge | Require independent analysis before group discussion |
| Availability bias | Over-weight recent or vivid events | Reference historical data and baselines |

### Fatigue and Circadian Impact

- Decision quality degrades significantly after 4-6 hours of continuous incident response
- Errors increase 30% during overnight shifts (0200-0600)
- Caffeine provides alertness but not judgment improvement
- Sleep debt is cumulative and cannot be resolved by a single rest period

## Decision Frameworks for Incidents

### OODA Loop (Boyd's Framework)

| Phase | IR Application | Key Actions |
|-------|---------------|-------------|
| Observe | Collect telemetry, alerts, logs | Aggregate all data sources into single timeline |
| Orient | Contextualize with threat intel, history | Map to MITRE ATT&CK, compare to known TTPs |
| Decide | Select containment/eradication action | Use pre-approved playbook actions where possible |
| Act | Execute decision, measure outcome | Document action, verify effectiveness, re-enter loop |

Speed through the OODA loop is a competitive advantage against the adversary. Pre-built playbooks accelerate the Orient and Decide phases.

### Recognition-Primed Decision Making (RPD)

Experienced analysts recognize patterns from past incidents:

1. **Situation recognized**: "This looks like the credential stuffing pattern from Q3"
2. **Mental simulation**: "If I block the source IP range, will that contain it?"
3. **Action evaluation**: "Are there downstream effects I'm not considering?"
4. **Execute or adapt**: Take action or modify approach if simulation reveals issues

RPD works well for experienced operators. Junior analysts benefit more from structured checklists.

### 10-10-10 Framework for Escalation Decisions

When facing a difficult escalation or communication decision:

- How will I feel about this decision in **10 minutes**? (Emotional check)
- How will I feel about it in **10 months**? (Strategic perspective)
- How will I feel about it in **10 years**? (Career/ethical lens)

Use this to counter both over-reaction (panic escalation) and under-reaction (hoping it goes away).

### Pre-Authorization Matrix

Establish before incidents occur:

| Severity | Pre-Authorized Actions | Requires Approval |
|----------|----------------------|-------------------|
| Critical | Isolate host, block IP, disable account, preserve evidence | Network segment isolation, public communication |
| High | Block IP, disable account, deploy additional monitoring | Production system changes |
| Medium | Deploy additional monitoring, request forensic image | Account disablement, IP blocks |
| Low | Investigate and document | Any active response |

## Stress Inoculation Training

### Progressive Exposure Model

1. **Education Phase**: Teach stress responses and coping mechanisms
2. **Skill Acquisition**: Practice decisions in low-stress tabletop exercises
3. **Graduated Exposure**: Increasingly realistic simulations with time pressure
4. **Full Simulation**: Unannounced exercises with realistic adversary behavior
5. **Real-World Application**: Apply skills in actual incidents with mentor support

### Tabletop Exercise Structure

```
Duration: 2-4 hours
Participants: Full IR team + management
Injects: 8-12 scenario developments at increasing severity
Evaluation: Decision quality, communication, escalation appropriateness
Deliverable: After-action report with improvement items
```

### Simulation Stress Factors (Progressive)

| Level | Added Stressor |
|-------|---------------|
| 1 | Time pressure (decisions within 15 minutes) |
| 2 | Incomplete information (logs unavailable) |
| 3 | Conflicting information (false positives mixed in) |
| 4 | Leadership pressure (simulated executive demands) |
| 5 | Media attention (simulated press inquiries) |
| 6 | Cascading failures (new incidents during response) |
| 7 | Personnel unavailability (key team members "unreachable") |

## Crisis Leadership Principles

### Incident Commander Responsibilities

1. **Own the decision**: The IC makes the call; distributed decision-making fails under pressure
2. **Communicate intent**: Share the "why" behind decisions so the team can adapt autonomously
3. **Manage energy**: Enforce breaks, rotations, and handoffs before fatigue degrades the team
4. **Control information flow**: Single source of truth, structured updates, no side-channel speculation
5. **Escalate early**: Over-communication to leadership is always better than surprise

### Communication Under Pressure

| Principle | Practice |
|-----------|----------|
| Brevity | Use structured formats (SITREP template) |
| Clarity | Avoid jargon with non-technical stakeholders |
| Frequency | Regular cadence (every 30-60 min during active incident) |
| Honesty | Report unknowns explicitly ("We do not yet know X") |
| Separation | Different messages for technical team vs. leadership vs. legal |

### Team Self-Regulation Techniques

- **Box breathing** (4-4-4-4): Inhale 4s, hold 4s, exhale 4s, hold 4s
- **Verbalize reasoning**: Speaking analysis aloud catches logical errors
- **Buddy check**: Partner reviews decisions before execution
- **Micro-breaks**: 2-minute stand-up every 60 minutes minimum
- **Mandatory handoff**: No analyst works more than 6 hours without rotation

## Post-Incident Decision Review

Conduct blameless review of all key decisions:

1. What information was available at the time of the decision?
2. What alternatives were considered?
3. What was the reasoning behind the chosen action?
4. With hindsight, was the decision reasonable given available information?
5. What would improve the decision process for next time?

The goal is process improvement, not blame assignment.

## Cross-References

- See `reference/psychology/analyst-burnout-prevention.md` for long-term wellness
- See `reference/psychology/social-engineering-psychology.md` for cognitive bias exploitation
- See `frameworks/nist-800-61-incident-response.md` for IR framework alignment
- See `workflows/incident-response-workflow.md` for operational workflow
- See `templates/runbooks/ransomware-response-runbook.md` for structured response
