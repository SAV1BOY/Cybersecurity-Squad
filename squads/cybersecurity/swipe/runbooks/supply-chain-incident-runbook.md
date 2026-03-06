# Supply Chain Incident Response Runbook

## Purpose

Response procedures for supply chain compromise incidents covering vendor communication, impact assessment, containment strategies, and recovery planning. Addresses software supply chain, managed service provider, and hardware supply chain scenarios.

## Supply Chain Incident Types

| Type | Description | Examples | Severity |
|------|-------------|----------|----------|
| Software supply chain | Compromised software update or dependency | SolarWinds, Codecov, ua-parser-js | Critical |
| MSP/MSSP compromise | Managed service provider access exploited | Kaseya, ConnectWise exploitation | Critical |
| Cloud service compromise | SaaS/PaaS/IaaS service breached | Okta, LastPass, Snowflake | Critical |
| Hardware/firmware | Tampered hardware or firmware | Pre-installed malware, implants | Critical |
| Open-source dependency | Malicious package injection | npm, PyPI, RubyGems | High |
| Certificate/signing | Compromised code signing certificate | Stolen signing keys | Critical |
| Data sharing partner | Partner with access to shared data breached | Customer data exposure | High |

## Phase 1: Initial Assessment (First 2 Hours)

### Detection Triggers

| Trigger | Source | Response |
|---------|--------|----------|
| Vendor notification | Email, portal, direct communication | Validate authenticity, assess impact |
| Threat intelligence | ISAC, CERT, media reports | Identify if vendor/product is in use |
| Internal detection | EDR, SIEM, anomaly detection | Investigate, determine if supply chain related |
| Government advisory | CISA, FBI, NSA | Immediate assessment of exposure |
| Customer report | Customer identifies issue traced to your vendor | Investigate and coordinate |

### Rapid Impact Assessment

```
1. Asset Identification
   - Do we use the affected vendor/product/service?
   - What version/configuration is deployed?
   - Where is it deployed (production, staging, dev)?
   - How many instances/installations?
   - What access does this vendor/product have?

2. Exposure Window
   - When was the compromise introduced?
   - When did we deploy the affected version?
   - How long have we been exposed?
   - Was the compromised component actively used?

3. Access Scope
   - What data can the compromised component access?
   - What network segments can it reach?
   - What credentials does it have?
   - What APIs/services does it call?

4. Initial Risk Rating
   - Confirmed compromise of our environment? -> SEV-1
   - Possible compromise, investigating? -> SEV-2
   - Vendor compromised, no evidence of our impact? -> SEV-3
```

### Rapid Assessment Checklist

- [ ] Confirm vendor/product is in use (CMDB, procurement records)
- [ ] Identify affected version(s) and deployment locations
- [ ] Check vendor advisory for IOCs
- [ ] Sweep environment for provided IOCs
- [ ] Assess network connectivity of affected systems
- [ ] Identify data classification of accessible data
- [ ] Determine if auto-update is enabled
- [ ] Check if affected product has privileged access

## Phase 2: Vendor Communication

### Vendor Contact Protocol

| Priority | Action | Timeline |
|----------|--------|----------|
| 1 | Identify vendor security contact (not just sales) | Immediate |
| 2 | Request formal incident notification with IOCs | Immediate |
| 3 | Request scope and timeline of compromise | Within 4 hours |
| 4 | Request recommended remediation steps | Within 4 hours |
| 5 | Obtain clean/verified version for replacement | Within 24 hours |
| 6 | Request ongoing updates at defined cadence | Continuous |

### Questions for Vendor

```
1. Scope and Timeline:
   - What was compromised (product, service, infrastructure)?
   - When did the compromise begin?
   - When was it discovered?
   - What versions/instances are affected?
   - Is the compromise contained?

2. Technical Details:
   - What are the IOCs (hashes, IPs, domains, behavioral)?
   - What access did the attacker gain?
   - Was customer data accessed?
   - Was the attacker able to push updates/changes to customers?
   - Were signing keys compromised?

3. Remediation:
   - What version/patch resolves the issue?
   - Can we verify the integrity of the fix?
   - Are there interim mitigation steps?
   - What logs should we review for evidence of exploitation?

4. Ongoing:
   - What is the update cadence for this incident?
   - Who is our dedicated contact?
   - What third parties are involved (forensics, law enforcement)?
   - What regulatory notifications are planned?
```

### Vendor Response Evaluation

| Response Quality | Indicators | Our Action |
|-----------------|-----------|-----------|
| Strong | Rapid notification, detailed IOCs, clear timeline, remediation steps | Follow guidance, verify independently |
| Adequate | Notification with some IOCs, general timeline | Follow guidance, supplement with own investigation |
| Weak | Vague notification, no IOCs, unclear timeline | Aggressive independent investigation, consider isolation |
| Non-responsive | No communication despite outreach | Assume worst case, isolate, engage alternatives |

