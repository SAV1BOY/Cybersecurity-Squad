# Confidence Calibration Guide

## Purpose

This guide standardizes how the squad expresses confidence levels in findings, threat intelligence assessments, recommendations, and analytical conclusions. Stating a finding without indicating confidence is like providing a measurement without units — the consumer cannot properly act on it. Calibrated confidence language prevents both false certainty and unnecessary hedging.

## Confidence Level Definitions

The squad uses a four-tier confidence framework aligned with intelligence community standards (ICD 203):

### Confirmed (Highest Confidence)

**Definition**: The assessment is based on direct, first-hand evidence that has been independently verified. The conclusion is as close to fact as analysis permits.

**Evidentiary Standard**:
- Direct observation (packet capture, log entry, artifact recovery)
- Successful reproduction in a controlled environment
- Multiple independent evidence sources corroborating the same conclusion
- Technical verification by at least two analysts

**Language**:
- "Analysis confirms that [finding]. This is based on [evidence type] verified by [method]."
- "Confirmed: [statement]. Evidence: [specific artifacts]."

**Use When**:
- You have exploited a vulnerability and captured evidence
- You have recovered malware and completed reverse engineering
- Log analysis conclusively demonstrates the stated activity
- Multiple independent detection sources agree

### Likely (High Confidence)

**Definition**: The assessment is well-supported by evidence and analytical reasoning, but some uncertainty remains. The most probable interpretation of available evidence.

**Evidentiary Standard**:
- Strong circumstantial evidence from multiple sources
- Consistent with known threat actor TTPs and infrastructure
- No significant contradictory evidence
- Minor gaps in evidence that do not undermine the core conclusion

**Language**:
- "Based on available evidence, it is likely that [assessment]. This is supported by [evidence summary]."
- "We assess with high confidence that [statement], based on [reasoning]."
- "The evidence strongly suggests [conclusion], though [specific gap] prevents full confirmation."

**Use When**:
- Indicators match known threat actor infrastructure but cannot be definitively attributed
- Behavioral analysis indicates compromise but you lack the specific artifact
- Multiple weak indicators converge on the same conclusion
- The vulnerability is theoretically exploitable but you did not complete full exploitation

### Possible (Moderate Confidence)

**Definition**: The assessment is one reasonable interpretation of the evidence, but alternative explanations exist. Additional investigation could change the conclusion.

**Evidentiary Standard**:
- Some supporting evidence, but limited in scope or quality
- Consistent with one or more hypotheses
- Notable gaps in evidence
- Some contradictory indicators present

**Language**:
- "It is possible that [assessment]. This interpretation is supported by [evidence], but [alternative explanation] cannot be ruled out."
- "We assess with moderate confidence that [statement]. Key uncertainty: [specific gap]."
- "Preliminary analysis suggests [conclusion], pending [additional investigation needed]."

**Use When**:
- A single indicator matches a known threat but could also be benign
- Anomalous activity detected but root cause not yet determined
- Threat intelligence suggests targeting of your sector but no direct indicators in your environment
- Static analysis identifies a potential vulnerability but dynamic testing has not been performed

### Unlikely (Low Confidence)

**Definition**: The assessment is based on limited, indirect, or speculative evidence. It represents a hypothesis worth tracking but should not drive significant resource allocation without further investigation.

**Language**:
- "While unlikely based on current evidence, we cannot rule out [scenario]. This assessment is based on [limited evidence]."
- "We assess with low confidence that [statement]. This is speculative and requires [specific investigation] to validate."
- "There is insufficient evidence to support [claim] at this time."

**Use When**:
- A single anomalous indicator with multiple benign explanations
- Threat actor attribution based solely on geopolitical context
- Vulnerability identified in source code but with no clear exploitation path
- Rumor or unverified reporting from low-reliability sources

## Confidence in Different Contexts

### Vulnerability Assessments
- **Confirmed**: Vulnerability exploited and impact demonstrated
- **Likely**: Vulnerability identified by scanner, version-confirmed, known exploit exists but not tested
- **Possible**: Version appears vulnerable based on banner, but fingerprinting may be inaccurate
- **Unlikely**: Theoretical vulnerability based on architecture review, no specific evidence

### Threat Intelligence
- **Confirmed**: Direct evidence of targeting (phishing email received, scanning observed from known adversary IP)
- **Likely**: Sector-specific threat advisory with IOCs matching your technology stack
- **Possible**: General threat reporting about adversary interest in your industry vertical
- **Unlikely**: Speculation based on geopolitical events with no technical indicators

### Incident Analysis
- **Confirmed**: Root cause identified with full evidence chain from initial access to impact
- **Likely**: Most evidence points to a specific attack vector, minor gaps remain
- **Possible**: Multiple potential attack vectors, investigation ongoing
- **Unlikely**: Hypothesis explored but evidence does not strongly support it

## Updating Confidence Over Time

Confidence levels are not permanent. As new evidence emerges, update assessments explicitly:

- "Previous assessment (2024-03-01): Possible compromise via phishing. Updated assessment (2024-03-05): Confirmed compromise via phishing — email artifact recovered from quarantine, credential use confirmed in authentication logs."
- Always retain the history of confidence changes with dates and the evidence that drove the change.

## Common Calibration Errors

### Overconfidence
- Treating scanner output as confirmed findings without validation
- Attributing to a specific threat actor based on a single TTP overlap
- Stating conclusions as facts when evidence is circumstantial

### Underconfidence
- Hedging confirmed findings with unnecessary qualifiers out of caution
- Using "possible" for findings you have directly verified and reproduced
- Adding disclaimers to well-supported assessments because the topic is sensitive

### Missing Confidence Statements
- Presenting findings without any confidence indicator, leaving the consumer to guess
- Mixing confirmed and possible findings in the same list without distinguishing them

## Cross-References

- See `voice/calibration/severity-calibration.md` for severity rating standards
- See `voice/calibration/attribution-calibration.md` for threat actor attribution confidence
- See `voice/language-guides/vulnerability-severity-language.md` for severity language
- See `voice/language-guides/pentest-report-language.md` for finding confidence in reports
