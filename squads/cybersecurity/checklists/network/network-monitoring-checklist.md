# Network Monitoring Setup Checklist

## Purpose

Checklist for deploying comprehensive network monitoring including sensor placement, traffic capture strategy, baseline development, and alerting configuration.

## Sensor Placement

### Placement Strategy

| Location | Sensor Type | Purpose | Priority |
|----------|-------------|---------|----------|
| Internet perimeter (outside firewall) | TAP + IDS | Full visibility of inbound threats | Critical |
| Internet perimeter (inside firewall) | TAP + IDS | See what passes firewall | Critical |
| DMZ segments | TAP or SPAN | Monitor exposed services | Critical |
| Core switch/router | NetFlow/sFlow | Internal traffic flow analysis | High |
| Data center interconnects | TAP + IDS/NDR | East-west traffic monitoring | High |
| Server VLANs | TAP or SPAN | Critical asset monitoring | High |
| User segments | NetFlow/sFlow | Endpoint behavior analysis | Medium |
| Cloud VPC | Flow logs + cloud IDS | Cloud workload monitoring | High |
| OT/ICS boundaries | TAP + passive IDS | Industrial network monitoring | Critical (if OT exists) |
| Wireless controller | Mirrored traffic | Wireless traffic analysis | Medium |

### TAP vs SPAN Considerations

| Factor | TAP (Test Access Point) | SPAN (Port Mirror) |
|--------|------------------------|---------------------|
| Reliability | No packet loss | May drop packets under load |
| Performance impact | None on network | Consumes switch resources |
| Full duplex | Separate TX/RX streams | Merged (may lose packets) |
| Fail mode | Network stays up (bypass TAP) | N/A |
| Cost | Hardware purchase | Free (built into switch) |
| Recommended for | Critical segments | Non-critical, temporary |

### Sensor Deployment Checklist

- [ ] Sensor placement plan documented and approved
- [ ] TAPs installed at all critical network boundaries
- [ ] SPAN ports configured where TAPs are not feasible
- [ ] Flow export (NetFlow v9/IPFIX or sFlow) enabled on core devices
- [ ] Sensor capacity verified (throughput matches link speed)
- [ ] Sensor management on dedicated management network
- [ ] Sensor high-availability considered (redundant sensors at critical points)
- [ ] Sensor health monitoring configured
- [ ] Sensor time synchronization verified (NTP, consistent timezone)

## Traffic Capture Strategy

### Capture Scope

| Traffic Type | Capture Method | Detail Level | Retention |
|-------------|---------------|-------------|-----------|
| Full packet | TAP to PCAP storage | Complete packet data | 3-7 days (critical segments) |
| Flow data | NetFlow/IPFIX/sFlow | Metadata (5-tuple, bytes, packets) | 30-90 days |
| DNS queries | DNS tap or log forwarding | Query/response pairs | 90 days |
| HTTP/S metadata | Proxy logs or TLS inspection | URLs, methods, response codes | 90 days |
| TLS metadata | JA3/JA3S fingerprinting | Client/server hello fingerprints | 90 days |
| Email metadata | Mail gateway logs | Sender, recipient, subject, attachments | 90 days |
| Authentication | RADIUS/LDAP/Kerberos logs | Auth events, source, result | 1 year |

### Storage Sizing

```
Full packet capture sizing:
- Average utilization * link speed * retention period
- Example: 40% utilization * 1 Gbps * 86400 sec/day * 7 days
  = 0.4 * 1,000,000,000 * 86,400 * 7 / 8 bytes
  = approximately 30 TB for 7 days at 1 Gbps 40% avg

Flow data sizing:
- Approximately 1/500th to 1/1000th of full packet volume
- Same link: approximately 30-60 GB for 30 days
```

### Capture Configuration

- [ ] Full packet capture deployed at perimeter and critical segments
- [ ] Capture filters exclude high-volume, low-value traffic (if needed for storage)
- [ ] BPF filters documented and reviewed
- [ ] PCAP rotation and retention configured
- [ ] Encrypted PCAP storage with access controls
- [ ] Flow export configured on all core routers/switches
- [ ] Flow export sampling rate documented (1:1 preferred, 1:100 acceptable at scale)
- [ ] DNS query logging enabled on all resolvers
- [ ] Proxy/web gateway logging comprehensive (not summary only)

## Baseline Development

### Network Baseline Components

- [ ] Normal traffic volume by segment/time (hourly, daily, weekly patterns)
- [ ] Normal protocol distribution (HTTP/S, DNS, SMB, etc.)
- [ ] Normal top-talkers (internal hosts by volume)
- [ ] Normal external destinations (top 100 by connection count)
- [ ] Normal port usage patterns
- [ ] Normal DNS query volume and patterns
- [ ] Normal authentication patterns (time, source, volume)
- [ ] Baseline documented and stored for comparison

