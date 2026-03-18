# Cloud Environment Forensic Evidence Collection

## Purpose

Collect, preserve, and analyze forensic evidence from cloud environments (AWS, Azure, GCP) during security incidents. Cloud forensics differs fundamentally from traditional forensics: there is no physical hardware to image, evidence is ephemeral and API-driven, and the shared responsibility model means some evidence is only available through provider cooperation.

## Task Owner
Cloud security engineer or digital forensics analyst with cloud platform expertise.

## Prerequisites
- Privileged access to cloud accounts under investigation (or pre-configured IR roles)
- Cloud CLI tools configured: AWS CLI, Azure CLI, gcloud CLI
- Evidence storage bucket/account (separate from production, write-once)
- Legal hold procedures for cloud data retention
- Understanding of cloud provider evidence preservation timelines

---

## Phase 1: Immediate Evidence Preservation

### 1.1 Critical Timeline
Cloud evidence has limited retention windows. Act immediately:

| Evidence Type | Default Retention | Action Required |
|---------------|------------------|-----------------|
| CloudTrail events | 90 days (Event History) | Ensure trail logging to S3 with long retention |
| VPC Flow Logs | As configured (often 14 days) | Export immediately; extend retention |
| Instance memory | Lost on stop/terminate | Snapshot before any instance changes |
| Container logs | Pod lifecycle dependent | Export before pod restart/termination |
| Azure Activity Log | 90 days | Export to Log Analytics/Storage |
| GCP Audit Logs | Admin: 400 days; Data: 30 days | Export to Cloud Storage |

### 1.2 Immediate Preservation Actions
- [ ] Enable legal hold on all relevant cloud storage (S3 Object Lock, Azure Legal Hold)
- [ ] Create snapshots of all affected EC2/VM instances BEFORE any changes
- [ ] Export CloudTrail/Activity Logs/Audit Logs for investigation timeframe
- [ ] Preserve VPC Flow Logs / NSG Flow Logs
- [ ] Capture running container state before restart
- [ ] Export DNS query logs if enabled
- [ ] Preserve load balancer access logs
- [ ] Document all actions with timestamps in evidence log

### 1.3 Evidence Integrity
- [ ] Store all evidence in a dedicated, isolated cloud account/subscription
- [ ] Enable versioning and immutability on evidence storage
- [ ] Calculate hashes of all exported evidence files
- [ ] Restrict access to evidence storage to forensics team only
- [ ] Enable access logging on evidence storage bucket

## Phase 2: API and Management Plane Evidence

### 2.1 AWS Evidence Collection
```bash
# CloudTrail - API activity log (the primary evidence source)
aws cloudtrail lookup-events \
  --start-time "2026-03-01T00:00:00Z" \
  --end-time "2026-03-06T23:59:59Z" \
  --output json > cloudtrail_events.json

# For specific user activity
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=Username,AttributeValue=suspect_user \
  --output json > user_activity.json

# S3 access logs (if enabled on buckets)
aws s3 sync s3://bucket-access-logs/ /evidence/s3-logs/

# IAM credential report
aws iam generate-credential-report
aws iam get-credential-report --output text --query Content | base64 -d > iam_cred_report.csv

# Access Analyzer findings
aws accessanalyzer list-findings --analyzer-arn [ARN] > access_findings.json

# GuardDuty findings
aws guardduty list-findings --detector-id [ID] > guardduty_findings.json

# VPC Flow Logs
aws logs get-log-events --log-group-name /vpc/flowlogs/[vpc-id] > flow_logs.json

# EKS audit logs (if Kubernetes)
aws logs filter-log-events --log-group-name /aws/eks/[cluster]/cluster > eks_audit.json
```

### 2.2 Azure Evidence Collection
```bash
# Activity Log
az monitor activity-log list \
  --start-time "2026-03-01T00:00:00Z" \
  --end-time "2026-03-06T23:59:59Z" \
  --output json > activity_log.json

# Sign-in logs
az ad audit-log sign-in list --output json > signin_logs.json

# Azure AD audit logs
az ad audit-log audit list --output json > aad_audit.json

# NSG Flow Logs
# Export from Storage Account where flow logs are stored

# Defender for Cloud alerts
az security alert list --output json > defender_alerts.json

# Key Vault access logs
az monitor diagnostic-settings list --resource [keyvault-resource-id]

# Azure Kubernetes Service audit logs
az aks show --resource-group [RG] --name [CLUSTER] --output json
```

### 2.3 GCP Evidence Collection
```bash
# Admin Activity audit logs
gcloud logging read 'logName="projects/[PROJECT]/logs/cloudaudit.googleapis.com%2Factivity"' \
  --project=[PROJECT] --freshness=7d --format=json > admin_audit.json

# Data Access audit logs
gcloud logging read 'logName="projects/[PROJECT]/logs/cloudaudit.googleapis.com%2Fdata_access"' \
  --project=[PROJECT] --freshness=7d --format=json > data_access.json

# VPC Flow Logs
gcloud logging read 'resource.type="gce_subnetwork"' \
  --project=[PROJECT] --freshness=7d --format=json > vpc_flows.json

# IAM policy analysis
gcloud asset search-all-iam-policies --scope=projects/[PROJECT] > iam_policies.json

# Security Command Center findings
gcloud scc findings list [ORG_ID] --format=json > scc_findings.json
```

