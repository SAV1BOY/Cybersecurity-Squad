# Security Policy Language Guide

## Purpose

This guide standardizes how the squad writes, reviews, and communicates security policies. A well-written policy is enforceable, auditable, and understandable. A poorly written policy is shelfware that creates compliance gaps while giving the illusion of governance. Every word in a security policy carries weight — ambiguity is a vulnerability.

## RFC 2119 Keyword Usage

Security policies must use requirement-level keywords consistently, following the conventions of RFC 2119:

| Keyword | Meaning | Usage |
|---------|---------|-------|
| **SHALL** / **MUST** | Absolute requirement, no exceptions without formal approval | Mandatory controls, regulatory requirements |
| **SHALL NOT** / **MUST NOT** | Absolute prohibition | Actions that are never permitted |
| **SHOULD** | Recommended, expected in most cases, deviation requires justification | Best practices, strongly recommended controls |
| **SHOULD NOT** | Discouraged, deviation requires justification | Practices that are generally inadvisable |
| **MAY** | Truly optional, at the discretion of the implementer | Optional enhancements, suggested approaches |

### Common Mistakes

- **Using "should" when you mean "shall"**: If non-compliance would create a material risk or regulatory violation, use SHALL. "Should" gives people permission to skip it.
- **Using "must" everywhere**: If everything is mandatory, nothing is prioritized. Reserve SHALL/MUST for true requirements.
- **Mixing keywords inconsistently**: Do not use "shall" in one section and "must" in another for the same requirement level. Pick one convention and document it.

## Policy Document Structure

```
POLICY TITLE: [Descriptive name]
POLICY ID: [POL-SEC-NNNN]
VERSION: [X.Y]
EFFECTIVE DATE: [Date]
LAST REVIEWED: [Date]
NEXT REVIEW: [Date]
OWNER: [Role/Department]
APPROVER: [Role]
CLASSIFICATION: [Internal / Confidential]

1. PURPOSE
   [One paragraph: why this policy exists and what risk it addresses]

2. SCOPE
   [Who and what this policy applies to — be explicit about inclusions
   and exclusions]

3. DEFINITIONS
   [Define every term that could be ambiguous. Include acronyms.]

4. POLICY STATEMENTS
   [Numbered, actionable requirements using RFC 2119 keywords]

5. ROLES AND RESPONSIBILITIES
   [Who is responsible for implementing, enforcing, and monitoring
   each requirement]

6. EXCEPTIONS
   [How to request an exception, who approves, documentation
   requirements, maximum exception duration, review cadence]

7. ENFORCEMENT
   [Consequences for non-compliance, progressive discipline model,
   investigation process]

8. RELATED DOCUMENTS
   [Standards, procedures, guidelines that support this policy]

9. REVISION HISTORY
   [Table: version, date, author, description of changes]
```

## Writing Effective Scope Definitions

### Good Scope Language
- "This policy applies to all employees, contractors, temporary workers, and third-party personnel who access [Company] information systems, regardless of location or device ownership."
- "This policy covers all information systems owned, operated, or managed by [Company], including cloud-hosted services procured by any business unit."
- "Systems classified as 'development-only' with no access to production data are excluded from Section 4.3 (encryption at rest) but remain subject to all other provisions."

### Bad Scope Language
- "This policy applies to relevant systems." (What is "relevant"?)
- "All employees should follow this policy." ("Should" — so it is optional?)
- "This covers our IT infrastructure." (Does that include cloud? SaaS? Shadow IT? BYOD?)

## Writing Enforceable Policy Statements

### Enforceable
- "All privileged accounts SHALL use multi-factor authentication. Service accounts that cannot support MFA SHALL be documented in the exception register with compensating controls approved by the CISO."
- "Portable storage devices SHALL NOT be connected to systems within the cardholder data environment. Authorized exceptions require written approval from the Data Security Manager and SHALL be logged."

### Unenforceable
- "Users should try to use strong passwords." (Vague, optional, unmeasurable)
- "Sensitive data must be protected appropriately." (What is "sensitive"? What is "appropriately"?)
- "Security best practices should be followed." (Which practices? By whom? How verified?)

### The Enforceability Test

For each policy statement, ask:
1. Can I objectively determine whether this statement is being followed? (Measurable)
2. Is there a specific person or role responsible for compliance? (Accountable)
3. Is the consequence for non-compliance defined? (Enforceable)
4. Can this be verified through technical controls or audit? (Auditable)

If any answer is no, rewrite the statement.

## Exception Handling Language

```
EXCEPTION REQUEST REQUIREMENTS:
1. The requesting party SHALL submit a formal exception request
   documenting:
   a. The specific policy requirement for which an exception is sought
   b. The business justification for the exception
   c. The risk assessment of operating without the required control
   d. Proposed compensating controls
   e. Requested exception duration (maximum 12 months)

2. Exceptions SHALL be approved by [authority level based on risk]:
   - Low risk: Security Operations Manager
   - Medium risk: Director of Information Security
   - High/Critical risk: CISO

3. All approved exceptions SHALL be:
   a. Documented in the exception register
   b. Reviewed at minimum every [90/180] days
   c. Revoked if compensating controls are not maintained
   d. Reported to the security governance committee quarterly
```

## Versioning and Review Language

- "This policy SHALL be reviewed at minimum annually, or upon significant changes to the threat landscape, regulatory environment, or organizational structure."
- "Substantive changes require re-approval by [approver]. Editorial corrections (grammar, formatting) may be made by the policy owner and documented in the revision history."
- "The effective date of a new version SHALL be no less than 30 days after publication to allow for training and implementation, unless an emergency revision is declared by the CISO."

## Cross-References

- See `voice/tone-profiles/compliance-auditor.md` for audit-appropriate policy referencing
- See `voice/calibration/severity-calibration.md` for aligning policy requirements to risk severity
- See `swipe-sources/regulatory-sources.md` for regulatory framework sources that inform policy requirements
