# Technical Operator Tone Profile

## Purpose

This tone profile governs communication directed at SOC analysts, penetration testers, detection engineers, threat hunters, and other hands-on security practitioners. The goal is maximum signal, minimum noise — every word should either convey actionable intelligence or provide necessary technical context.

## Core Tone Attributes

### Precise
- Use exact technical terminology — no paraphrasing protocol names, attack techniques, or tool outputs
- Reference MITRE ATT&CK technique IDs (e.g., T1059.001), CVE identifiers, and CWE classifications
- Specify versions, hashes, IP addresses, timestamps (UTC always), and log sources
- Distinguish between observed behavior and inferred intent

### Evidence-Based
- Every claim links to a log entry, packet capture, artifact, or reproducible test
- Screenshots and command output are expected, not optional
- Clearly separate facts from analysis from hypothesis
- Cite detection logic: what rule/signature/query fired and why

### Action-Oriented
- Lead with what the operator needs to do, then explain why
- Provide exact commands, queries, or procedures — not vague instructions
- Include rollback steps for any recommended change
- Specify expected outcomes so the operator can verify success

### No Fluff
- Eliminate filler words, pleasantries, and unnecessary context
- Do not explain basic concepts to a technical audience
- Use sentence fragments and bullet points when they improve clarity
- One-line summaries beat paragraphs when the content supports it

## Language Patterns

### Use
- "Observed C2 beaconing to 198.51.100.23:443 at 2024-03-15T14:32:00Z (T1071.001). Source: host WKSTN-042, PID 4728 (rundll32.exe)."
- "Run: `Get-WinEvent -LogName Security -FilterXPath "*[System[EventID=4688]]" | Where-Object {$_.Properties[5].Value -match 'powershell'}`"
- "Confirmed: vulnerable to CVE-2024-XXXX. Exploit requires authenticated access to /api/v2/admin endpoint. PoC attached."
- "False positive. Alert triggered on scheduled backup job. Tuning recommendation: exclude service account SVC-BACKUP from rule ID 4471."

### Avoid
- "I believe this might possibly be a security concern" — state what it is
- Vague remediation: "patch the system" — specify which patch, which system, which method
- Narrative writing when structured data would serve better
- Emotional language: "devastating attack" — describe the technical impact factually

## Structure Template for Technical Findings

```
## [Finding Title] — [Severity]

**MITRE ATT&CK:** T[XXXX.XXX] — [Technique Name]
**Affected Asset(s):** [hostname/IP/service]
**Detection Source:** [rule/alert/manual hunt]

### Observation
[Exact technical description of what was found with timestamps and evidence]

### Analysis
[What the evidence indicates, attack chain context, lateral movement potential]

### Recommended Action
1. [Immediate containment step with exact command/procedure]
2. [Remediation step with specific patch/config change]
3. [Verification step to confirm resolution]

### Evidence
- [Log excerpt, screenshot, hash, or artifact reference]

### References
- [CVE link, vendor advisory, ATT&CK page]
```

## Operator-Specific Conventions

- **SOC Analysts**: Include detection rule IDs, SIEM query syntax, and triage decision trees
- **Pentest Teams**: Include full attack chains, tool configurations, and cleanup procedures
- **Threat Hunters**: Include hypothesis, data sources queried, hunt query syntax, and null results (what was NOT found is also valuable)
- **Detection Engineers**: Include rule logic, test cases (true positive and benign triggers), and performance impact estimates

## Calibration Notes

- Technical operators respect brevity and precision above all else. Padding a finding with unnecessary context signals inexperience.
- When in doubt, include the raw data. Operators prefer to draw their own conclusions from evidence.
- Use code blocks liberally for commands, queries, log excerpts, and configuration snippets.
- Timestamps must always be in UTC with explicit timezone notation.

## Cross-References

- See `voice/language-guides/pentest-report-language.md` for formal report writing standards
- See `voice/calibration/severity-calibration.md` for consistent severity rating criteria
- See `voice/language-guides/vulnerability-severity-language.md` for CVSS contextualization
