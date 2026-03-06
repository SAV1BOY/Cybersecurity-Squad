# Attribution Calibration Guide

## Purpose

This guide standardizes how the squad handles threat actor attribution — one of the most sensitive and consequential aspects of security communication. Premature or inaccurate attribution can trigger geopolitical escalation, misdirect defensive resources, create legal liability, and damage credibility. Calibrated attribution balances the need for actionable intelligence with intellectual honesty about what the evidence actually supports.

## The Attribution Spectrum

Attribution exists on a spectrum from technical indicators to strategic intent. Each level requires progressively more evidence and carries progressively more risk if wrong.

### Level 1: Technical Attribution (What)

**Question**: What tools, infrastructure, and techniques were used?
**Evidence Required**: Malware samples, network indicators, exploit code, C2 infrastructure
**Confidence Achievable**: Confirmed or Likely (with good artifacts)

**Language**:
- "The attack used [malware family] communicating with C2 infrastructure at [IP/domain]."
- "The intrusion leveraged [technique] consistent with [ATT&CK ID]."
- "Artifacts recovered include [specific items] with the following indicators: [IOC list]."

**This is the safest form of attribution.** Stick to observable facts about the technical components of the attack.

### Level 2: Campaign Attribution (Who Else)

**Question**: Is this attack linked to other known campaigns or intrusion sets?
**Evidence Required**: Shared infrastructure, code overlap, TTP clustering, victimology patterns
**Confidence Achievable**: Likely or Possible

**Language**:
- "The infrastructure and TTPs overlap with activity previously tracked as [campaign/cluster name]. Specifically: [shared indicators]."
- "Code analysis reveals [X]% overlap with [malware family] associated with [intrusion set]. However, [caveats about code reuse/false flags]."
- "Victimology and targeting patterns are consistent with [cluster] activity observed by [source] in [timeframe]."

**Caveats to include**:
- Code and tools can be shared, stolen, or deliberately planted as false flags
- Infrastructure can be compromised and reused by unrelated actors
- TTP overlap may reflect shared training or tooling rather than organizational linkage

### Level 3: Organizational Attribution (Who)

**Question**: Which threat group or organization conducted the attack?
**Evidence Required**: Multiple corroborating intelligence sources, operational patterns, human intelligence, law enforcement information
**Confidence Achievable**: Rarely above Possible for private sector teams

**Language**:
- "Based on the convergence of [evidence types], this activity is assessed as possibly linked to [group name/designation]. This assessment is made with [confidence level]."
- "Multiple reporting sources associate the observed TTPs and infrastructure with [group]. However, independent verification of this attribution is beyond the scope of this assessment."
- "We defer to [intelligence agency/vendor] reporting for organizational attribution while noting the following supporting and contradicting indicators from our analysis."

**Critical Rules**:
- Private sector teams should generally stop at Level 2 and reference vendor/government attribution rather than making original Level 3 claims
- Always include contradicting indicators alongside supporting ones
- Acknowledge the possibility of false flag operations explicitly

### Level 4: State Attribution (State Sponsor)

**Question**: Which nation-state directed or sponsored the attack?
**Evidence Required**: Classified intelligence, diplomatic sources, law enforcement operations, signals intelligence — rarely available to private sector
**Confidence Achievable**: Almost never achievable by private sector alone

**Language**:
- "Government reporting [source, date] has attributed this activity to [state]. Our technical observations are consistent with / inconsistent with this attribution."
- "We assess no independent basis for state attribution from our technical evidence alone."

**Critical Rule**: Do not make state attribution claims based solely on technical evidence. Code comments in a specific language, IP geolocation, or working-hours analysis are insufficient individually or even in combination.

## Attribution Anti-Patterns

### Premature Attribution
**Problem**: Naming a threat actor in the first 24 hours of an incident based on a single indicator.
**Risk**: Misdirects the response, creates confirmation bias in the investigation, may be weaponized politically.
**Fix**: Use placeholder designations ("the threat actor in this incident" or internal tracking names) until attribution confidence reaches at least "Likely" with multiple corroborating evidence sources.

### Attribution by Press Release
**Problem**: Attributing based solely on a vendor blog post or media report without independent verification.
**Risk**: Vendor attribution may be driven by marketing incentives, limited evidence, or access to different datasets.
**Fix**: Reference vendor attribution as a source but verify against your own evidence. "Vendor X attributes similar activity to [group]. Our evidence [supports/does not support/is insufficient to confirm] this attribution."

### Single-Source Attribution
**Problem**: Basing attribution on one type of evidence (e.g., only infrastructure overlap, or only malware similarity).
**Risk**: Each individual evidence type has well-known defeat mechanisms (VPN, code theft, false flags).
**Fix**: Require at least three independent evidence types before reaching "Likely" confidence on campaign or organizational attribution.

### Geopolitical Assumption
**Problem**: "We are a defense contractor, so it must be [nation-state]."
**Risk**: Confirmation bias from the start. Defense contractors are also targeted by cybercriminals, hacktivists, and competitors.
**Fix**: Let the evidence lead. State the assumption explicitly and challenge it during analysis.

## Internal Tracking Designations

When attribution is uncertain, use internal tracking names rather than published group names:

- Format: `[SQUAD-PREFIX]-[YEAR]-[SEQUENCE]` (e.g., `CYBER-2024-003`)
- Map to published names only when confidence supports it, with a crosswalk table
- Update the mapping as confidence evolves

**Crosswalk Table Example**:

| Internal Designation | Vendor A Name | Vendor B Name | Government Name | Confidence | Last Updated |
|---------------------|---------------|---------------|-----------------|------------|-------------|
| CYBER-2024-003 | [Group X] | [Group Y] | [APT-NN] | Possible | 2024-03-15 |

## Attribution in Different Outputs

| Output Type | Attribution Depth | Rationale |
|-------------|------------------|-----------|
| Incident alert (internal) | Level 1 only | Focus on containment, not attribution |
| Threat intelligence report | Level 1-2, possibly 3 with caveats | Analytical product with appropriate hedging |
| Executive briefing | Level 1-2, reference government attribution for Level 3-4 | Executives need context, not speculation |
| Public statement | None or Level 1 only | Legal and reputational risk of premature public attribution |
| Law enforcement referral | All levels with confidence ratings | Let law enforcement make final attribution determination |
| Regulatory notification | Level 1 only unless required otherwise | Focus on what happened, not who did it |

## Cross-References

- See `voice/calibration/confidence-calibration.md` for the confidence framework used in attribution statements
- See `voice/language-guides/incident-communication-language.md` for attribution language during incidents
- See `voice/tone-profiles/executive-advisory.md` for presenting attribution to leadership
- See `swipe-sources/threat-intel-feeds.md` for intelligence sources that inform attribution
