# Cloud Security Audit Scripts

## Purpose

Provide automated audit scripts for identifying security misconfigurations, policy violations, and public exposure across AWS, Azure, and GCP environments. These scripts operationalize CIS Benchmarks and cloud security best practices into executable checks.

## Prerequisites
- Cloud CLI tools configured with read-only audit permissions
- Credentials with SecurityAudit (AWS), Reader + Security Reader (Azure), Viewer (GCP) roles
- jq installed for JSON processing

---

## AWS Security Audit

### IAM Audit

```bash
#!/bin/bash
# aws_iam_audit.sh - IAM security configuration audit
echo "=== AWS IAM Security Audit ==="

# Check for root account usage (last 90 days)
echo "[CHECK] Root account usage..."
aws iam generate-credential-report > /dev/null 2>&1
sleep 5
aws iam get-credential-report --output text --query Content | \
  base64 -d | grep "<root_account>" | \
  awk -F, '{print "Root last used: " $5 ", MFA: " $8, ", Access Key 1: " $9}'

# Users without MFA
echo "[CHECK] Users without MFA enabled..."
aws iam list-users --query 'Users[*].UserName' --output text | tr '\t' '\n' | while read user; do
  MFA=$(aws iam list-mfa-devices --user-name "$user" --query 'MFADevices' --output text)
  if [ -z "$MFA" ]; then
    echo "  [FAIL] $user - NO MFA"
  fi
done

# Access keys older than 90 days
echo "[CHECK] Access keys older than 90 days..."
aws iam list-users --query 'Users[*].UserName' --output text | tr '\t' '\n' | while read user; do
  aws iam list-access-keys --user-name "$user" --query 'AccessKeyMetadata[?Status==`Active`].[AccessKeyId,CreateDate]' --output text | while read key date; do
    AGE=$(( ($(date +%s) - $(date -d "$date" +%s)) / 86400 ))
    if [ "$AGE" -gt 90 ]; then
      echo "  [FAIL] $user - Key $key is $AGE days old"
    fi
  done
done

# Unused IAM roles (no activity in 90 days)
echo "[CHECK] Unused IAM roles..."
aws iam list-roles --query 'Roles[?RoleLastUsed.LastUsedDate!=`null`].[RoleName,RoleLastUsed.LastUsedDate]' --output text | while read role date; do
  if [ ! -z "$date" ]; then
    AGE=$(( ($(date +%s) - $(date -d "$date" +%s)) / 86400 ))
    if [ "$AGE" -gt 90 ]; then
      echo "  [WARN] $role - Last used $AGE days ago"
    fi
  fi
done

# Policies with admin access (*)
echo "[CHECK] Policies with full admin (*:*) access..."
aws iam list-policies --scope Local --query 'Policies[*].[PolicyName,Arn]' --output text | while read name arn; do
  VERSION=$(aws iam get-policy --policy-arn "$arn" --query 'Policy.DefaultVersionId' --output text)
  ADMIN=$(aws iam get-policy-version --policy-arn "$arn" --version-id "$VERSION" --query 'PolicyVersion.Document' --output text | grep -c '"*"')
  if [ "$ADMIN" -gt 1 ]; then
    echo "  [FAIL] $name has wildcard (*) permissions"
  fi
done
```

### S3 Bucket Audit

```bash
#!/bin/bash
# aws_s3_audit.sh - S3 security configuration audit
echo "=== AWS S3 Security Audit ==="

# Check account-level public access block
echo "[CHECK] Account-level S3 Block Public Access..."
aws s3control get-public-access-block --account-id $(aws sts get-caller-identity --query Account --output text) 2>&1
if [ $? -ne 0 ]; then
  echo "  [FAIL] Account-level Block Public Access NOT configured"
fi

# Per-bucket audit
echo "[CHECK] Per-bucket security audit..."
aws s3api list-buckets --query 'Buckets[*].Name' --output text | tr '\t' '\n' | while read bucket; do
  echo "  Bucket: $bucket"

  # Check public access block
  PUB=$(aws s3api get-public-access-block --bucket "$bucket" 2>&1)
  if echo "$PUB" | grep -q "NoSuchPublicAccessBlockConfiguration"; then
    echo "    [FAIL] No public access block configured"
  fi

  # Check bucket encryption
  ENC=$(aws s3api get-bucket-encryption --bucket "$bucket" 2>&1)
  if echo "$ENC" | grep -q "ServerSideEncryptionConfigurationNotFoundError"; then
    echo "    [FAIL] Default encryption NOT enabled"
  fi

  # Check versioning
  VER=$(aws s3api get-bucket-versioning --bucket "$bucket" --query 'Status' --output text)
  if [ "$VER" != "Enabled" ]; then
    echo "    [WARN] Versioning not enabled"
  fi

  # Check logging
  LOG=$(aws s3api get-bucket-logging --bucket "$bucket" --query 'LoggingEnabled' --output text)
  if [ "$LOG" == "None" ]; then
    echo "    [WARN] Access logging not enabled"
  fi
done
```

