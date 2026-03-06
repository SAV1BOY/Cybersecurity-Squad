# Incident Recovery Checklist

## Purpose / When to Use

Execute this checklist after eradication is verified and signed off. Recovery restores affected systems to normal operations while maintaining heightened vigilance against re-compromise. The process must be phased, monitored, and validated -- rushing recovery is how organizations get compromised twice by the same adversary.

## Prerequisites

- [ ] Eradication verified and signed off (`eradication-checklist.md`)
- [ ] Clean backup images or rebuild media available for affected systems
- [ ] Monitoring enhancements deployed (new detection rules from incident analysis)
- [ ] Recovery priority list agreed upon with business stakeholders
- [ ] Change management process engaged for recovery activities
- [ ] Communication plan ready for user and customer notifications

---

## Phase 1 -- System Restoration Planning

- [ ] Prioritize system recovery order based on:
  - Business criticality (revenue impact, operational dependency)
  - Interdependencies (systems that must be online before others)
  - Risk level (systems with highest confidence of clean state first)
- [ ] For each system, determine restoration method:
  - **Rebuild from gold image**: highest confidence, use for critical/sensitive systems
  - **Restore from backup**: verify backup predates compromise, scan before restore
  - **Remediate in place**: lowest confidence, use only when rebuild is not feasible
- [ ] Validate backup integrity before restoration:
  ```bash
  # Verify backup hasn't been tampered with
  sha256sum backup_image.img  # compare against known hash
  # Mount read-only and scan
  mount -o ro,loop backup_image.img /mnt/verify
  clamscan -r /mnt/verify
  yara -r /opt/incident-rules/ioc.yar /mnt/verify
  ```
- [ ] Prepare hardened configurations incorporating lessons from incident:
  - Updated firewall rules
  - Tightened access controls
  - Additional monitoring agents
  - Patched vulnerabilities
- [ ] Define recovery success criteria for each system (functional tests, security checks)

## Phase 2 -- Phased System Restoration

### Tier 1 -- Identity and Authentication Infrastructure
- [ ] Restore/verify Active Directory domain controllers
- [ ] If AD was compromised: execute full AD recovery (forest recovery if necessary)
- [ ] Verify DNS integrity (no rogue records pointing to attacker infrastructure)
- [ ] Restore certificate authority services; reissue certificates if CA was at risk
- [ ] Validate MFA infrastructure is operational
- [ ] Confirm identity federation and SSO services are clean

### Tier 2 -- Core Infrastructure
- [ ] Restore network infrastructure (verify routing tables, ACLs, no rogue configurations)
- [ ] Restore email systems with enhanced filtering rules
- [ ] Restore file servers with verified clean data
- [ ] Restore database servers; verify data integrity
- [ ] Restore monitoring and logging infrastructure (SIEM, EDR management servers)

### Tier 3 -- Business Applications
- [ ] Restore application servers in dependency order
- [ ] Validate application functionality with pre-defined test cases
- [ ] Restore user workstations (rebuild from image preferred over remediation)
- [ ] Restore remote access systems with hardened configurations

### Tier 4 -- Non-Critical Systems
- [ ] Restore remaining systems based on business priority
- [ ] Decommission any systems identified as unnecessary during incident

## Phase 3 -- Service Validation

- [ ] For each restored system, execute validation checks:
  - [ ] Operating system boots and runs correctly
  - [ ] All security patches applied (confirm with vulnerability scan)
  - [ ] EDR agent installed, reporting, and policy-compliant
  - [ ] Sysmon or equivalent host logging configured and forwarding
  - [ ] Host firewall configured with appropriate rules
  - [ ] Anti-malware signatures current
  - [ ] IOC sweep returns clean (run full incident IOC set against restored system)
  - [ ] Application functionality tested and confirmed
  - [ ] User access restored with appropriate permissions (not excess)
- [ ] Verify backup jobs are running for restored systems
- [ ] Confirm monitoring dashboards show restored systems as healthy
- [ ] Run automated compliance scan to verify hardening standards
  ```bash
  # CIS Benchmark scan
  oscap xccdf eval --profile cis --results results.xml /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml
  ```

## Phase 4 -- Monitoring Enhancement

- [ ] Deploy incident-specific detection rules:
  - YARA rules for malware variants on all endpoints
  - Sigma/SIEM rules for behavioral patterns observed during incident
  - Network signatures for C2 protocol patterns
  - EDR watchlists for IOC file hashes and network indicators
- [ ] Increase logging verbosity on recovered systems for 30-day observation period:
  - Enable PowerShell script block logging and module logging
  - Enable process command-line auditing
  - Enable detailed authentication logging
  - Increase netflow/packet capture sampling rates on affected network segments
- [ ] Create dedicated SIEM dashboards for recovered systems:
  - Authentication attempts (especially failed)
  - New process execution (focus on rare processes)
  - Outbound network connections (especially to new destinations)
  - File modifications in sensitive directories
  - Scheduled task and service creation
- [ ] Assign SOC analysts to actively monitor recovered systems during observation period
- [ ] Set lower alert thresholds for recovered systems (higher sensitivity, accept more false positives temporarily)

## Phase 5 -- Phased Reconnection

- [ ] Reconnect systems to network in phases, not all at once:
  - Phase A: reconnect to internal network with enhanced monitoring (Day 1)
  - Phase B: enable outbound internet access through proxy (Day 2-3)
  - Phase C: restore full external access and user connectivity (Day 3-5)
- [ ] After each reconnection phase, observe for 24 hours minimum:
  - [ ] No C2 communication detected
  - [ ] No anomalous authentication patterns
  - [ ] No unexpected outbound connections
  - [ ] No signs of re-infection or residual compromise
- [ ] If anomalies detected during observation: immediately re-isolate and investigate
- [ ] Document reconnection timeline and observation results

## Phase 6 -- User Communication and Credential Reset

- [ ] Communicate recovery status to affected users:
  - What happened (appropriate level of detail per communication policy)
  - What actions were taken
  - What users need to do (password reset, MFA re-enrollment, device return)
  - How to report suspicious activity going forward
- [ ] Execute credential reset for all affected users:
  - [ ] Force password change at next login
  - [ ] Require MFA re-enrollment
  - [ ] Revoke and reissue access tokens
  - [ ] Reissue VPN certificates if applicable
- [ ] Provide updated security awareness guidance related to the attack vector
- [ ] Establish clear reporting channel for users who notice anything abnormal

## Phase 7 -- Recovery Closure

- [ ] All systems restored and validated against success criteria
- [ ] 30-day observation period completed with no signs of re-compromise
- [ ] Enhanced monitoring reduced to sustainable operational level
- [ ] All temporary firewall rules and containment measures removed or formalized
- [ ] Asset inventory updated to reflect any systems rebuilt, decommissioned, or added
- [ ] Recovery costs documented for financial reporting and insurance
- [ ] Formal sign-off from incident commander and business stakeholders
- [ ] Transition to post-incident review (`post-incident-checklist.md`)

---

## Cross-References

- Eradication: `checklists/incident-response/eradication-checklist.md`
- Post-incident review: `checklists/incident-response/post-incident-checklist.md`
- Hardening baselines: `checklists/santos/santos-hardening-baselines.md`
- Detection engineering: `checklists/detection-engineering-quality.md`
- Logging coverage: `checklists/blue-team/blueteam-logging-coverage.md`
- NIST SP 800-61r2: Section 3.3.4 -- Eradication and Recovery
