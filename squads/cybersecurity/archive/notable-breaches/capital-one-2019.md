# Capital One Data Breach (2019)

## Incident Summary

| Field | Details |
|-------|---------|
| Organization | Capital One Financial Corporation |
| Date of Compromise | March 22-23, 2019 |
| Date Discovered | July 17, 2019 (via responsible disclosure on GitHub) |
| Date Disclosed | July 29, 2019 |
| Records Affected | 106 million individuals (US and Canada) |
| Data Exposed | Names, addresses, phone numbers, email, DOB, income, 140,000 SSNs, 80,000 bank account numbers, credit scores, transaction data |
| Attack Vector | SSRF (Server-Side Request Forgery) exploiting misconfigured WAF to access AWS metadata service |
| Root Cause | Cloud misconfiguration: overly permissive IAM role attached to WAF, SSRF vulnerability |
| Perpetrator | Paige Thompson (former AWS employee, not acting on behalf of AWS) |
| Financial Impact | $80M OCC fine, $190M consumer settlement, estimated $150M+ in breach costs |

---

## Attack Narrative

### Technical Attack Chain

**Step 1: SSRF via Misconfigured WAF**
The attacker exploited a Server-Side Request Forgery (SSRF) vulnerability in a misconfigured WAF (Web Application Firewall) that Capital One had deployed on AWS. The WAF was running as a reverse proxy with an overly permissive configuration that allowed it to be used to make requests to arbitrary internal endpoints.

**Step 2: AWS Metadata Service Access**
Using the SSRF, the attacker made a request to the AWS Instance Metadata Service (IMDS) at `http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE_NAME]`. This returned temporary AWS credentials (access key, secret key, session token) for the IAM role attached to the WAF instance.

**Step 3: Overly Permissive IAM Role**
The IAM role attached to the WAF had excessive permissions, including the ability to list and read S3 buckets. This violated the principle of least privilege -- a WAF does not need S3 access to function.

**Step 4: S3 Data Access**
Using the harvested credentials, the attacker:
```
# Listed Capital One S3 buckets
aws s3 ls

# Synced data from multiple buckets containing customer data
aws s3 sync s3://[BUCKET_NAME] /local/path/
```

**Step 5: Data Exfiltration**
Over 700 S3 folders containing customer data were accessed and exfiltrated. The attacker posted about the access on social media and shared data through various channels, ultimately leading to their identification.

### Detection
- **July 17, 2019**: A security researcher found a GitHub posting by the attacker containing Capital One data and reported it via Capital One's responsible disclosure program
- **July 19, 2019**: Capital One confirmed the breach and began investigation
- **July 29, 2019**: FBI arrested Paige Thompson; Capital One publicly disclosed the breach

## Root Cause Analysis

### Primary Failures

**1. SSRF Vulnerability in WAF Configuration**
The WAF was configured as a reverse proxy that could be abused to make server-side requests to any URL, including the AWS metadata service. This is a well-known cloud attack pattern that should have been mitigated by:
- Restricting the WAF from accessing the metadata service
- Using IMDSv2 (which requires a token-based approach, mitigating simple SSRF)
- Network-level restrictions on metadata service access

**2. Overly Permissive IAM Role**
The IAM role attached to the WAF instance had permissions far beyond what a WAF needs:
- ListBuckets: ability to enumerate all S3 buckets in the account
- GetObject: ability to read objects from S3 buckets
- A WAF needs zero S3 permissions to perform its function
- This violated least privilege in the most basic way

**3. No Detection of Anomalous S3 Access**
The exfiltration of 700+ S3 folders by a WAF instance was not detected by any monitoring system. Capital One was monitoring CloudTrail but did not have alerts for:
- S3 access from the WAF instance (which should never access S3)
- Bulk S3 object downloads
- IAM role credential usage from unexpected contexts

**4. No Metadata Service Protection**
AWS Instance Metadata Service v1 (IMDSv1) allows any process on the instance to retrieve credentials via a simple HTTP GET request. IMDSv2, which requires a PUT request with a hop limit, would have significantly complicated the SSRF exploitation.

**5. 4-Month Dwell Time**
The breach occurred in March 2019 but was not discovered until July 2019, and only because the attacker self-disclosed on GitHub. Without the responsible disclosure, the breach might have remained undetected indefinitely.

## Lessons for Defensive Operations

### Cloud IAM
- **Principle of least privilege is not optional in cloud environments**
- Every IAM role should have only the permissions necessary for its specific function
- Use AWS IAM Access Analyzer to identify overly permissive policies
- Implement SCPs (Service Control Policies) to prevent excessive permissions
- Regularly audit IAM roles for unused permissions (IAM Access Advisor)
- Separate roles per workload -- never share IAM roles between unrelated services

### SSRF Protection
- **SSRF is the #1 cloud-specific attack vector**
- Enable IMDSv2 and disable IMDSv1 on all EC2 instances:
```bash
aws ec2 modify-instance-metadata-options \
  --instance-id i-XXXXX \
  --http-tokens required \
  --http-endpoint enabled
```
- Block outbound access to 169.254.169.254 from application containers
- Implement SSRF-specific WAF rules
- Validate and sanitize all URLs processed by server-side code
- Use VPC endpoints to restrict metadata service access

### S3 Security
- Enable S3 Block Public Access at the account level
- Use S3 Access Points to scope bucket access per application
- Enable S3 server access logging or CloudTrail data events for sensitive buckets
- Alert on S3 API calls from unexpected IAM principals
- Encrypt sensitive data with CMK and restrict key access

### Cloud Detection
- **Monitor for credential use from unexpected sources**
- Alert when IAM role credentials are used from IP addresses outside expected ranges
- Detect bulk S3 read operations exceeding normal patterns
- Monitor CloudTrail for API calls to the metadata service from application instances
- Implement GuardDuty for automated threat detection
- Create SIEM rules for: unusual S3 access patterns, metadata service queries, cross-service credential usage

### Organizational Controls
- Conduct regular cloud security architecture reviews (see `workflows/security-architecture-review.md`)
- Run cloud penetration tests that specifically include SSRF and metadata attack scenarios
- Implement CSPM (Cloud Security Posture Management) for continuous misconfiguration detection
- Include SSRF protection in developer security training

## Regulatory and Legal Impact
- **OCC Fine**: $80 million (Capital One's banking regulator)
- **Consumer Settlement**: $190 million class action settlement
- **Consent Order**: Required Capital One to implement improved cloud security controls
- **Criminal Prosecution**: Paige Thompson convicted in June 2022
- **Industry Impact**: Accelerated AWS adoption of IMDSv2 and broader cloud security awareness

## ATT&CK Mapping

| Tactic | Technique | Specifics |
|--------|-----------|-----------|
| Initial Access | T1190 Exploit Public-Facing Application | SSRF in WAF |
| Credential Access | T1552 Unsecured Credentials | AWS metadata service credential theft |
| Discovery | T1580 Cloud Infrastructure Discovery | S3 bucket enumeration |
| Collection | T1530 Data from Cloud Storage | S3 object download |
| Exfiltration | T1537 Transfer Data to Cloud Account | Data exfiltrated to external systems |

## Cross-References

- `workflows/cloud-migration-security.md` — Cloud security architecture
- `scripts/cloud-security-audit.md` — Cloud misconfiguration detection
- `tasks/forensics/cloud-forensics.md` — Cloud evidence collection
- `frameworks/cloudsec-layer.md` — Cloud security framework
- `workflows/security-architecture-review.md` — Architecture review process
- `workflows/data-breach-response.md` — Breach response procedures