### EC2 and Network Audit

```bash
#!/bin/bash
# aws_network_audit.sh - EC2 and network security audit
echo "=== AWS Network Security Audit ==="

# Security groups with 0.0.0.0/0 ingress (non-HTTP/HTTPS)
echo "[CHECK] Security groups with unrestricted ingress..."
aws ec2 describe-security-groups --query 'SecurityGroups[*].[GroupId,GroupName,IpPermissions]' --output json | \
  jq -r '.[] | select(.[2][]?.IpRanges[]?.CidrIp == "0.0.0.0/0") | select(.[2][]?.FromPort != 80 and .[2][]?.FromPort != 443) | "\(.[0]) \(.[1])"' | sort -u | while read sg name; do
  echo "  [FAIL] $sg ($name) allows 0.0.0.0/0 on non-web ports"
done

# Instances with public IPs
echo "[CHECK] Instances with public IP addresses..."
aws ec2 describe-instances --query 'Reservations[*].Instances[?PublicIpAddress!=null].[InstanceId,PublicIpAddress,Tags[?Key==`Name`].Value|[0]]' --output text | while read id ip name; do
  echo "  [INFO] $id ($name) - Public IP: $ip"
done

# EBS volumes without encryption
echo "[CHECK] Unencrypted EBS volumes..."
aws ec2 describe-volumes --query 'Volumes[?Encrypted==`false`].[VolumeId,Size,State]' --output text | while read vol size state; do
  echo "  [FAIL] $vol - ${size}GB, $state - NOT encrypted"
done

# IMDSv1 enabled instances (SSRF risk)
echo "[CHECK] Instances with IMDSv1 enabled..."
aws ec2 describe-instances --query 'Reservations[*].Instances[?MetadataOptions.HttpTokens!=`required`].[InstanceId,Tags[?Key==`Name`].Value|[0],MetadataOptions.HttpTokens]' --output text | while read id name tokens; do
  echo "  [FAIL] $id ($name) - IMDSv1 enabled (HttpTokens: $tokens)"
done

# VPC Flow Logs check
echo "[CHECK] VPCs without flow logs..."
VPCS=$(aws ec2 describe-vpcs --query 'Vpcs[*].VpcId' --output text)
for vpc in $VPCS; do
  FLOWS=$(aws ec2 describe-flow-logs --filter "Name=resource-id,Values=$vpc" --query 'FlowLogs' --output text)
  if [ -z "$FLOWS" ]; then
    echo "  [FAIL] $vpc - No VPC Flow Logs enabled"
  fi
done
```

### CloudTrail Audit

```bash
#!/bin/bash
# aws_cloudtrail_audit.sh
echo "=== AWS CloudTrail Audit ==="

# Check CloudTrail is enabled in all regions
echo "[CHECK] CloudTrail multi-region logging..."
aws cloudtrail describe-trails --query 'trailList[*].[Name,IsMultiRegionTrail,LogFileValidationEnabled,S3BucketName]' --output text | while read name multi validation bucket; do
  echo "  Trail: $name"
  [ "$multi" == "False" ] && echo "    [FAIL] Multi-region: DISABLED"
  [ "$validation" == "False" ] && echo "    [FAIL] Log validation: DISABLED"
done

# Check for CloudTrail log encryption
echo "[CHECK] CloudTrail log encryption..."
aws cloudtrail describe-trails --query 'trailList[?KmsKeyId==null].Name' --output text | tr '\t' '\n' | while read trail; do
  echo "  [WARN] $trail - Not encrypted with KMS"
done
```

