# Terraform Security Reference

## Purpose

Operational reference for securing Terraform-managed infrastructure. Covers provider hardening, state file protection, policy-as-code implementation with Sentinel and OPA, drift detection, and secure CI/CD pipeline integration for infrastructure-as-code security.

## State File Security

### Threat Model

The Terraform state file contains:
- Resource IDs and attributes
- Plaintext secrets (database passwords, API keys, TLS private keys)
- Network topology and configuration details
- Full infrastructure map useful for adversary reconnaissance

### Remote Backend Configuration (Required)

```hcl
# S3 backend with encryption and access control
terraform {
  backend "s3" {
    bucket         = "org-terraform-state"
    key            = "environments/production/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    kms_key_id     = "arn:aws:kms:us-east-1:ACCOUNT:key/KEY_ID"
    dynamodb_table = "terraform-state-locks"
    acl            = "private"
  }
}

# Azure backend
terraform {
  backend "azurerm" {
    resource_group_name  = "tfstate-rg"
    storage_account_name = "orgtfstate"
    container_name       = "tfstate"
    key                  = "production.tfstate"
    use_oidc             = true
  }
}
```

### State File Protection Checklist

- [ ] Remote backend enabled (never local state in production)
- [ ] Encryption at rest (S3 SSE-KMS, Azure Storage encryption)
- [ ] Encryption in transit (TLS enforced)
- [ ] State locking enabled (DynamoDB, Azure Blob lease)
- [ ] Access restricted to CI/CD service accounts only
- [ ] Versioning enabled for state recovery
- [ ] No state file in version control (`.gitignore` includes `*.tfstate*`)
- [ ] State access logged and auditable

## Provider Hardening

### AWS Provider

```hcl
provider "aws" {
  region = var.region

  # Never hardcode credentials
  # Use: IAM roles, OIDC federation, or environment variables

  default_tags {
    tags = {
      ManagedBy   = "terraform"
      Environment = var.environment
      Owner       = var.team
    }
  }

  # Restrict to specific account
  allowed_account_ids = [var.aws_account_id]
}
```

### Credential Management

| Method | Security Level | Use Case |
|--------|---------------|----------|
| Hardcoded in HCL | NEVER | Never acceptable |
| Environment variables | Acceptable | Local development |
| AWS IAM Instance Role | Good | EC2-based runners |
| OIDC Federation | Best | CI/CD (GitHub Actions, GitLab) |
| Vault Dynamic Secrets | Best | Short-lived credentials |

### Sensitive Variables

```hcl
variable "db_password" {
  type      = string
  sensitive = true  # Prevents display in plan/apply output
}

# Use data sources for secrets
data "aws_secretsmanager_secret_version" "db_password" {
  secret_id = "production/database/password"
}

resource "aws_db_instance" "main" {
  password = data.aws_secretsmanager_secret_version.db_password.secret_string
}
```

## Policy-as-Code

### HashiCorp Sentinel

```python
# Sentinel policy: enforce encryption on S3 buckets
import "tfplan/v2" as tfplan

s3_buckets = filter tfplan.resource_changes as _, rc {
    rc.type is "aws_s3_bucket" and
    (rc.change.actions contains "create" or rc.change.actions contains "update")
}

main = rule {
    all s3_buckets as _, bucket {
        bucket.change.after.server_side_encryption_configuration is not null
    }
}

# Sentinel policy: restrict instance types
allowed_types = ["t3.micro", "t3.small", "t3.medium"]
ec2_instances = filter tfplan.resource_changes as _, rc {
    rc.type is "aws_instance"
}
main = rule {
    all ec2_instances as _, instance {
        instance.change.after.instance_type in allowed_types
    }
}
```

### Open Policy Agent (OPA/Conftest)

```rego
# OPA policy: deny public S3 buckets
package terraform.s3

deny[msg] {
    resource := input.resource_changes[_]
    resource.type == "aws_s3_bucket"
    resource.change.after.acl == "public-read"
    msg := sprintf("S3 bucket '%s' must not be publicly readable", [resource.name])
}

# OPA policy: require tags
deny[msg] {
    resource := input.resource_changes[_]
    required_tags := {"Environment", "Owner", "ManagedBy"}
    provided_tags := {tag | resource.change.after.tags[tag]}
    missing := required_tags - provided_tags
    count(missing) > 0
    msg := sprintf("Resource '%s' missing required tags: %v", [resource.name, missing])
}
```

### CI/CD Integration

```yaml
# GitHub Actions with security checks
jobs:
  terraform:
    steps:
      - name: Terraform Init
        run: terraform init

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Convert Plan to JSON
        run: terraform show -json tfplan > tfplan.json

      - name: OPA Policy Check
        run: conftest test tfplan.json --policy policies/

      - name: tfsec Static Analysis
        uses: aquasecurity/tfsec-action@v1.0.0

      - name: checkov IaC Scan
        uses: bridgecrewio/checkov-action@master
        with:
          directory: .
          framework: terraform

      - name: Terraform Apply (requires approval)
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve tfplan
```

## Drift Detection

### Automated Drift Monitoring

```bash
# Detect drift (compare state to reality)
terraform plan -detailed-exitcode
# Exit code 0: No changes
# Exit code 1: Error
# Exit code 2: Changes detected (drift)

# Refresh state to detect out-of-band changes
terraform refresh
terraform plan
```

### Drift Response Procedure

1. Detect drift via scheduled `terraform plan`
2. Classify: intentional change vs unauthorized modification
3. If unauthorized: investigate as potential security incident
4. If intentional: import into state or update configuration
5. Re-apply to enforce desired state

## Security Scanning Tools

| Tool | Focus | Integration |
|------|-------|-------------|
| tfsec | Static analysis of HCL | CI/CD, pre-commit |
| checkov | Multi-framework IaC scanning | CI/CD, IDE |
| Sentinel | Policy enforcement (HCP Terraform) | Terraform Cloud/Enterprise |
| OPA/Conftest | General policy engine | CI/CD, admission control |
| Terrascan | Compliance scanning | CI/CD |
| KICS | Multi-IaC vulnerability scanner | CI/CD |

## Cross-References

- See `reference/tools/kubernetes-security-reference.md` for K8s IaC security
- See `reference/industries/saas-cloud-security.md` for cloud security posture
- See `frameworks/cloudsec-layer.md` for cloud security methodology
- See `lib/patterns/secrets-management-patterns.md` for secrets handling
- See `checklists/cloud-security-assessment-quality.md` for assessment standards
