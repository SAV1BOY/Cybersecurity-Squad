# Presentation Delivery Guide

## Purpose

This guide standardizes how the squad presents security findings, risk assessments, and recommendations in meetings — from board presentations to technical deep-dives to all-hands awareness sessions. Security professionals are often brilliant analysts and poor presenters. This guide closes that gap. A finding that is not communicated effectively is a finding that does not get remediated.

## Presentation Types and Structures

### Type 1: Executive/Board Presentation

**Duration**: 15-30 minutes (including Q&A)
**Audience**: Board, C-suite, senior leadership
**Depth**: Level 1 (see `voice/calibration/technical-depth-calibration.md`)

**Slide Structure**:
```
Slide 1: Title — [Topic], [Date], [Presenter]
Slide 2: Bottom Line Up Front — 3 bullet points maximum
Slide 3: Risk Dashboard — visual risk posture with trend arrows
Slide 4-6: Top 3 Risks — one slide each, business impact focus
Slide 7: Investment Recommendations — prioritized with cost/benefit
Slide 8: Q&A / Discussion
```

**Rules**:
- No more than 8 slides for a 30-minute session (including title and Q&A)
- Maximum 4 bullet points per slide, maximum 10 words per bullet
- Use visuals: trend charts, heat maps, risk matrices — not paragraphs
- No live demos for executive audiences unless specifically requested
- Anticipate the CFO question: "How much does this cost and what do we get for it?"
- Anticipate the CEO question: "Are we better or worse than last quarter?"
- Anticipate the legal counsel question: "What is our liability exposure?"

### Type 2: Technical Findings Presentation

**Duration**: 30-60 minutes
**Audience**: Engineering teams, IT operations, security peers
**Depth**: Level 3-4

**Slide Structure**:
```
Slide 1: Title and scope
Slide 2: Methodology and tools
Slide 3: Summary of findings by severity (table/chart)
Slide 4-N: Individual findings with evidence
Slide N+1: Attack chain demonstration (if applicable)
Slide N+2: Remediation roadmap with priorities
Slide N+3: Q&A and next steps
```

**Rules**:
- Show the evidence: screenshots, tool output, code snippets
- Walk through attack chains step by step — show how individual findings combine
- Live demos are effective here but must be rehearsed and have fallback screenshots
- Include "what we tried that did not work" — this builds credibility and shows thoroughness
- End with a prioritized action list, not just a finding list

### Type 3: Incident Post-Mortem Review

**Duration**: 45-60 minutes
**Audience**: Response team, leadership, affected teams
**Depth**: Level 2-3

**Structure**:
```
Slide 1: Title — Incident [ID] Post-Mortem
Slide 2: Incident summary — what happened in 3 sentences
Slide 3: Timeline visualization
Slide 4-6: Contributing factors (not "root cause")
Slide 7: What went well in the response
Slide 8: What needs improvement
Slide 9: Action items with owners and deadlines
Slide 10: Discussion
```

**Rules**:
- Blameless. Focus on systems and processes, not individuals.
- Use a visual timeline — it is the most effective way to convey the sequence of events
- Dedicate equal time to what went well as what went wrong
- Every identified improvement must have an action item with an owner and a deadline
- Leave time for open discussion — post-mortems that are one-way lectures miss valuable perspective

### Type 4: Security Awareness Session

**Duration**: 15-30 minutes
**Audience**: All employees
**Depth**: Level 1

**Rules**:
- Lead with a story. Real-world examples (anonymized) are more compelling than statistics.
- Maximum three takeaways. If people remember three things, you have succeeded.
- Interactive elements: live polls, "spot the phish" exercises, Q&A
- No shaming. No "and this is what happens when you click the wrong link" with a disappointed face.
- Provide a one-page handout or follow-up email with the key actions

## Demo Preparation

### Before the Presentation
1. Test the demo in the exact environment you will present from (projector resolution, network, VPN)
2. Record a backup video of the demo in case of technical failure
3. Have pre-captured screenshots for every demo step as a fallback
4. Verify that demo credentials still work
5. Clear browser history, close personal tabs, disable notifications
6. Ensure screen sharing shows only what you intend — no sensitive data in other windows

### During the Demo
- Narrate every step: "I am now navigating to the login page and entering the test credentials"
- Zoom in on relevant portions — audience members in the back cannot read 10-point font
- Pause after showing the result: "Notice that the response includes the database contents — this confirms the SQL injection"
- If the demo breaks, switch to the backup video or screenshots without apologizing excessively. Say: "Let me show you the captured result."

### After the Demo
- Summarize what the demo proved: "This demonstrated that an external attacker can access the customer database without authentication"
- Connect the demo to the recommendation: "This is why we are recommending [specific remediation]"

## Q&A Handling

### Preparation
- Anticipate the top 5 questions for each presentation type and prepare concise answers
- Prepare a "parking lot" for questions outside the scope — acknowledge them and commit to follow up
- Know your boundaries: what you can share in this forum and what requires a different setting

### During Q&A
- Repeat the question before answering (ensures everyone heard it and gives you a moment to think)
- "That is a great question" is filler — just answer the question
- If you do not know the answer: "I do not have that data with me. I will follow up by [specific date] with the answer." Then actually follow up.
- If the question is hostile or political: acknowledge the concern, restate the facts, offer to discuss further offline. Do not get defensive.

### Difficult Questions

| Question Type | Response Strategy |
|--------------|-------------------|
| "Why did this happen?" | Focus on contributing factors, not blame. "Several factors contributed..." |
| "Who is responsible?" | "The remediation owner is [role/team]. We are working together on resolution." |
| "How do we compare to peers?" | Reference industry benchmarks if available. Do not guess. |
| "Why should we spend money on this?" | Return to the cost-benefit analysis. Quantify the risk being reduced. |
| "Can you guarantee this will not happen again?" | "We can significantly reduce the likelihood through [controls], but no guarantee eliminates all risk." |

## Slide Design Principles

- **One idea per slide**. If you need two slides, use two slides.
- **Dark text on light background** for rooms with ambient light. Avoid dark themes in well-lit conference rooms.
- **Minimum 24-point font** for body text. If you cannot fit your content at 24pt, you have too much content.
- **No clip art or stock photos** of hackers in hoodies. Use diagrams, data visualizations, and real evidence.
- **Consistent color coding**: Red = critical/bad, Yellow = warning/medium, Green = good/resolved. Do not vary this.
- **Slide numbers on every slide** — enables audience members to reference specific slides in Q&A.

## Cross-References

- See `voice/tone-profiles/executive-advisory.md` for board presentation tone
- See `voice/tone-profiles/security-educator.md` for awareness session tone
- See `voice/calibration/technical-depth-calibration.md` for audience depth matching
- See `voice/language-guides/risk-communication-language.md` for risk quantification in presentations
