# Network Segmentation Framework

## Purpose

Define a comprehensive network segmentation strategy that limits lateral movement, contains breaches, and enforces least-privilege network access. Covers macro-segmentation (zones/VLANs) through micro-segmentation (workload-level).

## Segmentation Architecture

### Zone Model

| Zone | Trust Level | Purpose | Examples |
|------|------------|---------|----------|
| Untrusted (Red) | 0 | Internet, external networks | Public internet, partner extranets |
| DMZ (Orange) | 1 | Internet-facing services | Web servers, reverse proxies, API gateways |
| General (Yellow) | 2 | Standard business operations | Workstations, printers, general servers |
| Restricted (Green) | 3 | Sensitive business systems | HR systems, finance, ERP |
| Secure (Blue) | 4 | Critical infrastructure | Domain controllers, PKI, SIEM, backup |
| Highly Secure (Purple) | 5 | Most sensitive assets | Payment processing, crypto key stores, OT/SCADA |

### Zone Communication Rules

| Source Zone | Destination Zone | Default Policy | Required Controls |
|------------|-----------------|---------------|-------------------|
| Untrusted -> DMZ | Allow (specific ports) | WAF, IPS, rate limiting |
| Untrusted -> Any other | Deny | N/A |
| DMZ -> General | Deny (exceptions via proxy) | Application proxy, inspection |
| DMZ -> Restricted+ | Deny | N/A |
| General -> DMZ | Allow (specific) | Firewall ACL |
| General -> Restricted | Allow (authorized users/services) | Firewall + identity-based policy |
| General -> Secure | Deny (exceptions with PAM) | PAM, MFA, session recording |
| Restricted -> Secure | Allow (specific services) | Firewall, mutual TLS |
| Any -> Highly Secure | Deny (exceptions with jump host) | Jump host, PAM, MFA, full logging |

## Conduit Design

### Conduit Definition
A conduit is a controlled communication path between zones that specifies:
- Source and destination zones
- Allowed protocols and ports
- Authentication requirements
- Inspection requirements
- Logging requirements

### Conduit Template

```
Conduit: [Name]
Source Zone: [Zone]
Destination Zone: [Zone]
Direction: [Unidirectional/Bidirectional]
Protocols: [TCP/UDP ports, application protocols]
Authentication: [None/Certificate/Token/MFA]
Inspection: [None/IPS/DPI/WAF]
Encryption: [None/TLS/IPSec]
Logging: [None/Metadata/Full]
Business Justification: [Why this conduit exists]
Owner: [Team/Individual]
Review Date: [Next review]
```

## Micro-Segmentation

### Implementation Approaches

| Approach | Mechanism | Granularity | Use Case |
|----------|-----------|-------------|----------|
| Host-based firewall | OS firewall (iptables, Windows Firewall) | Per-host | Server workloads |
| Agent-based | Microseg agent (Illumio, Guardicore) | Per-workload | Data center |
| SDN-based | NSX, ACI, Calico | Per-workload/container | Virtualized/containerized |
| Cloud-native | Security groups, NACLs | Per-instance/ENI | Cloud workloads |
| Identity-based | Zero trust proxy (Zscaler, BeyondCorp) | Per-user-per-app | User access |

### Micro-Segmentation Policy Design

1. **Discover** -- Map all communication flows (netflow, agent telemetry)
2. **Baseline** -- Establish normal communication patterns (30-60 days)
3. **Label** -- Tag workloads by application, environment, data classification
4. **Policy** -- Define allow rules based on labels (deny-by-default)
5. **Test** -- Enforce in monitor/alert mode before blocking
6. **Enforce** -- Enable blocking, monitor for breakage
7. **Maintain** -- Continuous policy review and updates

### Label Taxonomy Example

```
Application: payment-service
Environment: production
Data Classification: restricted
Business Unit: finance
Compliance Scope: pci-dss
Tier: backend
```

## Policy Enforcement Points

| Enforcement Point | Function | Placement |
|-------------------|----------|-----------|
| Perimeter firewall | Zone-to-zone filtering | Zone boundaries |
| Internal firewall | Intra-zone filtering | Between subnets |
| Web Application Firewall | L7 inspection for web traffic | In front of web applications |
| Network IPS/IDS | Threat detection and prevention | Zone conduits |
| Proxy/API Gateway | Protocol-aware access control | Application entry points |
| Host firewall | Workload-level filtering | On each host |
| Cloud security groups | Instance-level filtering | Cloud workloads |
| Service mesh | Service-to-service control | Kubernetes/microservices |

## Monitoring Requirements

### Per-Segment Monitoring

| Data Source | Purpose | Retention |
|-------------|---------|-----------|
| Firewall logs | Policy enforcement verification | 90 days (1 year for compliance) |
| Flow data (NetFlow/sFlow) | Communication pattern analysis | 30-90 days |
| IDS/IPS alerts | Threat detection at boundaries | 1 year |
| DNS logs | Service resolution and anomaly detection | 90 days |
| Authentication logs | Identity-based access verification | 1 year |
| Micro-seg agent telemetry | Workload communication verification | 90 days |

### Key Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Unauthorized cross-zone traffic | 0 events | Firewall deny logs |
| Policy violation alerts | Decreasing trend | Micro-seg alerts |
| Segmentation coverage | >95% of critical assets | Assets behind policy / total |
| Mean time to contain (lateral) | < 15 minutes | IR metrics |
| Policy review completion | 100% quarterly | Review tracking |

## Validation

- Run periodic lateral movement tests from each zone
- Validate deny rules with controlled traffic generation
- Red team exercises targeting cross-zone movement
- Automated compliance scanning against segmentation policy
- Network path analysis for policy drift detection

## Cross-References

- [Firewall Audit Checklist](../checklists/network/firewall-audit-checklist.md) -- firewall rule review
- [Network Monitoring Checklist](../checklists/network/network-monitoring-checklist.md) -- monitoring setup
- [VPN Security Checklist](../checklists/network/vpn-security-checklist.md) -- remote access segmentation
- [Lateral Movement Methodology](lateral-movement-methodology.md) -- adversary perspective
