# Breach Notification Template

## Purpose

Legal-ready breach notification templates for communicating data breaches to affected individuals, regulators, and other stakeholders. Covers regulatory requirements, notification timing, and multi-audience communication for compliance with GDPR, state breach notification laws, HIPAA, and other regulatory frameworks.

## Pre-Notification Checklist

- [ ] Legal counsel has reviewed all notifications
- [ ] Regulatory requirements identified for all applicable jurisdictions
- [ ] Notification timeline established (meets shortest applicable deadline)
- [ ] Affected individual count determined
- [ ] Types of data involved confirmed
- [ ] Remediation actions confirmed (credit monitoring, identity protection)
- [ ] Call center/support team briefed and ready
- [ ] FAQ document prepared for customer support
- [ ] Executive spokesperson designated for media
- [ ] Regulatory filings prepared (HHS, state AGs, ICO, etc.)

## Notification Timeline Requirements

| Regulation | Deadline | Notify |
|-----------|----------|--------|
| GDPR (EU) | 72 hours to supervisory authority | DPA + affected individuals (if high risk) |
| HIPAA (US) | 60 days to individuals; immediate to HHS if >500 | HHS, individuals, media (if >500 in state) |
| State breach laws (US) | 30-90 days (varies by state) | State AG + affected individuals |
| PCI-DSS | As soon as possible | Card brands, acquiring bank |
| CCPA/CPRA (California) | "Most expedient time possible" | Individuals, CA AG if >500 residents |
| PIPEDA (Canada) | "As soon as feasible" | Privacy Commissioner + individuals |
| SEC (public companies) | 4 business days (material incidents) | Form 8-K filing |

---

## [TEMPLATE 1: Individual Notification Letter]

```
[ORGANIZATION LETTERHEAD]

[Date]

[Recipient Name]
[Address]

RE: NOTICE OF DATA SECURITY INCIDENT

Dear [Recipient Name],

We are writing to inform you of a data security incident that may have
involved some of your personal information. We take the protection of
your information seriously, and we want to provide you with details
about the incident, the steps we have taken, and resources available
to you.

WHAT HAPPENED

On [discovery date], [Organization] identified [brief, factual
description of incident]. We immediately [containment actions taken].
Our investigation, [conducted with the assistance of leading
cybersecurity forensic experts], determined that [scope of unauthorized
access]. The incident occurred between approximately [date range].

WHAT INFORMATION WAS INVOLVED

The personal information that may have been involved includes:
- [Full name]
- [Email address]
- [Other specific data types: SSN, financial account numbers,
  medical information, etc.]

[If applicable: We have no evidence that [specific sensitive data]
was accessed or misused.]

WHAT WE ARE DOING

Upon discovering this incident, we:
- [Specific containment and remediation actions]
- [Engaged third-party forensic investigators]
- [Notified law enforcement]
- [Enhanced security measures implemented]

WHAT YOU CAN DO

We recommend that you:
- Monitor your financial accounts and credit reports for any
  unauthorized activity
- [If SSN involved: Place a fraud alert or security freeze on your
  credit files]
- Be cautious of unsolicited communications asking for personal
  information
- Report any suspected identity theft to law enforcement

COMPLIMENTARY CREDIT MONITORING AND IDENTITY PROTECTION

We are offering [N] months of complimentary credit monitoring and
identity protection services through [Provider Name]. To enroll:
- Visit: [URL]
- Use enrollment code: [CODE]
- Enrollment deadline: [Date]

FOR MORE INFORMATION

If you have questions or concerns, please contact our dedicated
assistance line:
- Phone: [Toll-free number]
- Hours: [Operating hours]
- Email: [Dedicated email address]
- Website: [Incident-specific webpage]

We sincerely apologize for any inconvenience or concern this incident
may cause you. Protecting your information is a top priority, and we
are committed to taking the steps necessary to prevent a recurrence.

Sincerely,

[Executive Name]
[Title]
[Organization]
```

