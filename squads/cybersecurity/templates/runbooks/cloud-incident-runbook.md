# Cloud-Specific Incident Response Runbook

## Purpose

Step-by-step operational runbook for responding to security incidents in cloud environments (AWS, Azure, GCP). Covers cloud-specific containment, evidence preservation, investigation techniques, and recovery procedures.

## Cloud IR Differences from Traditional IR

| Aspect | Traditional | Cloud |
|--------|-------------|-------|
| Evidence collection | Disk imaging, memory dump | API logs, cloud trails, snapshots |
| Containment | Network isolation, pull cables | Security groups, IAM policy, resource tagging |
| Forensics | Physical media analysis | Log analysis, snapshot mounting, serverless traces |
| Jurisdiction | Physical location known | Multi-region, data residency questions |
| Shared responsibility | Full control | Provider controls some layers |
| Scale | Known asset count | Dynamic, auto-scaling, ephemeral |

---

## Phase 1: Detection and Triage (0-30 Minutes)

### Step 1.1: Identify Incident Type

| Indicator | Likely Incident | Priority |
|-----------|----------------|----------|
| GuardDuty/Defender alert: credential exfiltration | Compromised credentials | Critical |
| Unusual API calls (CreateUser, AttachPolicy) | IAM compromise | Critical |
| S3/Blob public access alert | Data exposure | Critical |
| Cryptomining detection | Resource hijacking | High |
| Unauthorized data access (CloudTrail) | Data breach | Critical |
| Cost anomaly alert | Resource abuse | Medium-High |
| VPC flow log: unusual outbound | Data exfiltration | High |

### Step 1.2: Determine Scope

```
Questions to answer:
1. Which account(s) / subscription(s) are affected?
2. Which region(s)?
3. What resources are compromised (instances, functions, storage)?
4. What IAM principals are involved?
5. When did the activity begin (CloudTrail/Activity Log)?
6. Is the activity ongoing?
```

---

## Phase 2: Containment (30-120 Minutes)

### AWS Containment Actions

```bash
# Disable compromised IAM user
aws iam update-login-profile --user-name COMPROMISED_USER --no-password-reset-required
aws iam delete-login-profile --user-name COMPROMISED_USER

# Deactivate access keys
aws iam update-access-key --user-name COMPROMISED_USER --access-key-id AKIAXXXXXXXX --status Inactive

# Revoke all sessions for IAM role (add inline deny policy)
aws iam put-role-policy --role-name COMPROMISED_ROLE --policy-name DenyAll --policy-document '{
  "Version": "2012-10-17",
  "Statement": [{"Effect": "Deny", "Action": "*", "Resource": "*",
    "Condition": {"DateLessThan": {"aws:TokenIssueTime": "CURRENT_TIMESTAMP"}}}]
}'

# Isolate EC2 instance (replace security group with no-ingress/no-egress)
aws ec2 create-security-group --group-name forensic-isolation --description "Isolation SG" --vpc-id vpc-xxx
aws ec2 modify-instance-attribute --instance-id i-xxx --groups sg-forensic-isolation

# Block S3 bucket public access
aws s3api put-public-access-block --bucket BUCKET_NAME \
  --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
```

### Azure Containment Actions

```bash
# Disable compromised user
az ad user update --id USER_ID --account-enabled false

# Revoke sessions
az ad user update --id USER_ID --force-change-password-next-sign-in true

# Isolate VM (apply deny-all NSG)
az network nsg rule create --nsg-name forensic-nsg --name DenyAll \
  --priority 100 --access Deny --direction Inbound --protocol '*'

# Block storage account public access
az storage account update --name ACCOUNT --default-action Deny
```

### GCP Containment Actions

```bash
# Disable service account
gcloud iam service-accounts disable SA_EMAIL

# Remove IAM bindings
gcloud projects remove-iam-policy-binding PROJECT_ID \
  --member="user:COMPROMISED@domain.com" --role="roles/editor"

# Isolate VM (remove network tags, apply deny firewall)
gcloud compute firewall-rules create forensic-deny-all \
  --action=DENY --rules=all --target-tags=forensic-isolated
gcloud compute instances add-tags INSTANCE --tags=forensic-isolated
```

---

## Phase 3: Evidence Preservation

### Log Sources to Collect Immediately

