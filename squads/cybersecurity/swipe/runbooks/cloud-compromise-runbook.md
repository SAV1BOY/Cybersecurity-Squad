# Cloud Account Compromise Response Runbook

## Purpose

Response procedures for cloud account compromise incidents covering token revocation, IAM audit, resource enumeration, cost anomaly detection, and cloud-specific evidence preservation across AWS, Azure, and GCP.

## Cloud Compromise Indicators

| Indicator | Source | Severity |
|-----------|--------|----------|
| Console login from unusual location/IP | CloudTrail/Activity Log | High |
| API calls from never-seen-before IP | Cloud audit logs | High |
| New IAM user/role/service principal created | IAM audit logs | Critical |
| New access key pair generated | IAM audit logs | Critical |
| Security group modified (0.0.0.0/0 ingress) | Config change logs | High |
| New EC2/VM instances launched (unusual type/region) | Compute logs | High |
| S3/Blob policy changed to public | Storage access logs | Critical |
| CloudTrail/audit logging disabled | Management logs | Critical |
| Cost anomaly alert | Billing/cost management | Medium |
| GuardDuty/Defender/SCC high-severity finding | Security services | High |

## Phase 1: Containment (First 30 Minutes)

### AWS Containment

```bash
# 1. Identify compromised identity
# Review CloudTrail for the suspicious activity source
aws cloudtrail lookup-events \
    --lookup-attributes AttributeKey=EventSource,AttributeValue=iam.amazonaws.com \
    --start-time "2026-03-05T00:00:00Z" \
    --max-results 50

# 2. Disable compromised access keys
aws iam update-access-key \
    --user-name COMPROMISED_USER \
    --access-key-id AKIAXXXXXXXXXXXXXXXX \
    --status Inactive

# 3. Disable compromised IAM user (if user account)
aws iam delete-login-profile --user-name COMPROMISED_USER

# 4. Revoke all sessions for IAM role (attach inline deny-all policy)
aws iam put-user-policy \
    --user-name COMPROMISED_USER \
    --policy-name DenyAll-IncidentResponse \
    --policy-document '{
      "Version":"2012-10-17",
      "Statement":[{
        "Effect":"Deny",
        "Action":"*",
        "Resource":"*",
        "Condition":{"DateLessThan":{"aws:TokenIssueTime":"2026-03-06T12:00:00Z"}}
      }]
    }'

# 5. For compromised role - revoke sessions
aws iam put-role-policy \
    --role-name COMPROMISED_ROLE \
    --policy-name RevokeOlderSessions \
    --policy-document '{
      "Version":"2012-10-17",
      "Statement":[{
        "Effect":"Deny",
        "Action":"*",
        "Resource":"*",
        "Condition":{"DateLessThan":{"aws:TokenIssueTime":"2026-03-06T12:00:00Z"}}
      }]
    }'

# 6. Verify CloudTrail is still enabled
aws cloudtrail get-trail-status --name management-trail
```

### Azure Containment

```powershell
# 1. Revoke all user sessions
Revoke-AzureADUserAllRefreshToken -ObjectId "USER_OBJECT_ID"

# 2. Reset user password
Set-AzureADUserPassword -ObjectId "USER_OBJECT_ID" `
    -Password (ConvertTo-SecureString "TempP@ss!" -AsPlainText -Force) `
    -ForceChangePasswordNextLogin $true

# 3. Disable user account
Set-AzureADUser -ObjectId "USER_OBJECT_ID" -AccountEnabled $false

# 4. Block sign-in for service principal
Set-AzureADServicePrincipal -ObjectId "SP_OBJECT_ID" -AccountEnabled $false

# 5. Remove compromised service principal credentials
Remove-AzureADServicePrincipalKeyCredential -ObjectId "SP_OBJECT_ID" `
    -KeyId "KEY_ID"

# 6. Check Conditional Access policies are intact
Get-AzureADMSConditionalAccessPolicy | Select-Object DisplayName, State
```

### GCP Containment

```bash
# 1. Disable compromised service account
gcloud iam service-accounts disable \
    compromised@project-id.iam.gserviceaccount.com

