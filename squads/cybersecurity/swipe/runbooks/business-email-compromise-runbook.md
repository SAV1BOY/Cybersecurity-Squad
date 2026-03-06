# Business Email Compromise (BEC) Response Runbook

## Purpose

Step-by-step response procedures for business email compromise incidents, covering email analysis, account takeover assessment, financial fraud prevention, and evidence preservation.

## BEC Incident Types

| Type | Description | Urgency |
|------|-------------|---------|
| CEO/Executive Fraud | Impersonation of executive requesting wire transfer | Critical |
| Invoice Manipulation | Vendor email compromised, payment details changed | Critical |
| Account Takeover | Employee email account compromised and weaponized | High |
| Payroll Diversion | HR/payroll targeted to redirect employee pay | High |
| Data Theft | Compromised account used to exfiltrate data | High |
| Vendor Impersonation | External domain spoofing a known vendor | Medium |

## Phase 1: Detection and Triage (0-30 Minutes)

### Detection Sources

| Source | Indicator | Priority |
|--------|-----------|----------|
| User report | "I received a suspicious email from [executive/vendor]" | High |
| Email security | Forwarding rule creation, impossible travel | High |
| Financial team | Wire transfer request with unusual characteristics | Critical |
| DLP alert | Sensitive data sent to external address | High |
| Threat intelligence | Known BEC actor infrastructure match | Medium |
| Help desk | User reports inability to access email | Medium |

### Initial Triage Questions

1. Is there an active financial transaction in progress?
   - YES -> Immediately escalate to Phase 2a (Financial Containment)
   - NO -> Proceed to Phase 2b (Account Assessment)

2. Is an employee email account compromised?
   - YES -> Proceed to account containment
   - NO (external impersonation) -> Proceed to email analysis

3. How many accounts/users are affected?
4. What is the timeline of suspicious activity?
5. Has any sensitive data been accessed or sent?

## Phase 2a: Financial Containment (IMMEDIATE)

### If Wire Transfer Requested or Initiated

```
CRITICAL PATH -- TIME-SENSITIVE

1. Contact bank/financial institution IMMEDIATELY
   - Request wire recall/hold
   - Provide transaction details
   - Note reference numbers from bank

2. Contact receiving bank (if known)
   - Request hold on incoming funds
   - Provide fraud reference

3. Escalate to legal counsel
   - Potential regulatory reporting (SAR, law enforcement)
   - Evidence preservation requirements

4. Notify CFO/Treasury
   - Halt all pending payments from affected accounts
   - Implement manual verification for all wire transfers

5. File report with FBI IC3 (ic3.gov) or local law enforcement
   - Within 72 hours for best recovery chance
   - Include all transaction details
```

### Financial Recovery Timeline

| Time Since Transfer | Recovery Probability | Action |
|--------------------|--------------------|--------|
| < 24 hours | High (60-80%) | Bank recall, law enforcement |
| 24-72 hours | Medium (30-50%) | Bank recall, IC3 filing |
| 72 hours - 2 weeks | Low (10-20%) | Law enforcement, legal action |
| > 2 weeks | Very low (<5%) | Legal action, insurance claim |

## Phase 2b: Account Containment (First Hour)

### Immediate Actions

| Step | Action | Tool/Method |
|------|--------|-------------|
| 1 | Reset compromised account password | Azure AD / M365 Admin |
| 2 | Revoke all active sessions | `Revoke-AzureADUserAllRefreshToken` |
| 3 | Disable account temporarily (if needed) | Azure AD portal |
| 4 | Remove attacker's MFA device registrations | Azure AD MFA settings |
| 5 | Disable suspicious inbox rules | Exchange Admin / PowerShell |
| 6 | Remove email forwarding | Exchange Admin |
| 7 | Block identified malicious IPs | Conditional Access |
| 8 | Review and revoke OAuth app consents | Azure AD Enterprise Apps |

### PowerShell Commands for Exchange Online

```powershell
# Connect to Exchange Online
Connect-ExchangeOnline -UserPrincipalName admin@domain.com

# Check for inbox rules (forwarding, deletion)
Get-InboxRule -Mailbox compromised@domain.com |
  Where-Object {$_.ForwardTo -or $_.ForwardAsAttachmentTo -or
                $_.RedirectTo -or $_.DeleteMessage} |
  Select-Object Name, ForwardTo, RedirectTo, DeleteMessage

# Remove suspicious inbox rules
Remove-InboxRule -Mailbox compromised@domain.com -Identity "RuleName"

# Check for email forwarding
Get-Mailbox compromised@domain.com |
  Select-Object ForwardingAddress, ForwardingSmtpAddress, DeliverToMailboxAndForward

# Remove email forwarding
Set-Mailbox compromised@domain.com -ForwardingAddress $null -ForwardingSmtpAddress $null

# Check for delegate access
Get-MailboxPermission compromised@domain.com |
  Where-Object {$_.User -ne "NT AUTHORITY\SELF"}

# Check mail flow rules (transport rules)
Get-TransportRule | Where-Object {$_.State -eq "Enabled"} |
  Select-Object Name, Priority, SentTo, CopyTo, BlindCopyTo
```

