# Incident Containment Checklist

## Purpose / When to Use

Execute this checklist after initial triage confirms a security incident requiring active containment. Containment limits attacker access, stops lateral movement, prevents data exfiltration, and preserves evidence. The goal is to box the adversary in without alerting them prematurely (when possible) and without causing unnecessary business disruption.

## Prerequisites

- [ ] Initial triage completed (`initial-triage-checklist.md`) with severity assigned
- [ ] Incident commander designated and communication channels established
- [ ] Known IOCs documented: compromised accounts, malicious IPs/domains, malware hashes, affected systems
- [ ] Access to: EDR console, firewall management, DNS administration, Active Directory, cloud console
- [ ] Legal team consulted on evidence preservation requirements
- [ ] Business stakeholders aware that service disruption may occur

---

## Phase 1 -- Network Isolation

- [ ] Implement tiered network isolation based on threat severity:
  - **Tier 1 -- Full isolation**: Move affected systems to quarantine VLAN with no internet or lateral access
  - **Tier 2 -- Selective blocking**: Block specific C2 IPs/domains at perimeter; allow internal access for monitoring
  - **Tier 3 -- Monitoring only**: No network changes; observe attacker activity for intelligence gathering
- [ ] Block confirmed C2 infrastructure at all egress points:
  ```bash
  # Firewall: deny outbound to C2 IPs
  # DNS: sinkhole C2 domains to internal honeypot
  # Proxy: block C2 URLs and patterns; add SSL inspection if not present
  ```
- [ ] Implement emergency firewall rules to restrict lateral movement from affected subnets:
  ```
  Deny: affected_subnet -> any : SMB (445), RDP (3389), WinRM (5985/5986), SSH (22)
  Allow: affected_subnet -> SIEM_collector : syslog (514), agent ports
  ```
- [ ] Disable switch ports for systems requiring physical isolation (coordinate with network team)
- [ ] If VPN is compromised: revoke VPN certificates/tokens, force re-authentication
- [ ] Review and tighten inter-VLAN routing rules to limit blast radius
- [ ] Document all network changes with rollback procedures

## Phase 2 -- Account Lockout and Credential Containment

- [ ] Disable all confirmed compromised accounts immediately
  ```powershell
  # Active Directory
  Disable-ADAccount -Identity compromised_user
  Set-ADUser -Identity compromised_user -Description "DISABLED - Incident IR-2024-XXX"
  ```
- [ ] Force password reset for accounts with confirmed credential exposure
- [ ] Revoke active sessions and tokens for compromised accounts:
  - Azure AD: `Revoke-AzureADUserAllRefreshToken`
  - AWS: deactivate IAM access keys, invalidate console sessions
  - OAuth: revoke all granted tokens
- [ ] If privileged account compromised:
  - [ ] Reset the account password from a clean, isolated admin workstation
  - [ ] Review all actions performed by the account during compromise window
  - [ ] Reset passwords of any accounts the compromised privileged account could access
  - [ ] If domain admin compromised: initiate KRBTGT reset procedure (double reset, 12-hour gap)
- [ ] Disable service accounts associated with compromised systems
- [ ] Enforce MFA re-enrollment for all affected users
- [ ] Review and revoke API keys, SSH keys, and certificates associated with compromised identities
- [ ] Monitor authentication logs for attempts to use disabled/reset credentials (attacker awareness indicator)

## Phase 3 -- Endpoint Quarantine

- [ ] Isolate confirmed compromised endpoints via EDR network containment
  ```
  CrowdStrike: Contain host via Falcon console
  Defender: Isolate device via MDE portal
  SentinelOne: Network quarantine via console
  ```
- [ ] Verify isolation is effective: confirm no outbound connections from isolated endpoints
- [ ] For endpoints without EDR: use host firewall rules or physical disconnection
  ```powershell
  # Windows Firewall emergency lockdown
  netsh advfirewall set allprofiles firewallpolicy blockinbound,blockoutbound
  netsh advfirewall firewall add rule name="IR-Allow-SIEM" dir=out action=allow remoteip=SIEM_IP
  ```
