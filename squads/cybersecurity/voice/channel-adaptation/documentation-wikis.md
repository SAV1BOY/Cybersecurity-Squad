# Documentation and Wiki Communication Guide

## Purpose

This guide standardizes how the squad creates and maintains security documentation in wikis (Confluence, Notion, SharePoint, GitBook, or equivalent). Security documentation is the institutional memory of the team — runbooks, architecture decisions, policies, procedures, and lessons learned. Well-maintained documentation enables consistent operations regardless of who is on shift. Poorly maintained documentation is worse than no documentation because it creates false confidence.

## Documentation Categories

### Runbooks (Operational)

**Purpose**: Step-by-step procedures for recurring security operations tasks.
**Audience**: SOC analysts, security engineers, on-call responders
**Update Cadence**: After every use that reveals a gap or change

**Structure**:
```
# Runbook: [Procedure Name]
**ID**: RB-[NNN]
**Last Verified**: [Date — the date someone actually followed this runbook and confirmed it works]
**Owner**: [Name/Role]
**Estimated Duration**: [Time]

## Prerequisites
- [ ] [Access/permission required]
- [ ] [Tool/system required]
- [ ] [Knowledge required]

## Procedure
### Step 1: [Action]
[Exact instructions. Include commands, screenshots, and expected output.]

Expected result: [What you should see if this step succeeds]
If this fails: [Troubleshooting step or escalation path]

### Step 2: [Action]
[Continue with the same detail level]

## Verification
[How to confirm the procedure was completed successfully]

## Rollback
[How to undo this procedure if something goes wrong]

## Revision History
| Date | Author | Change |
|------|--------|--------|
```

**Critical Rule**: A runbook that has not been verified in the last 90 days should be flagged for review. Systems change. Runbooks that have not kept pace are dangerous.

### Architecture and Design Documents

**Purpose**: Record security architecture decisions, network diagrams, data flow maps, and control implementations.
**Audience**: Security architects, engineers, auditors
**Update Cadence**: With every significant architecture change, reviewed quarterly

**Structure**:
```
# [System/Service] Security Architecture

## Overview
[What this system does, its business criticality, data classification]

## Architecture Diagram
[Embed or link to current diagram — include date of last update]

## Security Controls
| Control Category | Implementation | Status |
|-----------------|---------------|--------|
| Authentication | [Specific mechanism] | [Active/Planned/Gap] |
| Authorization | [Specific mechanism] | [Active/Planned/Gap] |
| Encryption in Transit | [Protocol/version] | [Active/Planned/Gap] |
| Encryption at Rest | [Mechanism/key mgmt] | [Active/Planned/Gap] |
| Logging | [What is logged, where] | [Active/Planned/Gap] |
| Network Segmentation | [Zones, firewall rules] | [Active/Planned/Gap] |

## Data Flow
[Describe data flows with sensitivity classification at each point]

## Threat Model
[Link to threat model document or summarize key threats and mitigations]

## Dependencies
[Upstream and downstream systems, third-party services]

## Decision Log
| Date | Decision | Rationale | Decided By |
|------|----------|-----------|------------|
```

### Knowledge Base Articles

**Purpose**: Reference material for common questions, tool usage, process explanations.
**Audience**: Varies — tag with audience level
**Update Cadence**: As needed, reviewed semi-annually

**Structure**:
```
# [Topic]
**Audience**: [SOC / Engineering / All Staff]
**Last Reviewed**: [Date]

## Summary
[Brief overview in 2-3 sentences]

## Details
[Comprehensive explanation with examples]

## Common Questions
### [Question 1]
[Answer]

### [Question 2]
[Answer]

## Related Resources
- [Link to related articles]
```

## Documentation Standards

### Writing Standards
- **Active voice**: "The analyst runs the query" not "The query is run by the analyst"
- **Present tense**: "This runbook describes" not "This runbook will describe"
- **Imperative for procedures**: "Run the following command" not "You should run the following command"
- **Consistent terminology**: Maintain a glossary page and reference it. Do not use "server," "host," and "machine" interchangeably in the same document if they mean the same thing.

### Structural Standards
- Every page has an owner (specific person or role, not "the team")
- Every page has a "last reviewed" date that is updated when someone verifies the content
- Every page has a clear audience tag
- Table of contents auto-generated for pages longer than three sections
- Code blocks with language syntax highlighting for all commands, queries, and configurations

### Linking Standards
- Link to related pages rather than duplicating content. Duplication creates divergence.
- Use relative links within the wiki so URLs survive space moves.
- Link to external sources (vendor docs, CVE pages) with the access date noted in case the external content changes.
- Maintain a "start here" index page for each documentation area.

## Access Control

| Documentation Type | Access Level | Rationale |
|-------------------|-------------|-----------|
| Security policies | All employees | Policies apply to everyone |
| General security KB | All employees | Enables self-service |
| Runbooks | Security team + IT ops | Contains operational details |
| Architecture docs | Security team + engineering | Contains sensitive design details |
| Incident post-mortems | Security team + leadership | May contain sensitive details |
| Threat intel reports | Security team only | Contains IOCs and sensitive analysis |
| Pentest reports | Security team + asset owners | Contains exploitable vulnerability details |

## Versioning and Lifecycle

- **Draft**: Document in progress, not yet reviewed. Clearly labeled "DRAFT — NOT FOR OPERATIONAL USE."
- **Published**: Reviewed and approved by the owner. Ready for use.
- **Under Review**: Scheduled review in progress, may be updated. Note: "UNDER REVIEW — verify steps before relying on this document."
- **Deprecated**: Superseded by a newer document. Include a link to the replacement. Do not delete — archive for historical reference.
- **Archived**: No longer relevant. Moved to archive space, retained for institutional memory.

## Documentation Debt

Track documentation gaps as tickets in the team backlog:
- Missing runbooks for established procedures
- Runbooks that have not been verified in more than 90 days
- Architecture documents that do not reflect current state
- Knowledge base articles referenced in onboarding that do not exist

Review documentation debt quarterly. Allocate dedicated sprint capacity for documentation maintenance — it does not happen on its own.

## Cross-References

- See `voice/tone-profiles/technical-operator.md` for technical writing tone in runbooks
- See `voice/tone-profiles/compliance-auditor.md` for policy and audit documentation tone
- See `voice/channel-adaptation/ticketing-systems.md` for linking documentation to tickets
- See `voice/calibration/technical-depth-calibration.md` for audience-appropriate depth in documentation
