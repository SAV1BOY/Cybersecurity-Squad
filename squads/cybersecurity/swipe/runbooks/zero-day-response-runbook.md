# Zero-Day Vulnerability Response Runbook

## Purpose

Response procedures for zero-day vulnerability disclosures when no patch is available. Covers rapid assessment, compensating controls deployment, monitoring enhancement, and patching timeline management.

## Zero-Day Response Triggers

| Trigger | Source | Example |
|---------|--------|---------|
| Vendor advisory (no patch) | Vendor security bulletin | Microsoft out-of-band advisory |
| CISA/CERT alert | Government advisory | CISA Known Exploited Vulnerabilities (KEV) |
| Threat intelligence | Intel feeds, ISACs | Active exploitation reported in the wild |
| Security researcher disclosure | Blog post, conference, social media | Proof-of-concept published |
| Internal discovery | Penetration test, red team, bug bounty | Discovered during assessment |
| Incident investigation | During IR, root cause is zero-day | Forensic analysis reveals unknown vuln |

## Phase 1: Rapid Assessment (First 2 Hours)

### Vulnerability Classification

| Factor | Assessment | Impact on Response |
|--------|-----------|-------------------|
| CVSS Score | 0-10 | Sets baseline severity |
| Active exploitation | Yes/No | Yes = immediate escalation |
| Public PoC available | Yes/No | Yes = faster weaponization expected |
| Remote exploitable | Yes/No | Yes = higher urgency |
| Authentication required | Yes/No | No = wider attack surface |
| User interaction required | Yes/No | No = higher urgency |
| Affected product in our environment | Yes/No/Unknown | Determines if action needed |
| Internet-facing exposure | Yes/No | Yes = highest priority |

### Exposure Assessment Checklist

```
1. Product/Component Inventory
   [ ] Identify all instances of affected product/component
   [ ] Map versions deployed across environment
   [ ] Distinguish internet-facing vs. internal-only
   [ ] Identify data classification of affected systems
   [ ] Document business criticality of affected systems

2. Attack Surface Analysis
   [ ] Is the vulnerable component reachable from untrusted networks?
   [ ] What ports/protocols expose the vulnerability?
   [ ] Are there existing controls that may mitigate (WAF, IPS, EDR)?
   [ ] What authentication is required to reach the vulnerable component?
   [ ] Can the vulnerability be chained with other known issues?

3. Exploitation Assessment
   [ ] Is the vulnerability being actively exploited in the wild?
   [ ] Is a public proof-of-concept available?
   [ ] What is the likely attacker profile (nation-state, commodity)?
   [ ] What is the exploitation difficulty (trivial, moderate, complex)?
   [ ] What MITRE ATT&CK techniques does exploitation enable?
```

### Severity Rating

| Severity | Criteria | Response Timeline |
|----------|---------|-------------------|
| Emergency | Active exploitation + internet-facing + no auth required | Compensating controls within 4 hours |
| Critical | Active exploitation + internal exposure | Compensating controls within 24 hours |
| High | PoC available + internet-facing | Compensating controls within 48 hours |
| Medium | PoC available + internal only | Compensating controls within 1 week |
| Low | No PoC + internal only + auth required | Monitor, plan for patch |

## Phase 2: Compensating Controls (Hours 2-24)

### Control Selection Matrix

| Compensating Control | Speed to Deploy | Effectiveness | Side Effects |
|---------------------|----------------|---------------|-------------|
| WAF rule | Hours | Moderate (can be bypassed) | Possible false positives |
| IPS/IDS signature | Hours | Moderate | Performance impact |
| Network ACL/firewall | Minutes | High (if network-based) | Service disruption risk |
| Disable affected feature | Minutes-Hours | High | Functionality loss |
| Application configuration | Hours | Variable | Functionality impact |
| EDR custom rule | Hours | Moderate-High | Agent required |
| Proxy/reverse proxy filter | Hours | Moderate | Latency |
| Microsegmentation | Hours-Days | High | Complexity |

### Compensating Control Deployment

```
Priority Order:

1. NETWORK-LEVEL CONTROLS (fastest, broadest)
   [ ] Block external access to vulnerable service (if possible)
   [ ] Restrict source IPs to trusted ranges
   [ ] Apply geo-blocking if applicable
   [ ] Enable enhanced firewall logging

2. APPLICATION-LEVEL CONTROLS (targeted)
   [ ] Deploy WAF rules (vendor-provided or custom)
   [ ] Disable vulnerable feature/endpoint
   [ ] Apply configuration workaround (per vendor advisory)
   [ ] Restrict authentication to specific methods
   [ ] Enable additional input validation

3. HOST-LEVEL CONTROLS (defense in depth)
   [ ] Deploy EDR custom detection rule
   [ ] Enable enhanced audit logging
   [ ] Apply filesystem/registry restrictions
   [ ] Harden service account permissions
   [ ] Enable exploit protection features (ASLR, DEP, CFG)

4. MONITORING CONTROLS (detection)
   [ ] Deploy IOC-based detection rules
   [ ] Enable verbose logging on affected services
   [ ] Deploy YARA rules for known exploit artifacts
   [ ] Configure alerts for exploitation indicators
   [ ] Implement canary files/tokens near vulnerable services
```

### Vendor-Specific Workaround Examples

