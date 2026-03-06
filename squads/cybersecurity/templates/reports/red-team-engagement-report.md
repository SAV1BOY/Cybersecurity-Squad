# Red Team Engagement Report Template

## Purpose

Full red team engagement report template for documenting objectives, attack narratives, findings, and recommendations. Structured for both executive and technical audiences with clear attack path visualization.

---

## [TEMPLATE BEGINS]

# Red Team Engagement Report

**Client**: [Organization Name]
**Engagement ID**: [RT-YYYY-NNN]
**Classification**: [Confidential]
**Report Date**: [YYYY-MM-DD]
**Assessment Period**: [Start Date] to [End Date]
**Red Team Lead**: [Name]
**Report Version**: [1.0]

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [Date] | [Author] | Initial report |
| [1.1] | [Date] | [Author] | [Changes] |

---

## 1. Executive Summary

### 1.1 Engagement Overview

[2-3 paragraphs describing: scope, objectives, methodology, and key outcomes. Written for executive audience.]

### 1.2 Key Findings Summary

| # | Finding | Severity | Objective Achieved |
|---|---------|----------|-------------------|
| 1 | [Finding title] | [Critical/High/Medium/Low] | [Yes/No/Partial] |
| 2 | [Finding] | [Severity] | [Status] |
| 3 | [Finding] | [Severity] | [Status] |

### 1.3 Objective Achievement

| Objective | Status | Notes |
|-----------|--------|-------|
| [Obj 1: e.g., Achieve domain admin] | [Achieved/Not Achieved/Partial] | [Brief note] |
| [Obj 2: e.g., Access PII database] | [Status] | [Notes] |
| [Obj 3: e.g., Exfiltrate test data] | [Status] | [Notes] |

### 1.4 Risk Rating

**Overall Security Posture**: [Critical / High / Medium / Low] Risk

---

## 2. Scope and Rules of Engagement

### 2.1 Scope

**In Scope**:
- [Networks/systems/applications in scope]
- [Physical locations if applicable]
- [Personnel (social engineering authorized?)]

**Out of Scope**:
- [Excluded systems/networks]
- [Excluded attack types]
- [Third-party systems]

### 2.2 Rules of Engagement

| Rule | Detail |
|------|--------|
| Testing window | [Dates and times] |
| Denied techniques | [DoS, data destruction, etc.] |
| Emergency contact | [Name, phone, email] |
| Notification triggers | [When to notify blue team / management] |
| Data handling | [How sensitive data encountered during testing is handled] |

### 2.3 Threat Model

**Assumed adversary profile**: [APT / Organized crime / Insider / Opportunistic]
**Initial access assumption**: [External no-knowledge / Assumed breach / Insider position]

---

## 3. Attack Narrative

### 3.1 Phase 1: Reconnaissance

[Narrative description of reconnaissance activities, discoveries, and decisions made]

**Key Discoveries**:
- [Discovery 1]
- [Discovery 2]

**Time Spent**: [X hours/days]

### 3.2 Phase 2: Initial Access

[Detailed narrative of how initial access was achieved, including failed attempts]

**Technique Used**: [MITRE ATT&CK technique ID and name]
**Target**: [System/person targeted]
**Result**: [Access obtained, with what privileges]

### 3.3 Phase 3: Privilege Escalation

[Narrative of escalation from initial access to higher privileges]

**Path**: [Initial user] -> [Technique] -> [Higher privilege]
**Detection**: [Was this detected by blue team? Y/N, details]

### 3.4 Phase 4: Lateral Movement

[Narrative of movement across the network to reach objectives]

**Path**: [System A] -> [Technique] -> [System B] -> [Technique] -> [Objective]

### 3.5 Phase 5: Objective Achievement

[Description of how each objective was completed or why it was not]

### 3.6 Attack Path Diagram

```
[ASCII or reference to visual diagram showing the complete attack chain]

Internet -> Phishing (User A) -> Workstation WS-001 -> Credential Dump
  -> Lateral Movement (PsExec) -> Server SRV-DB-01 -> Database Access
  -> Data Exfiltration (HTTPS) -> Objective Complete
```

---

## 4. Detailed Findings

### Finding 1: [Title]

**Severity**: [Critical/High/Medium/Low]
**MITRE ATT&CK**: [Technique ID]
**CVSS Score**: [If applicable]

**Description**: [What was found]
**Evidence**: [Screenshots, logs, commands used - redacted as needed]
**Impact**: [What an attacker could achieve]
**Affected Systems**: [List of affected systems]
**Recommendation**: [Specific remediation steps]
**Priority**: [Immediate / 30 days / 90 days]

[Repeat for each finding]

---

## 5. Detection and Response Analysis

### 5.1 Blue Team Detection Summary

| Attack Phase | Detected | Time to Detect | Response |
|-------------|----------|---------------|----------|
| Reconnaissance | [Y/N] | [Time] | [Action taken] |
| Initial Access | [Y/N] | [Time] | [Action taken] |
| Privilege Escalation | [Y/N] | [Time] | [Action taken] |
| Lateral Movement | [Y/N] | [Time] | [Action taken] |
| Objective Achievement | [Y/N] | [Time] | [Action taken] |

### 5.2 Detection Gaps

| Gap | MITRE ATT&CK Technique | Recommended Detection |
|-----|----------------------|----------------------|
| [Gap description] | [T-XXXX] | [Detection rule recommendation] |

---

## 6. Recommendations

### 6.1 Immediate Actions (0-30 days)

1. [Action with specific implementation guidance]
2. [Action]

### 6.2 Short-Term (30-90 days)

1. [Action]
2. [Action]

### 6.3 Strategic (90+ days)

1. [Action]
2. [Action]

---

## 7. Appendices

### A. Tools Used
### B. MITRE ATT&CK Mapping
### C. Raw Evidence (Encrypted)
### D. Remediation Verification Plan

## [TEMPLATE ENDS]

---

## Cross-References

- See `templates/briefs/red-team-engagement-brief.md` for engagement scoping
- See `frameworks/red-team-maturity-model.md` for maturity assessment
- See `frameworks/offense-layer.md` for offensive methodology
- See `frameworks/finding-structure-standard.md` for finding format
- See `frameworks/evidence-standard.md` for evidence documentation