## Phase 3: Compute Instance Evidence

### 3.1 Instance Snapshot and Image
```bash
# AWS - Create EBS snapshot
aws ec2 create-snapshot --volume-id vol-XXXXX --description "Forensic snapshot - CASE-2026-001"

# AWS - Create AMI for full instance preservation
aws ec2 create-image --instance-id i-XXXXX --name "forensic-case-001" --no-reboot

# Azure - Create VM snapshot
az snapshot create --resource-group [RG] --name forensic-snap --source [DISK-ID]

# GCP - Create disk snapshot
gcloud compute disks snapshot [DISK-NAME] --snapshot-names=forensic-case-001 --zone=[ZONE]
```

### 3.2 Memory Acquisition from Cloud Instances
Cloud instances do not support traditional memory acquisition. Alternatives:
- [ ] AWS: Use SSM to run memory acquisition tool (LiME, WinPmem) on live instance
- [ ] Azure: Use Run Command to execute memory capture
- [ ] GCP: Use OS Login or SSH to run memory acquisition tool
- [ ] Alternative: Analyze hibernation file if instance was hibernated
- [ ] If instance is terminated, memory is unrecoverable

### 3.3 Container and Serverless Evidence
```bash
# Kubernetes pod logs
kubectl logs [POD_NAME] --all-containers --timestamps > pod_logs.txt
kubectl logs [POD_NAME] --all-containers --previous > pod_previous_logs.txt

# Container image analysis
docker save [IMAGE:TAG] > container_image.tar

# Lambda function versions and configuration
aws lambda get-function --function-name [NAME] > lambda_config.json
aws lambda list-versions-by-function --function-name [NAME] > lambda_versions.json

# CloudWatch Logs for serverless
aws logs get-log-events --log-group-name /aws/lambda/[FUNCTION] > lambda_logs.json
```

## Phase 4: Identity and Access Evidence

### 4.1 Compromised Identity Investigation
- [ ] Pull all API calls made by suspected compromised identity
- [ ] Identify source IPs for API calls (compare against known legitimate IPs)
- [ ] Check for access key creation, IAM policy changes, role assumption
- [ ] Review MFA status changes
- [ ] Check for console login from unusual locations
- [ ] Identify cross-account role assumptions
- [ ] Review temporary credential issuance (STS AssumeRole)

### 4.2 Permission Analysis
- [ ] Document effective permissions of compromised identity at time of incident
- [ ] Identify privilege escalation paths used
- [ ] Check for IAM policy modifications during incident window
- [ ] Review service-linked roles and their usage
- [ ] Identify resource policies modified (S3 bucket policies, KMS key policies)

## Phase 5: Data Access Evidence

### 5.1 Storage Access Analysis
- [ ] Review S3/Blob/GCS access logs for unauthorized data access
- [ ] Check for bulk download patterns (GetObject calls at scale)
- [ ] Identify bucket policy or ACL changes
- [ ] Check for public access configuration changes
- [ ] Review data transfer logs (cross-region, cross-account)
- [ ] Check for presigned URL generation

### 5.2 Database Access Analysis
- [ ] Review RDS/SQL audit logs for query patterns
- [ ] Check for snapshot sharing or export
- [ ] Identify database credential access from secrets manager
- [ ] Review DynamoDB/Cosmos DB access patterns

## Phase 6: Analysis and Reporting

### 6.1 Timeline Construction
- [ ] Build unified timeline from all cloud evidence sources
- [ ] Correlate API calls with network logs and identity events
- [ ] Map attacker progression: initial access, persistence, privilege escalation, impact
- [ ] Identify data accessed, modified, or exfiltrated
- [ ] Determine blast radius (all resources accessed by compromised identity)

### 6.2 Cloud Forensics Report
- [ ] Incident summary and scope
- [ ] Evidence sources and collection methods
- [ ] Timeline of attacker activity
- [ ] Identity compromise analysis
- [ ] Data impact assessment
- [ ] Infrastructure modifications made by attacker
- [ ] IOCs (IPs, user agents, API patterns)
- [ ] Remediation actions taken and recommended
- [ ] Evidence integrity documentation

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Instance disk analysis
- `tasks/forensics/memory-forensics.md` — Instance memory analysis
- `workflows/incident-response-workflow.md` — IR process
- `scripts/cloud-security-audit.md` — Cloud audit automation
- `workflows/cloud-migration-security.md` — Cloud security architecture
- `archive/notable-breaches/capital-one-2019.md` — Cloud breach case study

## Routing & Escalation

| Campo | Valor |
|-------|-------|
| Frameworks | evidence-standard, nist-800-61-incident-response |
| Checklists | forensics-collection-quality, evidence-chain-quality |
| Templates | reports/postmortem-template |
| Registry | data/registries/incident-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief
- **Owner**: chris-sanders + shannon-runner
