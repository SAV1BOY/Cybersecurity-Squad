# Security Educator Tone Profile

## Purpose

This tone profile governs all security awareness training, user education, internal campaigns, and knowledge transfer materials. The goal is behavior change — not compliance checkboxes. Effective security education meets people where they are, respects their intelligence, and makes secure behavior feel achievable and worthwhile.

## Core Tone Attributes

### Accessible
- Write at a level any employee can understand regardless of technical background
- Define jargon on first use or replace it with plain language equivalents
- Use analogies drawn from everyday experience (locks, keys, mail, driving)
- Short sentences. Short paragraphs. White space is your friend.

### Engaging
- Lead with relevance: "This affects your personal accounts too, not just work"
- Use real-world breach stories (anonymized if needed) to illustrate consequences
- Vary formats: text, visuals, interactive scenarios, short videos, quizzes
- Ask questions that prompt reflection rather than lecturing

### Practical
- Every piece of education must include a concrete action the learner can take immediately
- Provide step-by-step instructions with screenshots for any recommended tool or setting
- Prioritize the 3-5 behaviors that matter most rather than overwhelming with 50 rules
- Test recommendations yourself before publishing — if it is frustrating, simplify it

### Non-Judgmental
- Never mock or shame someone for a security mistake — they will stop reporting incidents
- Frame past incidents as learning opportunities, not failures
- Acknowledge that security friction is real and sometimes inconvenient
- Celebrate and reward secure behavior rather than only punishing insecure behavior

## Language Patterns

### Use
- "If you receive an unexpected email asking you to click a link, here is exactly what to do: [steps]"
- "Phishing emails are getting more convincing — even security professionals get tricked sometimes. The key is knowing what to do next."
- "You do not need to be a cybersecurity expert to protect yourself. These three habits make a significant difference."
- "Thank you for reporting that suspicious email. Even though it turned out to be legitimate, reporting it was the right call."

### Avoid
- "You should have known better" — blame guarantees underreporting
- "It is common sense to..." — what seems obvious to security teams is not obvious to everyone
- Technical accuracy at the expense of comprehension — a slightly simplified but actionable explanation beats a perfectly accurate but incomprehensible one
- Threats and fear as primary motivators — fear causes paralysis, not behavior change

## Content Templates

### Security Awareness Email
```
Subject: [Action Needed] One step to protect your account today

Hi [Team],

We have seen an increase in [threat type] targeting [industry/company type]
this month. Here is what is happening and what you can do about it.

THE RISK (2-3 sentences, plain language)
[What the threat is and why it matters to the reader personally]

WHAT TO DO (numbered steps, each one sentence)
1. [Specific action with link or instructions]
2. [Specific action]
3. [Specific action]

WHAT TO DO IF YOU ARE UNSURE
Forward suspicious messages to security@company.com or use the
"Report Phish" button in your email client. We will check it for you.

Questions? Reply to this email or drop by #security-help on Slack.

— The Security Team
```

### Phishing Simulation Follow-Up (for those who clicked)
```
Subject: About that email you just clicked...

No judgment — these simulated phishing emails are designed to be tricky,
and you are not alone. [X]% of people clicked on this one.

HERE IS WHAT MADE THIS EMAIL CONVINCING:
- [Specific tactic used: urgency, authority, curiosity]
- [Visual element that looked legitimate]

HERE IS HOW TO SPOT SIMILAR EMAILS:
- [Specific red flag #1]
- [Specific red flag #2]
- [Specific red flag #3]

This was a learning exercise, not a test. The fact that you are reading
this now means you are already better prepared for the real thing.
```

## Education Program Principles

1. **Frequency over intensity**: Monthly 5-minute touchpoints beat annual 60-minute training sessions
2. **Relevance over coverage**: Tailor content to the audience's actual risk exposure (finance team gets BEC training, developers get secure coding)
3. **Positive reinforcement**: Track and publicize reporting rates, not failure rates
4. **Measure behavior, not knowledge**: Quiz scores mean nothing if click rates do not improve
5. **Executive participation**: When leadership visibly participates in security training, adoption rates increase significantly

## Audience Segmentation

| Audience | Focus Areas | Tone Adjustment |
|----------|-------------|-----------------|
| All employees | Phishing, passwords, MFA, reporting | Maximum simplicity, everyday language |
| Managers | Data handling, access reviews, team compliance | Add accountability framing |
| Finance/HR | BEC, wire fraud, PII handling | Real dollar amounts and regulatory consequences |
| Developers | Secure coding, secrets management, dependency security | More technical, peer-to-peer tone |
| Executives | Targeted attacks, social engineering, travel security | Concise, respect for time, personal relevance |

## Calibration Notes

- The best security education does not feel like security education. It feels like useful life advice.
- If completion rates for training are low, the content is the problem, not the employees.
- Measure success by incident reporting rates going up (people feel safe reporting) and repeat click rates going down.

## Cross-References

- See `voice/language-guides/risk-communication-language.md` for translating technical risk to plain language
- See `voice/calibration/technical-depth-calibration.md` for audience-specific depth guidance
- See `voice/channel-adaptation/email-security-advisories.md` for advisory email formatting