| Cloud | Log Source | Command |
|-------|-----------|---------|
| AWS | CloudTrail | `aws cloudtrail lookup-events --start-time --end-time` |
| AWS | VPC Flow Logs | S3 bucket or CloudWatch Logs |
| AWS | GuardDuty findings | `aws guardduty list-findings` |
| AWS | S3 access logs | S3 server access logging bucket |
| Azure | Activity Log | Azure Monitor, export to storage |
| Azure | Sign-in logs | Azure AD, export to Log Analytics |
| Azure | NSG Flow Logs | Storage account |
| GCP | Cloud Audit Logs | Logging > Logs Explorer |
| GCP | VPC Flow Logs | Logging > Logs Explorer |
| GCP | Access Transparency Logs | Organization-level logging |

### Instance Forensics

```bash
# AWS: Create snapshot of compromised instance volume
aws ec2 create-snapshot --volume-id vol-xxx --description "Forensic - Incident INC-001"
# Tag for evidence chain
aws ec2 create-tags --resources snap-xxx --tags Key=Incident,Value=INC-001 Key=Evidence,Value=true

# AWS: Capture instance metadata
aws ec2 describe-instances --instance-ids i-xxx > instance_metadata.json

# Mount snapshot for analysis (attach to forensic workstation)
aws ec2 create-volume --snapshot-id snap-xxx --availability-zone us-east-1a
aws ec2 attach-volume --volume-id vol-new --instance-id i-forensic --device /dev/xvdf
```

---

## Phase 4: Investigation

### Step 4.1: CloudTrail/Audit Log Analysis

```bash
# AWS: Find all actions by compromised principal
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=Username,AttributeValue=COMPROMISED_USER \
  --start-time "2026-03-01T00:00:00Z" \
  --end-time "2026-03-07T00:00:00Z"

# Key events to look for:
# - CreateUser, CreateAccessKey, AttachUserPolicy (persistence)
# - RunInstances (cryptomining)
# - GetObject on S3 (data access)
# - CreateLoginProfile (backdoor access)
# - PutBucketPolicy (data exposure)
# - AssumeRole (privilege escalation)
# - CreateEventDataStore changes (covering tracks)
```

### Step 4.2: Determine Entry Vector

| Vector | Investigation Steps |
|--------|-------------------|
| Leaked credentials | Check code repos, paste sites, breach databases |
| SSRF to metadata | Check application logs for metadata endpoint access |
| Compromised CI/CD | Review pipeline logs, secret access |
| Third-party integration | Review OAuth tokens, cross-account roles |
| Phished credentials | Email logs, SSO sign-in anomalies |
| Overprivileged role | IAM policy analysis, unused permissions |

### Step 4.3: Assess Data Impact

```
1. What data stores were accessed?
2. What objects/rows were read or modified?
3. Was data exfiltrated (check VPC flow logs, S3 access logs)?
4. What is the classification of affected data?
5. Does this trigger breach notification requirements?
```

---

## Phase 5: Eradication and Recovery

### Step 5.1: Remove Persistence

- [ ] Remove unauthorized IAM users, roles, policies
- [ ] Delete unauthorized access keys
- [ ] Remove unauthorized EC2 key pairs
- [ ] Delete unauthorized Lambda functions
- [ ] Remove unauthorized CloudFormation/Terraform stacks
- [ ] Review and remove unauthorized VPC peering connections
- [ ] Check for unauthorized SNS/SQS subscriptions (data exfil)

### Step 5.2: Rotate Credentials

- [ ] Rotate all IAM access keys for affected accounts
- [ ] Rotate all secrets in Secrets Manager/Parameter Store that were accessible
- [ ] Rotate RDS/database passwords
- [ ] Update any hardcoded credentials (and move to secrets manager)
- [ ] Invalidate and regenerate API keys for third-party integrations

### Step 5.3: Harden Environment

- [ ] Enable MFA on all human IAM users
- [ ] Enforce IMDSv2 on all EC2 instances
- [ ] Enable GuardDuty/Defender in all regions
- [ ] Enable CloudTrail in all regions with organization trail
- [ ] Review and tighten IAM policies (least privilege)
- [ ] Enable S3 Block Public Access at account level

---

## Cross-References

- See `frameworks/cloudsec-layer.md` for cloud security methodology
- See `templates/runbooks/ransomware-response-runbook.md` for ransomware in cloud
- See `frameworks/nist-800-61-incident-response.md` for IR framework
- See `reference/tools/terraform-security-reference.md` for IaC remediation
- See `templates/communications/breach-notification-template.md` for data breach response