## Phase 3: Investigation (Hours 1-24)

### Email Analysis

| Analysis Task | What to Look For | Tool |
|--------------|-----------------|------|
| Email headers | Originating IP, SPF/DKIM/DMARC results, reply-to manipulation | Header analyzer |
| Sending infrastructure | Domain registration date, hosting provider, reputation | WHOIS, VirusTotal |
| Content analysis | Urgency language, payment details, impersonation indicators | Manual review |
| Link analysis | Credential harvesting pages, malware delivery | URL sandbox |
| Attachment analysis | Malware, macro-enabled documents | Sandbox, VirusTotal |
| Conversation thread | Full thread to understand social engineering context | Exchange search |

### Account Activity Review

```
Review Period: 30 days before incident to present

1. Sign-in logs
   - Unusual locations or IPs
   - Sign-ins from VPN/TOR/proxy services
   - Failed MFA followed by successful bypass
   - Multiple device registrations

2. Email activity
   - Messages sent to external recipients (especially with attachments)
   - Bulk email access or download
   - Sent items and deleted items review
   - Search query history (if available)

3. File access
   - SharePoint/OneDrive file downloads
   - Unusual file sharing activity
   - Access to financial or HR documents

4. Administrative actions
   - Inbox rule creation/modification
   - Forwarding configuration changes
   - OAuth app consent grants
   - MFA method changes
```

### Scope Assessment

| Question | Investigation Method |
|----------|---------------------|
| How did the attacker gain access? | Sign-in logs, phishing email review |
| How long has the account been compromised? | Earliest anomalous sign-in |
| What emails did the attacker read? | Message trace, audit logs |
| What emails did the attacker send? | Sent items, message trace |
| Were other accounts targeted from this account? | Internal phishing review |
| Was data exfiltrated? | DLP logs, SharePoint access logs |
| Were forwarding rules used to maintain access? | Inbox rule audit |
| Were OAuth apps consented to? | Azure AD app consent audit |

## Phase 4: Evidence Preservation

### Evidence Collection Checklist

- [ ] Sign-in audit logs (export to CSV/JSON)
- [ ] Unified audit log for affected mailbox (90 days)
- [ ] Inbox rules (current and deleted)
- [ ] Email forwarding configuration
- [ ] Message trace logs (sent/received)
- [ ] Phishing email (original with full headers as .eml)
- [ ] OAuth app consent records
- [ ] MFA registration/change events
- [ ] Conditional Access policy evaluation logs
- [ ] Screenshots of attacker-created rules/forwarding
- [ ] Financial transaction records (if applicable)
- [ ] Communication records with bank/law enforcement

### Evidence Preservation Commands

```powershell
# Export unified audit log
Search-UnifiedAuditLog -StartDate "2026-02-01" -EndDate "2026-03-06" `
  -UserIds "compromised@domain.com" -ResultSize 5000 |
  Export-Csv -Path "C:\Evidence\audit_log.csv" -NoTypeInformation

# Export message trace
Get-MessageTrace -SenderAddress "compromised@domain.com" `
  -StartDate "2026-02-28" -EndDate "2026-03-06" |
  Export-Csv -Path "C:\Evidence\message_trace.csv" -NoTypeInformation
```

## Phase 5: Remediation and Recovery

### Account Recovery

1. Confirm all attacker persistence removed (rules, forwarding, OAuth, MFA)
2. Generate new password (strong, unique)
3. Re-enable account with new credentials
4. Re-enroll user in MFA (phishing-resistant preferred)
5. Brief user on what happened and what to watch for
6. Monitor account closely for 30 days

### Notification Requirements

| Stakeholder | When | Content |
|-------------|------|---------|
| Affected user | After containment | What happened, new credentials, monitoring |
| User's contacts | If impersonation occurred | Warning about fraudulent communications |
| Vendors/partners | If financial fraud attempted | Payment verification, updated contacts |
| Legal counsel | Immediately | Breach assessment, regulatory obligations |
| Insurance carrier | Within 24-48 hours | Claim notification if financial loss |
| Law enforcement | Within 72 hours | IC3 filing, local police report |
| Regulators | Per requirements | GDPR (72hr), state breach notification |

## Phase 6: Post-Incident Improvements

| Improvement Area | Action |
|-----------------|--------|
| Email security | Enable DMARC enforcement (p=reject) |
| Authentication | Deploy phishing-resistant MFA (FIDO2/WebAuthn) |
| Conditional Access | Implement trusted location/device policies |
| Awareness | BEC-specific training for finance and executive staff |
| Process | Implement out-of-band verification for wire transfers |
| Monitoring | Alert on inbox rule creation, forwarding changes, OAuth consents |
| Policy | Dual-authorization for payments above threshold |

## Cross-References

- [Incident Response Workflow](../../workflows/incident-response-workflow.md) -- overall IR process
- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity rating
- [KQL Hunting Queries](../detection/kql-hunting-queries.md) -- Sentinel queries for BEC
- [Insider Threat Runbook](insider-threat-runbook.md) -- if insider involvement suspected