# 2. Delete service account keys
gcloud iam service-accounts keys list \
    --iam-account=compromised@project-id.iam.gserviceaccount.com
gcloud iam service-accounts keys delete KEY_ID \
    --iam-account=compromised@project-id.iam.gserviceaccount.com

# 3. Disable user account (Google Workspace)
gcloud identity users update user@domain.com --suspended

# 4. Verify audit logging is enabled
gcloud logging sinks list
gcloud projects get-iam-policy PROJECT_ID
```

## Phase 2: IAM Audit (Hours 1-4)

### IAM Changes to Investigate

| Change Type | Why It Matters | How to Check |
|------------|---------------|-------------|
| New IAM users/roles created | Persistence mechanism | List all users/roles created in window |
| New access keys generated | Long-term credential persistence | List access keys with creation dates |
| Policy changes | Privilege escalation | Compare current vs baseline policies |
| New MFA devices registered | Account takeover persistence | List MFA devices per user |
| Trust policy changes (AWS) | Cross-account access | Review role trust policies |
| Service principal credentials | Azure persistence | List SP credentials and creation dates |
| OAuth app consents | API access persistence | Review granted permissions |
| Federation trust changes | Identity bypass | Check SAML/OIDC configurations |

### AWS IAM Audit Queries

```bash
# List all IAM changes in the last 24 hours
aws cloudtrail lookup-events \
    --lookup-attributes AttributeKey=EventSource,AttributeValue=iam.amazonaws.com \
    --start-time $(date -u -d '24 hours ago' '+%Y-%m-%dT%H:%M:%SZ') \
    --max-results 100 \
    --query 'Events[].{Time:EventTime,Name:EventName,User:Username}'

# Check for new users
aws iam list-users --query 'Users[?CreateDate>=`2026-03-05`]'

# Check for new roles
aws iam list-roles --query 'Roles[?CreateDate>=`2026-03-05`]'

# Check for new access keys
for user in $(aws iam list-users --query 'Users[].UserName' --output text); do
    aws iam list-access-keys --user-name $user \
        --query "AccessKeyMetadata[?CreateDate>=\`2026-03-05\`]"
done
```

## Phase 3: Resource Enumeration

### Check for Attacker-Created Resources

| Resource Type | Why Attackers Create Them | Impact |
|--------------|--------------------------|--------|
| Compute instances | Cryptomining, C2, pivoting | Cost, security |
| Lambda/Functions | Persistence, data processing | Cost, data access |
| S3 buckets/Storage | Data staging, exfiltration | Data exposure |
| VPC/Network changes | Backdoor access, NAT bypass | Network security |
| Snapshots/AMIs | Data theft, persistence | Data exposure |
| DNS records | C2, phishing infrastructure | Reputation |

### AWS Resource Enumeration

```bash
# List all EC2 instances across all regions
for region in $(aws ec2 describe-regions --query 'Regions[].RegionName' --output text); do
    echo "Region: $region"
    aws ec2 describe-instances --region $region \
        --query 'Reservations[].Instances[].{ID:InstanceId,Type:InstanceType,LaunchTime:LaunchTime,State:State.Name}' \
        --output table
done

# Check for Lambda functions created recently
aws lambda list-functions \
    --query 'Functions[].{Name:FunctionName,Modified:LastModified,Runtime:Runtime}'

# Check for new S3 buckets
aws s3api list-buckets \
    --query 'Buckets[?CreationDate>=`2026-03-05`].{Name:Name,Created:CreationDate}'

# Check for new security groups
aws ec2 describe-security-groups \
    --query 'SecurityGroups[?contains(IpPermissions[].IpRanges[].CidrIp, `0.0.0.0/0`)].{ID:GroupId,Name:GroupName}'