- [ ] Collect volatile evidence from isolated endpoints before any remediation
- [ ] Disable auto-remediation in EDR to preserve evidence (quarantine, don't delete)
- [ ] Tag affected endpoints in asset management system with incident ID
- [ ] For mobile devices: initiate remote wipe or selective wipe if corporate data at risk

## Phase 4 -- Cloud Resource Isolation

- [ ] Revoke compromised cloud credentials and access keys
- [ ] Isolate affected cloud workloads:
  ```bash
  # AWS: Modify security group to deny all traffic
  aws ec2 modify-instance-attribute --instance-id i-xxx --groups sg-quarantine
  # Azure: Apply NSG blocking all traffic
  az network nsg rule create --name quarantine --nsg-name affected-nsg \
    --priority 100 --access Deny --direction Inbound --source-address-prefixes '*'
  # GCP: Apply firewall rule
  gcloud compute firewall-rules create quarantine-ir --action=DENY --rules=all --target-tags=compromised
  ```
- [ ] Disable or restrict IAM roles/policies associated with compromised workloads
- [ ] Check for and disable any new IAM users, roles, or access keys created by attacker
- [ ] Review cloud trail/activity logs for unauthorized resource creation (new instances, Lambda functions, S3 buckets)
- [ ] Suspend or delete attacker-created resources after evidence collection
- [ ] Check for data exfiltration via cloud storage (S3 bucket policies, blob access logs)
- [ ] Review and restrict cross-account access if lateral movement to other cloud accounts is possible

## Phase 5 -- Communication Lockdown

- [ ] If email system is compromised:
  - [ ] Block attacker-controlled mailbox rules (forwarding, auto-delete)
  - [ ] Disable compromised email accounts
  - [ ] Review and revoke OAuth app permissions granted via phishing
  - [ ] Search for and remove phishing emails still in user mailboxes
    ```powershell
    # Exchange Online: Content search and purge
    New-ComplianceSearch -Name "IR-Phish-Purge" -ExchangeLocation all -ContentMatchQuery 'subject:"phish subject" AND received>=2024-01-15'
    ```
- [ ] Establish out-of-band communication for incident response team:
  - Dedicated Signal group or phone bridge
  - Avoid corporate Slack/Teams if identity provider or endpoint is compromised
- [ ] Restrict information about incident to need-to-know basis
- [ ] If internal threat: ensure the suspected individual has no visibility into response activities
- [ ] Prepare external communication templates (customer notification, regulatory, press) but do not release without legal approval

## Phase 6 -- Containment Verification

- [ ] Verify all containment actions are effective:
  - [ ] Confirm isolated endpoints have no network connectivity to production
  - [ ] Confirm C2 domains/IPs are blocked at all egress points (test resolution and connectivity)
  - [ ] Confirm compromised accounts cannot authenticate
  - [ ] Confirm cloud resources are isolated
- [ ] Monitor for attacker adaptation:
  - New C2 channels activating (different domains, IPs, protocols)
  - New accounts being created or existing accounts being compromised
  - Attempts to remove monitoring tools or disable logging
  - Lateral movement to previously unaffected systems
- [ ] If attacker evades containment: expand containment scope and reassess severity
- [ ] Document containment effectiveness assessment
- [ ] Confirm with incident commander that containment is sufficient to proceed to eradication

---

## Cross-References

- Initial triage: `checklists/incident-response/initial-triage-checklist.md`
- Eradication: `checklists/incident-response/eradication-checklist.md`
- Recovery: `checklists/incident-response/recovery-checklist.md`
- Malware response: `checklists/malware/malware-response-checklist.md`
- Evidence integrity: `checklists/sanders/sanders-evidence-integrity.md`
- Cloud security: `checklists/cloud/cloud-iam-least-privilege.md`
- NIST SP 800-61r2: Section 3.3 -- Containment, Eradication, and Recovery
