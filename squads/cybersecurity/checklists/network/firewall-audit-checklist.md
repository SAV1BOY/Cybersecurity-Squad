# Firewall Rule Audit Checklist

## Purpose

Checklist for auditing firewall rules covering rule review, optimization, documentation, change management, and validation testing. Applicable to network firewalls, cloud security groups, and host-based firewalls.

## Rule Review

### Rule Inventory

- [ ] Complete rule export obtained from all firewall platforms
- [ ] Total rule count documented per firewall/policy
- [ ] Rules sorted by hit count (identify unused rules)
- [ ] Rules sorted by age (identify stale rules)
- [ ] Each rule has a unique identifier/name
- [ ] Rules without descriptions/comments identified

### Rule Quality Assessment

| Check | Criteria | Verified |
|-------|---------|----------|
| No "any-any-any-permit" rules | No rules allowing all traffic | [ ] |
| No "any" source with "any" destination | Broad rules identified for tightening | [ ] |
| No "any" service/port rules | Port ranges should be specific | [ ] |
| Deny rules before permit rules (where order matters) | Rule order validates intent | [ ] |
| Default deny rule at end of policy | Implicit deny verified | [ ] |
| Logging enabled on deny rules | Dropped traffic is logged | [ ] |
| Logging enabled on high-risk permit rules | Sensitive access logged | [ ] |
| No duplicate rules | Redundant rules removed | [ ] |
| No shadowed rules | Rules not made irrelevant by earlier rules | [ ] |
| No expired temporary rules | Time-limited rules removed after expiry | [ ] |

### Specific Rule Checks

- [ ] No inbound rules allowing direct access to management ports (SSH/22, RDP/3389) from internet
- [ ] No inbound rules allowing database ports (3306, 5432, 1433, 1521) from internet
- [ ] No outbound rules allowing unrestricted egress (should be proxy-enforced)
- [ ] DMZ-to-internal rules are minimal and justified
- [ ] Internal-to-DMZ rules are specific (not broad)
- [ ] Cross-zone rules have documented business justification
- [ ] VPN rules restrict access to authorized resources (not full network)
- [ ] Partner/vendor rules are time-bounded and specific
- [ ] Legacy rules (from decommissioned systems) identified and removed

## Rule Optimization

### Consolidation Opportunities

- [ ] Rules with same source and destination but different ports consolidated
- [ ] Sequential IP ranges consolidated into CIDR blocks
- [ ] Rules using individual IPs converted to group objects where appropriate
- [ ] Overlapping rules identified and simplified
- [ ] Rule groups/sections organized by function (management, application, infrastructure)
- [ ] Object groups/address groups used consistently (no inline IPs in rules)

### Performance Optimization

- [ ] Most-hit rules placed higher in policy (where order-dependent)
- [ ] Disabled rules removed (not just disabled)
- [ ] Empty object groups removed
- [ ] Unused object groups removed
- [ ] Rule count within vendor-recommended limits
- [ ] Policy compilation time within acceptable range

## Documentation

### Rule Documentation Requirements

| Field | Required | Verified |
|-------|----------|----------|
| Rule name/description | Yes | [ ] |
| Business justification | Yes | [ ] |
| Requesting party | Yes | [ ] |
| Approval reference (ticket/CR number) | Yes | [ ] |
| Creation date | Yes | [ ] |
| Review date (next) | Yes | [ ] |
| Expiration date (if temporary) | If applicable | [ ] |
| Owner/responsible team | Yes | [ ] |
| Related application or service | Yes | [ ] |

### Architecture Documentation

- [ ] Firewall topology diagram current and accurate
- [ ] Zone definitions documented
- [ ] Zone trust levels documented
- [ ] Default inter-zone policies documented
- [ ] High-availability configuration documented
- [ ] Failover procedure documented and tested
- [ ] Management access restricted and documented

## Change Management

### Change Process

- [ ] All firewall changes require a change request ticket
- [ ] Change requests include business justification
- [ ] Change requests specify exact rule (source, destination, port, action)
- [ ] Change requests have an approval workflow (requester -> security -> implementation)
- [ ] Emergency change process defined (with post-hoc review requirement)
- [ ] Changes are tested before production deployment
- [ ] Rollback procedure defined for each change
- [ ] Change verification performed after implementation
- [ ] Configuration backup taken before and after changes

### Change Review

- [ ] Quarterly review of all changes made in the period
- [ ] Emergency changes reviewed within 5 business days
- [ ] Temporary rules have expiration dates enforced
- [ ] Reverted changes cleaned up (removed, not just disabled)
- [ ] Change log maintained and auditable

## Testing and Validation

### Rule Validation

- [ ] Critical deny rules tested (verify traffic is blocked)
- [ ] Critical permit rules tested (verify traffic is allowed)
- [ ] Default deny rule tested (verify unknown traffic is blocked)
- [ ] Rules tested after changes (before and after comparison)
- [ ] Cross-zone rules tested from actual source to destination
- [ ] HA failover tested (rules function correctly on standby)

### Security Testing

- [ ] Penetration test validates firewall effectiveness
- [ ] Firewall bypass attempts documented and reviewed
- [ ] Egress filtering validated (can unauthorized protocols exit?)
- [ ] DNS tunneling prevention validated
- [ ] ICMP tunneling prevention validated
- [ ] Split tunneling implications assessed (VPN users)

## Operational Security

### Firewall Platform Security

- [ ] Firewall management interface on dedicated management network
- [ ] Firewall management access requires MFA
- [ ] Firewall admin accounts are individual (no shared accounts)
- [ ] Firewall admin activity logged to external syslog/SIEM
- [ ] Firewall OS/firmware current and patched
- [ ] Default credentials changed
- [ ] Unused interfaces administratively disabled
- [ ] SNMP v3 used (v1/v2c disabled)
- [ ] NTP configured and synchronized
- [ ] Configuration backups automated and encrypted

### Monitoring

- [ ] Firewall health monitored (CPU, memory, connections, throughput)
- [ ] Alert on firewall failover events
- [ ] Alert on admin login events
- [ ] Alert on configuration changes
- [ ] Alert on policy violations (denied traffic spikes)
- [ ] Log storage capacity sufficient for retention period
- [ ] Logs forwarded to SIEM in real-time

## Audit Metrics

| Metric | Target | Measured |
|--------|--------|---------|
| Rules with documentation | 100% | [ ] |
| Rules with hit count = 0 (30 days) | 0 (remove unused) | [ ] |
| Rules older than 1 year without review | 0 | [ ] |
| "Any" source or destination rules | 0 (or documented exceptions) | [ ] |
| Temporary rules past expiration | 0 | [ ] |
| Changes without change request | 0 | [ ] |
| Average rule review age | < 12 months | [ ] |

## Cross-References

- [Network Segmentation Framework](../../frameworks/network-segmentation-framework.md) -- segmentation strategy
- [Network Monitoring Checklist](network-monitoring-checklist.md) -- monitoring setup
- [VPN Security Checklist](vpn-security-checklist.md) -- VPN-related firewall rules
- [Snort/Suricata Rules](../../swipe/detection/snort-suricata-rules.md) -- IDS/IPS integration
