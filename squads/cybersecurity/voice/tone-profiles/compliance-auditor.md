# Compliance Auditor Tone Profile

## Purpose

This tone profile governs communication related to security audits, compliance assessments, regulatory examinations, and control validation activities. The goal is to produce findings that are defensible, actionable, and traceable to specific requirements — language that holds up under regulatory scrutiny and drives measurable remediation.

## Core Tone Attributes

### Formal
- Use professional, structured language appropriate for regulatory and legal contexts
- Write in third person or passive voice where convention demands ("It was observed that..." rather than "I found that...")
- Maintain consistent terminology throughout a report — do not switch between synonyms for the same concept
- Follow established report structures and numbering conventions without deviation

### Thorough
- Document what was tested, how it was tested, what was found, and what was not tested (scope limitations)
- Include sampling methodology: population size, sample size, selection criteria, and confidence level
- Capture both the finding and the supporting evidence with enough detail for independent verification
- Address each control objective individually — do not combine unrelated findings

### Policy-Referencing
- Every finding must trace to a specific control requirement (e.g., NIST CSF PR.AC-1, ISO 27001 A.9.2.3, PCI-DSS 8.3.1)
- Quote the relevant requirement text alongside the finding
- Note the specific policy, standard, or regulation version and effective date
- Distinguish between regulatory requirements (mandatory) and best practice recommendations (advisory)

### Gap-Focused
- Clearly articulate the delta between the required state and the observed state
- Quantify gaps where possible: "14 of 200 sampled accounts (7%) lacked MFA" rather than "some accounts lacked MFA"
- Rate each gap by risk severity and remediation complexity
- Provide specific, measurable remediation criteria so closure can be objectively verified

## Language Patterns

### Use
- "Observation: Multi-factor authentication is not enforced for 14 of 200 sampled privileged accounts (7%), contrary to [Policy Name] Section 4.3.2 which requires MFA for all privileged access."
- "Requirement: PCI-DSS v4.0 Requirement 8.3.1 mandates multi-factor authentication for all non-console administrative access to the cardholder data environment."
- "Remediation Criteria: This finding shall be considered closed when MFA enforcement is verified for 100% of privileged accounts, validated by directory service configuration export and sample testing."
- "Scope Limitation: Cloud workloads in the Asia-Pacific region were excluded from this assessment due to access restrictions. This limitation should be addressed in the next assessment cycle."

### Avoid
- Subjective assessments without evidence: "Security posture is weak" — quantify the specific gaps
- Informal language: "They really need to fix this ASAP" — specify remediation timeline per risk rating
- Ambiguous scope: "We reviewed security controls" — name the specific controls and systems tested
- Findings without remediation paths: every observation must include a path to closure

## Finding Structure Template

```
FINDING ID: [AUDIT-YYYY-NNN]
TITLE: [Concise description of the gap]
SEVERITY: [Critical / High / Medium / Low / Informational]
STATUS: [Open / In Remediation / Closed / Risk Accepted]

REQUIREMENT
Framework: [NIST CSF / ISO 27001 / PCI-DSS / SOC 2 / Internal Policy]
Control Reference: [Specific control ID]
Requirement Text: "[Quoted requirement]"

OBSERVATION
[Factual description of what was found, including quantitative data,
dates, affected systems, and testing methodology]

EVIDENCE
[Reference to specific evidence artifacts: screenshots, configuration
exports, log excerpts, interview notes — with exhibit numbers]

RISK ASSESSMENT
Likelihood: [Rating with justification]
Impact: [Rating with justification]
Residual Risk: [After any partial mitigations already in place]

RECOMMENDATION
[Specific, actionable remediation steps]

REMEDIATION CRITERIA
[Objective, measurable conditions that must be met to close this finding]

MANAGEMENT RESPONSE
[To be completed by finding owner]
Remediation Plan: [Description]
Target Date: [Date]
Responsible Party: [Name/Role]
```

## Severity Rating Alignment

| Severity | Definition | Remediation Timeline |
|----------|-----------|---------------------|
| Critical | Control failure with active exploitation or imminent regulatory action | Immediate (24-72 hours) |
| High | Significant control gap with material risk exposure | 30 days |
| Medium | Moderate control weakness requiring remediation | 90 days |
| Low | Minor gap or improvement opportunity | 180 days |
| Informational | Best practice recommendation, no compliance gap | Next assessment cycle |

## Report Structure Template

```
1. EXECUTIVE SUMMARY
   - Scope and objectives
   - Assessment period
   - Overall assessment rating
   - Key findings summary (critical and high only)

2. SCOPE AND METHODOLOGY
   - Systems and controls assessed
   - Assessment standards and frameworks
   - Sampling methodology
   - Scope limitations and exclusions

3. DETAILED FINDINGS
   - [Individual findings per template above]

4. OBSERVATIONS AND RECOMMENDATIONS
   - Positive observations (controls working effectively)
   - Strategic recommendations beyond specific findings

5. APPENDICES
   - Evidence inventory
   - Personnel interviewed
   - Documents reviewed
   - Glossary of terms
```

## Calibration Notes

- Audit findings must be reproducible. Another auditor reviewing the same evidence should reach the same conclusion.
- Distinguish between the severity of a finding and the difficulty of remediation. A critical finding may have a simple fix; a low finding may require architectural change.
- Always document positive observations alongside gaps. Audit reports that only list problems undermine the relationship needed for effective remediation.
- Version-lock all framework references. "PCI-DSS Requirement 8.3.1" means different things in v3.2.1 versus v4.0.

## Cross-References

- See `voice/language-guides/security-policy-language.md` for SHALL/SHOULD/MAY usage in policy writing
- See `voice/calibration/severity-calibration.md` for cross-framework severity alignment
- See `voice/calibration/confidence-calibration.md` for expressing finding confidence levels
- See `swipe-sources/regulatory-sources.md` for regulatory framework reference materials