---

## [TEMPLATE 2: Regulatory Notification (State Attorney General)]

```
[Date]

[State] Attorney General
[Office Address]

RE: Data Breach Notification Pursuant to [State Statute Reference]

Dear Attorney General [Name]:

Pursuant to [State breach notification law citation], [Organization]
is providing notice of a data security incident involving personal
information of [State] residents.

NATURE OF THE INCIDENT
[Factual description of the breach]

DATE OF BREACH: [Date or date range]
DATE OF DISCOVERY: [Date]
NUMBER OF [STATE] RESIDENTS AFFECTED: [Number]

TYPES OF PERSONAL INFORMATION INVOLVED:
[List specific data elements per state law definition]

ACTIONS TAKEN:
[Containment and remediation steps]

NOTICE TO AFFECTED INDIVIDUALS:
Individual notification [was sent / will be sent] on [date] via
[method: mail, email, substitute notice]. A copy of the notification
is enclosed.

SERVICES OFFERED:
[Credit monitoring and identity protection details]

CONTACT INFORMATION:
[Organization contact for AG inquiries]

Respectfully submitted,

[Name, Title]
[Organization]
[Contact Information]

Enclosures:
- Copy of individual notification letter
- [Other required materials per state law]
```

---

## [TEMPLATE 3: Media Statement]

```
STATEMENT FROM [ORGANIZATION] REGARDING DATA SECURITY INCIDENT

[City, State] - [Date] - [Organization] today announced that it
recently identified a data security incident that may have affected
certain personal information.

[Organization] discovered the incident on [date] and immediately
took steps to [containment actions]. The company engaged leading
cybersecurity experts to conduct a thorough investigation and has
notified law enforcement.

The investigation determined that [scope of incident]. The types of
information that may have been involved include [general categories,
not specifics].

[Organization] is notifying affected individuals and offering
[complimentary credit monitoring/identity protection services].

"[Quote from executive about taking security seriously, commitment
to protecting information, and steps being taken]" said [Executive
Name, Title].

Affected individuals and others with questions may contact
[Organization] at [toll-free number] or visit [website].

###

Media Contact:
[Name]
[Phone]
[Email]
```

---

## [TEMPLATE 4: Customer FAQ]

```
FREQUENTLY ASKED QUESTIONS

Q: What happened?
A: [Clear, concise explanation]

Q: When did this happen?
A: [Date range of incident and discovery date]

Q: What information was involved?
A: [Specific data types]

Q: Was my [specific data type] involved?
A: [How individuals can determine if they are affected]

Q: How did this happen?
A: [General explanation without revealing security details]

Q: What are you doing about it?
A: [Remediation actions, security improvements]

Q: What can I do to protect myself?
A: [Actionable steps for individuals]

Q: How do I enroll in credit monitoring?
A: [Specific enrollment instructions]

Q: Who can I contact with questions?
A: [Contact information]

Q: Will this happen again?
A: [Commitment to security improvements without guarantees]
```

---

## Post-Notification Actions

- [ ] Track notification delivery (mail returns, email bounces)
- [ ] Monitor call center volume and common questions
- [ ] Update FAQ based on actual inquiries received
- [ ] Respond to regulatory follow-up questions within required timeframes
- [ ] Monitor media coverage and prepare responses as needed
- [ ] Track credit monitoring enrollment rates
- [ ] Document all notification activities for compliance records
- [ ] Prepare for potential litigation (document preservation, legal hold)

## [TEMPLATE ENDS]

---

## Cross-References

- See `templates/runbooks/ransomware-response-runbook.md` for incident response
- See `templates/runbooks/phishing-response-runbook.md` for phishing incidents
- See `reference/industries/healthcare-security.md` for HIPAA breach requirements
- See `reference/industries/financial-services-security.md` for financial breach requirements
- See `frameworks/nist-800-61-incident-response.md` for IR framework alignment
