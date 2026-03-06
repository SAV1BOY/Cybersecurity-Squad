# Phishing Incident Response Runbook

## Purpose

Step-by-step operational runbook for responding to phishing incidents. Covers triage, containment, investigation, remediation, and lessons learned for SOC analysts and incident responders.

## Severity Classification

| Severity | Criteria | Response Time |
|----------|----------|--------------|
| Critical | Credentials confirmed compromised, data accessed | Immediate (within 15 min) |
| High | User clicked link AND entered credentials | Within 30 minutes |
| Medium | User clicked link but no credential entry | Within 2 hours |
| Low | User reported phishing, no interaction | Within 24 hours |
| Info | Phishing email blocked by gateway | No incident response needed |

---

## Phase 1: Detection and Triage (0-15 minutes)

### Step 1.1: Receive Report

- [ ] Record reporter name, email, timestamp
- [ ] Obtain original email (as attachment, not forwarded, to preserve headers)
- [ ] Ask reporter: "Did you click any links? Did you enter any information? Did you open any attachments?"

### Step 1.2: Analyze Email

```
Check the following:
1. Sender address (From header vs. envelope sender)
2. Reply-To address (different from From?)
3. SPF/DKIM/DMARC pass/fail (view email headers)
4. URLs in email body (hover/extract, DO NOT CLICK)
5. Attachment name, type, hash
6. Subject line and urgency indicators
7. Received headers (trace email path)
```

### Step 1.3: Classify Severity

Based on user interaction level (see table above), assign severity.

### Step 1.4: Check Scope

```
Determine how many users received the same email:
1. Search email gateway logs for sender address
2. Search for subject line across all mailboxes
3. Search for URLs/domains found in email
4. Count: total delivered, total opened, total clicked
```

---

## Phase 2: Containment (15-60 minutes)

### Step 2.1: Block Indicators

- [ ] Block sender email address/domain at email gateway
- [ ] Block phishing URL(s) at web proxy/DNS
- [ ] Block phishing domain at firewall
- [ ] Add URL/domain to threat intelligence blocklist
- [ ] If attachment: block file hash at endpoint protection

### Step 2.2: Remove Emails

- [ ] Purge phishing email from all mailboxes (Exchange: Compliance Search + Purge; Google: Admin investigation tool)
- [ ] Verify purge completion

### Step 2.3: If Credentials Were Entered

- [ ] Force password reset for affected user(s) IMMEDIATELY
- [ ] Revoke all active sessions (Azure AD: Revoke-AzureADUserAllRefreshToken; Google: Sign out all sessions)
- [ ] Revoke OAuth app consents granted by the user
- [ ] If MFA was not enabled: enable MFA before allowing re-authentication
- [ ] Check for mail forwarding rules added by attacker
- [ ] Check for OAuth apps authorized by compromised account
- [ ] Check for inbox rules (auto-forward, auto-delete)

### Step 2.4: If Attachment Was Opened

- [ ] Isolate affected endpoint via EDR
- [ ] Collect forensic image if malware confirmed
- [ ] Run full endpoint scan
- [ ] Check for persistence mechanisms
- [ ] Check for lateral movement indicators

---

## Phase 3: Investigation (1-24 hours)

### Step 3.1: Email Analysis

```
1. Extract all URLs from email body and headers
2. Check URLs against threat intel (VirusTotal, URLhaus)
3. Submit attachment to sandbox (Any.Run, Joe Sandbox, Cuckoo)
4. Analyze email headers for originating infrastructure
5. Check domain registration (whois) for phishing domain
6. Identify if this is part of a known campaign
```

### Step 3.2: Compromised Account Investigation

```
For each user who entered credentials:
1. Review sign-in logs (past 72 hours minimum)
   - New IP addresses
   - New locations
   - New devices
   - Failed MFA attempts (MFA fatigue)
2. Review mailbox activity
   - Emails sent (attacker replies to existing threads)
   - Forwarding rules added
   - OAuth consents granted
   - Contacts exported
3. Review file access
   - SharePoint/OneDrive/Google Drive access
   - Files downloaded or shared externally
4. Review admin actions (if admin account compromised)
```

### Step 3.3: Lateral Impact Assessment

```
1. Did the compromised account send internal phishing to others?
2. Were any shared resources accessed (shared mailboxes, team drives)?
3. Was the account used to access other systems (SSO)?
4. Were any password resets performed by the compromised account?
```

### Step 3.4: Document Timeline

```
[YYYY-MM-DD HH:MM] - Phishing email delivered to [N] users
[YYYY-MM-DD HH:MM] - User [X] clicked link
[YYYY-MM-DD HH:MM] - User [X] entered credentials
[YYYY-MM-DD HH:MM] - Attacker logged in from [IP/location]
[YYYY-MM-DD HH:MM] - Attacker performed [action]
[YYYY-MM-DD HH:MM] - Incident reported by [reporter]
[YYYY-MM-DD HH:MM] - Containment actions initiated
```

---

## Phase 4: Remediation (1-7 days)

### Step 4.1: Verify Containment

- [ ] Confirm all phishing emails purged
- [ ] Confirm all IOCs blocked
- [ ] Confirm affected accounts secured
- [ ] Confirm no persistence mechanisms remain

### Step 4.2: Restore Access

- [ ] Allow affected users to re-authenticate (with new password + MFA)
- [ ] Verify no unauthorized changes persist in accounts
- [ ] Re-enable any temporarily disabled services

### Step 4.3: Update Defenses

- [ ] Add new IOCs to threat intelligence platform
- [ ] Update email gateway rules based on observed patterns
- [ ] Review and improve detection rules (did SIEM detect this?)
- [ ] Consider phishing simulation targeting the same technique

---

## Phase 5: Post-Incident (Within 7 days)

### Step 5.1: Metrics

| Metric | Value |
|--------|-------|
| Time from delivery to report | [X hours] |
| Time from report to containment | [X minutes] |
| Total users who received email | [N] |
| Total users who clicked | [N] |
| Total users who entered credentials | [N] |
| Total users who reported | [N] |
| Business impact | [Description] |

### Step 5.2: Lessons Learned

- [ ] What worked well in the response?
- [ ] What could be improved?
- [ ] Were detection and blocking rules adequate?
- [ ] Does user awareness training need updating?
- [ ] Are there process improvements to implement?

### Step 5.3: Report

Create incident report using the incident template and share with stakeholders.

---

## Cross-References

- See `reference/psychology/social-engineering-psychology.md` for phishing psychology
- See `frameworks/nist-800-61-incident-response.md` for IR framework
- See `workflows/incident-response-workflow.md` for general IR workflow
- See `templates/communications/breach-notification-template.md` if PII accessed
- See `data/registries/incident-registry.md` for incident tracking