## Phase 3: Containment

### Containment Decision Matrix

| Scenario | Action | Justification |
|----------|--------|---------------|
| Confirmed compromise, active exploitation | Isolate immediately | Stop active threat |
| Confirmed vendor compromise, no evidence of our impact | Monitor + restrict | Precautionary while investigating |
| Possible compromise, vendor investigating | Enhanced monitoring | Balanced approach |
| Software dependency compromise | Block updates, scan existing | Prevent further exposure |

### Software Supply Chain Containment

```
1. Block auto-updates for affected product
   - Firewall rules to block update servers
   - Disable auto-update configuration
   - Block DNS resolution for update domains

2. Isolate affected systems (if confirmed compromise)
   - Network isolation via firewall rules
   - EDR containment (host isolation)
   - Disable service accounts used by the product

3. Scan for IOCs across all instances
   - Deploy YARA rules for known malicious payloads
   - Search for C2 communication in network logs
   - Check for persistence mechanisms
   - Review process execution logs

4. Verify software integrity
   - Compare file hashes against known-good versions
   - Check code signing certificate validity
   - Verify package checksums against vendor-provided values
   - Scan for unauthorized modifications
```

### MSP Compromise Containment

```
1. Revoke MSP access credentials immediately
   - Disable MSP VPN accounts
   - Revoke API tokens and access keys
   - Change shared passwords
   - Remove MSP admin accounts from systems

2. Review MSP activity logs
   - Last 90 days of MSP access
   - Systems accessed by MSP accounts
   - Changes made by MSP accounts
   - Data accessed or exported

3. Assess tools deployed by MSP
   - Remote management agents (RMM)
   - Monitoring agents
   - Any software pushed via MSP tools

4. Secure the management plane
   - Change all credentials that MSP knew
   - Review and reset firewall rules added by MSP
   - Audit DNS records managed by MSP
```

## Phase 4: Investigation

### Investigation Scope

| Area | Investigation Actions |
|------|---------------------|
| Network | Review firewall logs for C2 traffic, unusual outbound connections from affected systems |
| Endpoint | EDR investigation of affected hosts, process trees, file modifications |
| Identity | Review authentication from affected service accounts, privilege usage |
| Data | DLP review for data exfiltration, access to sensitive data stores |
| Cloud | API call audit for affected service integrations |
| Email | Review for phishing or BEC leveraging vendor relationship |

### Software Bill of Materials (SBOM) Analysis

| Check | Purpose | Tool/Method |
|-------|---------|-------------|
| Dependency tree | Identify all dependencies that include compromised component | SBOM tools (Syft, CycloneDX) |
| Transitive dependencies | Find indirect usage of compromised package | Dependency graph analysis |
| Version mapping | Which specific versions are deployed | Package manager audit |
| Build pipeline | Was compromised component used in builds | CI/CD pipeline audit |
| Artifact integrity | Verify build artifacts are untampered | Hash comparison, reproducible builds |

## Phase 5: Recovery

### Recovery Priority

| Priority | Action | Timeline |
|----------|--------|----------|
| 1 | Deploy clean/patched version of affected software | ASAP |
| 2 | Rotate all credentials accessible to compromised component | 24 hours |
| 3 | Rebuild systems if compromise confirmed | 48-72 hours |
| 4 | Re-establish vendor access with enhanced controls | After vendor remediation |
| 5 | Conduct thorough post-compromise audit | 1-2 weeks |

### Vendor Re-Engagement Criteria

```
Before restoring vendor access:
[ ] Vendor has completed forensic investigation
[ ] Root cause identified and remediated
[ ] Vendor provides written attestation of remediation
[ ] Enhanced monitoring in place for vendor access
[ ] Credentials rotated and new credentials provisioned
[ ] Access scope reviewed and minimized
[ ] SLA/contract updated with security requirements
[ ] Incident notification obligations formalized
```

## Phase 6: Post-Incident Improvements

### Third-Party Risk Improvements

| Area | Improvement |
|------|------------|
| Vendor assessment | Add supply chain security questions to vendor risk assessment |
| Monitoring | Implement continuous monitoring of critical vendor security posture |
| Contractual | Add incident notification SLAs, right-to-audit, security requirements |
| Technical | Implement software composition analysis (SCA) in CI/CD pipeline |
| Architecture | Apply zero trust to vendor integrations (least privilege, monitoring) |
| SBOM | Require and maintain SBOMs for all critical software |
| Detection | Develop detection rules for vendor-specific compromise indicators |
| Recovery | Update DR plans to include vendor compromise scenarios |

## Cross-References

- [Incident Response Workflow](../../workflows/incident-response-workflow.md) -- overall IR process
- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity rating
- [Zero-Day Response Runbook](zero-day-response-runbook.md) -- if supply chain delivers zero-day
- [Cloud Compromise Runbook](cloud-compromise-runbook.md) -- if cloud service is the supply chain vector