## Azure Security Audit

### Azure Identity Audit

```bash
#!/bin/bash
# azure_identity_audit.sh
echo "=== Azure Identity Security Audit ==="

# Users without MFA (requires Azure AD Premium)
echo "[CHECK] Checking MFA registration status..."
az ad user list --query '[*].[displayName,userPrincipalName]' -o tsv | head -20
echo "  [NOTE] Full MFA audit requires Graph API and Azure AD Premium"

# Service principals with high privileges
echo "[CHECK] Service principals with Owner/Contributor role..."
az role assignment list --role "Owner" --query '[?principalType==`ServicePrincipal`].[principalName,scope]' -o tsv
az role assignment list --role "Contributor" --query '[?principalType==`ServicePrincipal`].[principalName,scope]' -o tsv

# Guest users
echo "[CHECK] Guest users in Azure AD..."
az ad user list --filter "userType eq 'Guest'" --query '[*].[displayName,userPrincipalName,createdDateTime]' -o tsv
```

### Azure Storage Audit

```bash
#!/bin/bash
# azure_storage_audit.sh
echo "=== Azure Storage Security Audit ==="

# Storage accounts allowing public blob access
echo "[CHECK] Storage accounts with public access..."
az storage account list --query '[*].[name,resourceGroup,allowBlobPublicAccess]' -o tsv | while read name rg public; do
  if [ "$public" == "true" ] || [ "$public" == "" ]; then
    echo "  [FAIL] $name ($rg) - Public blob access allowed"
  fi
done

# Storage accounts without HTTPS-only
echo "[CHECK] Storage accounts without HTTPS enforcement..."
az storage account list --query '[?enableHttpsTrafficOnly==`false`].[name,resourceGroup]' -o tsv | while read name rg; do
  echo "  [FAIL] $name ($rg) - HTTPS not enforced"
done

# Storage accounts with shared key access (prefer Azure AD)
echo "[CHECK] Storage accounts with shared key access..."
az storage account list --query '[?allowSharedKeyAccess!=`false`].[name,resourceGroup]' -o tsv | while read name rg; do
  echo "  [WARN] $name ($rg) - Shared key access enabled"
done
```

## GCP Security Audit

```bash
#!/bin/bash
# gcp_audit.sh - GCP security configuration audit
PROJECT=$1
echo "=== GCP Security Audit for $PROJECT ==="

# Check for overly permissive IAM bindings
echo "[CHECK] IAM bindings with allUsers or allAuthenticatedUsers..."
gcloud projects get-iam-policy "$PROJECT" --format=json | \
  jq -r '.bindings[] | select(.members[] | contains("allUsers") or contains("allAuthenticatedUsers")) | "\(.role): \(.members[])"'

# Public GCS buckets
echo "[CHECK] Public GCS buckets..."
gsutil ls -p "$PROJECT" 2>/dev/null | while read bucket; do
  IAM=$(gsutil iam get "$bucket" 2>/dev/null)
  if echo "$IAM" | grep -q "allUsers\|allAuthenticatedUsers"; then
    echo "  [FAIL] $bucket - Publicly accessible"
  fi
done

# Firewall rules allowing 0.0.0.0/0
echo "[CHECK] Firewall rules with unrestricted source..."
gcloud compute firewall-rules list --project="$PROJECT" --format=json | \
  jq -r '.[] | select(.sourceRanges[]? == "0.0.0.0/0") | select(.direction == "INGRESS") | "\(.name): \(.allowed[].ports // ["all"])"'

# Audit logging configuration
echo "[CHECK] Audit logging configuration..."
gcloud projects get-iam-policy "$PROJECT" --format=json | \
  jq '.auditConfigs // "No audit config found"'

echo "[*] GCP audit complete"
```

## Cross-References

- `workflows/cloud-migration-security.md` — Cloud security architecture
- `archive/notable-breaches/capital-one-2019.md` — Cloud misconfiguration breach
- `frameworks/cloudsec-layer.md` — Cloud security framework
- `tasks/forensics/cloud-forensics.md` — Cloud evidence collection
- `checklists/cloud-security-assessment-quality.md` — Cloud assessment checklist