| Scenario | Workaround Pattern |
|----------|-------------------|
| Web application vulnerability | Disable affected URL path at reverse proxy |
| Authentication bypass | Add additional authentication layer (MFA, proxy auth) |
| RCE in service | Restrict network access + disable unused features |
| Privilege escalation | Reduce service account privileges, enable audit |
| Information disclosure | Add response filtering at WAF/proxy |
| SSRF | Block outbound connections from service, allowlist URLs |
| Deserialization | Disable affected serialization format, enable type filtering |

## Phase 3: Monitoring Enhancement (Hours 4-48)

### Detection Rules to Deploy

| Detection Target | Detection Method | Tool |
|-----------------|-----------------|------|
| Exploitation attempt | Network signature (Snort/Suricata) | IDS/IPS |
| Exploitation attempt | WAF custom rule with logging | WAF |
| Post-exploitation behavior | Host-based behavioral detection | EDR |
| Known IOCs | IOC sweep and continuous monitoring | SIEM |
| Lateral movement from affected host | Network anomaly detection | NDR |
| Data exfiltration from affected host | DLP + network monitoring | DLP/NDR |
| Privilege escalation on affected host | Process and authentication monitoring | SIEM/EDR |

### Hunting Queries

```
Deploy targeted hunting queries for:
1. Anomalous process execution on affected hosts
2. Unusual network connections from affected services
3. Unexpected file modifications in service directories
4. Authentication anomalies from service accounts
5. New scheduled tasks or services on affected hosts
6. Unusual parent-child process relationships
7. Exploitation artifacts (webshells, implants, tools)
```

### Monitoring Dashboard

| Metric | Source | Alert Threshold |
|--------|--------|----------------|
| Exploitation attempts (blocked) | WAF/IPS | Any detection = alert |
| Exploitation attempts (allowed) | WAF/IPS/EDR | Any detection = critical alert |
| Affected service errors | Application logs | Spike > 2x baseline |
| Network connections from affected hosts | Firewall logs | New external destinations |
| Process creation on affected hosts | EDR | Unexpected processes |
| Compensating control health | All controls | Any control failure = alert |

## Phase 4: Patch Management

### Patching Timeline

| Activity | Timeline | Owner |
|----------|----------|-------|
| Monitor vendor for patch release | Continuous | Vulnerability team |
| Evaluate patch (testing) | Within 24 hours of release | IT + Security |
| Deploy to test environment | Within 24 hours of evaluation | IT Ops |
| Validate fix and no regression | Within 48 hours of test deploy | QA + Security |
| Deploy to production (critical) | Within 24-72 hours of validation | IT Ops |
| Deploy to production (all) | Within 7 days | IT Ops |
| Verify patch effectiveness | Within 24 hours of production deploy | Security |
| Remove compensating controls | After verification | Security + IT |

### Patch Validation Checklist

```
Before deploying patch:
[ ] Verify patch is from legitimate vendor source
[ ] Validate digital signature on patch
[ ] Test in non-production environment
[ ] Verify vulnerability is remediated (re-test)
[ ] Confirm no functionality regression
[ ] Document rollback procedure
[ ] Schedule maintenance window (if required)

After deploying patch:
[ ] Verify patch applied successfully on all targets
[ ] Re-scan for vulnerability confirmation
[ ] Test affected service functionality
[ ] Monitor for stability issues
[ ] Plan compensating control removal
[ ] Update vulnerability management system
[ ] Close associated tickets
```

## Phase 5: Communication

### Stakeholder Communication

| Stakeholder | When | Content | Method |
|-------------|------|---------|--------|
| CISO/Security leadership | Upon discovery | Exposure assessment, response plan | Direct briefing |
| IT leadership | Within 2 hours | Affected systems, compensating controls | Email + meeting |
| Executive team | Within 4 hours (if critical) | Business impact, response status | Executive briefing |
| Affected system owners | Within 4 hours | Specific actions required from them | Email + ticket |
| SOC/IR team | Immediately | Detection rules, monitoring guidance | Chat + wiki |
| Vendor management | Within 24 hours | Vendor expectations, escalation | Email + call |
| Customers (if applicable) | Per contractual/regulatory obligations | Impact assessment, actions taken | Formal notification |

### Status Update Template

```
ZERO-DAY RESPONSE STATUS UPDATE

Vulnerability: [CVE/Name]
Status: [Assessing / Mitigating / Monitoring / Patching / Resolved]
Update Time: [Timestamp]

Exposure:
- Affected systems: [count] instances across [environments]
- Internet-facing: [Yes/No] ([count] instances)
- Active exploitation detected: [Yes/No]

Compensating Controls:
- [Control 1]: [Deployed/Pending] - [Status]
- [Control 2]: [Deployed/Pending] - [Status]

Patch Status:
- Vendor patch: [Available/Not yet released/ETA]
- Testing: [Not started/In progress/Complete]
- Production deployment: [Scheduled/In progress/Complete]

Next Update: [Timestamp]
```

## Cross-References

- [Vulnerability Management Lifecycle](../../frameworks/vulnerability-management-lifecycle.md) -- vuln management process
- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity framework
- [Supply Chain Incident Runbook](supply-chain-incident-runbook.md) -- if zero-day is supply chain delivered
- [Sigma Rule Examples](../detection/sigma-rule-examples.md) -- detection rule development
- [Snort/Suricata Rules](../detection/snort-suricata-rules.md) -- network detection rules