### Baseline Development Process

| Step | Activity | Duration |
|------|----------|----------|
| 1 | Deploy sensors and begin collection | Week 1 |
| 2 | Initial data quality validation | Week 1-2 |
| 3 | Passive observation and data collection | Weeks 2-6 |
| 4 | Analyze patterns and establish baselines | Week 6-8 |
| 5 | Validate baselines with operations teams | Week 8-9 |
| 6 | Configure anomaly detection thresholds | Week 9-10 |
| 7 | Tune alerts based on initial alerting | Weeks 10-14 |
| 8 | Baseline refinement (ongoing) | Continuous |

## Alerting Configuration

### Alert Categories

| Category | Examples | Severity | Response |
|----------|---------|----------|----------|
| Threat detection | IDS/IPS signature match, malware C2 | High-Critical | SOC investigation |
| Anomaly detection | Traffic volume spike, new protocol, new destination | Medium | SOC triage |
| Policy violation | Unauthorized service, blocked protocol bypass | Medium | SOC triage |
| Availability | Link down, sensor failure, packet loss | High | NOC + SOC |
| Performance | Latency spike, utilization threshold | Low-Medium | NOC |
| Compliance | Unencrypted sensitive data detected | High | Security team |

### Alert Tuning Principles

- [ ] Start with high-confidence alerts only (known-bad indicators)
- [ ] Add anomaly-based alerts gradually after baseline is established
- [ ] Threshold-based alerts use baseline + standard deviation
- [ ] Suppressions documented with justification and review date
- [ ] False positive rate tracked per alert rule
- [ ] Alert volume manageable (SOC can review within SLA)
- [ ] Correlation rules combine multiple low-confidence signals
- [ ] Alert enrichment automated (GeoIP, reputation, CMDB context)

### Specific Alerts to Configure

- [ ] Known malicious IP/domain communication
- [ ] DNS tunneling indicators (high-entropy queries, excessive TXT)
- [ ] Beaconing behavior (regular-interval connections to external hosts)
- [ ] Large data transfers to unusual destinations
- [ ] New external service exposure (new listening ports)
- [ ] SMB/RDP traffic across security zones (lateral movement)
- [ ] ICMP tunneling indicators (large/frequent ICMP packets)
- [ ] Cleartext credential transmission (FTP, Telnet, HTTP auth)
- [ ] Unauthorized DHCP/DNS servers
- [ ] ARP spoofing indicators
- [ ] Network scanning activity (port sweeps, ping sweeps)

## Integration

### SIEM Integration

- [ ] Flow data forwarded to SIEM
- [ ] IDS/IPS alerts forwarded to SIEM
- [ ] DNS query logs forwarded to SIEM
- [ ] Proxy logs forwarded to SIEM
- [ ] NDR alerts forwarded to SIEM
- [ ] Correlation rules combine network and host data
- [ ] Network context enrichment available in SIEM (asset, location, owner)

### Ticketing Integration

- [ ] High-severity network alerts auto-create tickets
- [ ] Alert-to-ticket mapping documented
- [ ] Ticket SLAs aligned with alert severity
- [ ] Feedback loop from ticket resolution to alert tuning

## Operational Requirements

- [ ] Network monitoring tools have dedicated hardware/VM resources
- [ ] Monitoring infrastructure on separate management network
- [ ] Monitoring tool access restricted to authorized security personnel
- [ ] Monitoring tool patching and update process defined
- [ ] Monitoring data backup and retention policy enforced
- [ ] Capacity planning for monitoring infrastructure (growth projection)
- [ ] Runbooks for common network alerts documented
- [ ] Regular monitoring effectiveness review (quarterly)

## Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| Network segment visibility | >95% of critical segments | Monthly |
| Sensor uptime | >99.9% | Monthly |
| Packet loss at sensors | <0.1% | Weekly |
| Alert false positive rate | <20% | Monthly |
| Mean time to detect network anomaly | <15 minutes | Monthly |
| Flow data coverage | 100% of core devices | Monthly |

## Cross-References

- [Network Segmentation Framework](../../frameworks/network-segmentation-framework.md) -- segment definitions
- [Firewall Audit Checklist](firewall-audit-checklist.md) -- firewall logging integration
- [DNS Security Checklist](dns-security-checklist.md) -- DNS monitoring
- [Snort/Suricata Rules](../../swipe/detection/snort-suricata-rules.md) -- IDS rules