```

## Phase 4: Cost Anomaly Analysis

### Cost Indicators of Compromise

| Service | Anomaly | Likely Attack |
|---------|---------|--------------|
| EC2/Compute | Spike in large GPU instances | Cryptomining |
| Lambda/Functions | Massive invocation spike | Cryptomining or DDoS |
| Data Transfer | Large outbound transfer spike | Data exfiltration |
| S3 | Unusual API request volume | Data access/exfiltration |
| EBS/Disks | Many snapshots created | Data theft |
| Route 53/DNS | New hosted zones | C2 infrastructure |

```bash
# AWS Cost Explorer - check for anomalies
aws ce get-cost-and-usage \
    --time-period Start=2026-03-01,End=2026-03-06 \
    --granularity DAILY \
    --metrics BlendedCost \
    --group-by Type=DIMENSION,Key=SERVICE

# Check for active cost anomalies
aws ce get-anomalies \
    --date-interval '{"StartDate":"2026-03-01","EndDate":"2026-03-06"}' \
    --max-results 10
```

## Phase 5: Evidence Preservation

### Log Preservation Priority

| Log Source | AWS | Azure | GCP | Retention |
|-----------|-----|-------|-----|-----------|
| Management API logs | CloudTrail | Activity Log | Admin Activity | Copy to secure bucket |
| Data API logs | S3 data events | Diagnostic logs | Data Access | Copy to secure bucket |
| Network logs | VPC Flow Logs | NSG Flow Logs | VPC Flow Logs | Copy to secure bucket |
| DNS logs | Route 53 query logs | DNS Analytics | Cloud DNS logs | Copy to secure bucket |
| Compute logs | CloudWatch Logs | Azure Monitor | Cloud Logging | Copy to secure bucket |

### Evidence Preservation Steps

```
1. Create forensic storage (separate account/subscription)
   - Dedicated S3 bucket/storage with:
     - Object lock (WORM)
     - Server-side encryption (CMK)
     - Access logging enabled
     - Cross-account write-only access for IR team

2. Export and preserve:
   - CloudTrail/Activity Log/Audit Logs (full period)
   - VPC Flow Logs for affected VPCs
   - GuardDuty/Defender/SCC findings
   - IAM configuration snapshot (all users, roles, policies)
   - Resource configuration snapshot (AWS Config, etc.)
   - Cost and billing data
   - Any EBS snapshots of compromised instances

3. Instance forensics:
   - Create EBS snapshots BEFORE stopping instances
   - If memory forensics needed: use SSM to dump memory first
   - Do NOT terminate instances until evidence is preserved
   - Tag all evidence with case number and timestamp
```

## Phase 6: Remediation

### Credential Rotation

| Credential Type | Rotation Method | Priority |
|----------------|----------------|----------|
| IAM access keys | Delete and recreate | Immediate |
| Console passwords | Force password reset | Immediate |
| Service account keys | Rotate in secrets manager | Immediate |
| Application secrets | Rotate in vault/parameter store | Within 24 hours |
| OAuth tokens | Revoke and re-authorize | Immediate |
| SSH keys | Replace on all instances | Within 24 hours |
| API keys (third-party) | Rotate at provider | Within 24 hours |
| Database passwords | Rotate and update applications | Within 24 hours |

### Architecture Hardening

| Action | Implementation | Timeline |
|--------|---------------|----------|
| Enable MFA on all console users | IAM MFA enforcement | Immediate |
| Enable SCPs to prevent log disable | Organization policy | 24 hours |
| Enable GuardDuty/Defender/SCC | Security service activation | 24 hours |
| Review and restrict network access | Security group audit | 48 hours |
| Implement least-privilege IAM | Access Analyzer review | 1 week |
| Enable S3 Block Public Access | Account-level setting | Immediate |
| Implement budget alerts | Cost management | 24 hours |

## Cross-References

- [Secure Cloud Architecture](../../frameworks/secure-cloud-architecture.md) -- architecture patterns
- [Cloud Shared Responsibility](../../frameworks/cloud-shared-responsibility.md) -- responsibility model
- [Cloud Security Assessment Examples](../reports/cloud-security-assessment-examples.md) -- reporting
- [Incident Severity Classification](../../frameworks/incident-severity-classification.md) -- severity rating
