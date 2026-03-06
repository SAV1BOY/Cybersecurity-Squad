# Splunk for Security Reference

## Purpose

Operational reference for Splunk as a security operations platform. Covers SPL query patterns for threat detection, notable event management, risk-based alerting, CIM data model usage, and threat intelligence integration for SOC analysts and detection engineers.

## SPL (Search Processing Language) Essentials

### Search Structure

```
index=main sourcetype=syslog host=webserver01
| where status >= 400
| stats count by src_ip, status
| sort -count
| head 20
```

### Core Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `search` | Filter events | `search index=security EventCode=4625` |
| `where` | Conditional filter | `where count > 10` |
| `stats` | Aggregation | `stats count, dc(dest) by src_ip` |
| `timechart` | Time-series | `timechart span=1h count by action` |
| `eval` | Calculate fields | `eval mb=bytes/1024/1024` |
| `rex` | Regex extraction | `rex field=_raw "user=(?<username>\w+)"` |
| `lookup` | Enrich with lookup | `lookup threat_intel ip AS src_ip` |
| `transaction` | Group related events | `transaction src_ip maxspan=5m` |
| `tstats` | Accelerated data model search | `tstats count from datamodel=Authentication` |
| `dedup` | Remove duplicates | `dedup src_ip dest_ip` |
| `table` | Select columns | `table _time src_ip dest_ip action` |
| `rename` | Rename fields | `rename src_ip AS "Source IP"` |

## Security-Focused SPL Queries

### Authentication Monitoring

```spl
// Brute force detection
index=security sourcetype=WinEventLog EventCode=4625
| stats count dc(TargetUserName) AS unique_users values(TargetUserName) by src_ip
| where count > 20 OR unique_users > 5

// Successful login after failures (credential stuffing indicator)
index=security sourcetype=WinEventLog (EventCode=4625 OR EventCode=4624)
| stats count(eval(EventCode=4625)) AS failures count(eval(EventCode=4624)) AS successes by TargetUserName, src_ip
| where failures > 10 AND successes > 0

// Off-hours authentication
index=security sourcetype=WinEventLog EventCode=4624
| eval hour=strftime(_time, "%H")
| where hour < 6 OR hour > 22
| stats count by TargetUserName, src_ip, hour

// Impossible travel
index=security EventCode=4624
| iplocation src_ip
| stats earliest(_time) AS first latest(_time) AS last values(City) AS cities dc(City) AS city_count by TargetUserName
| where city_count > 1
| eval time_diff=last-first
| where time_diff < 3600
```

### Lateral Movement Detection

```spl
// PsExec-style service installation
index=security EventCode=7045 ServiceType="user mode service"
| regex ServiceFileName="(?i)(psexec|cmd|powershell|mshta)"

// Pass-the-Hash indicators
index=security EventCode=4624 LogonType=3 AuthenticationPackageName=NTLM
| stats count by TargetUserName, src_ip, dest
| where count > 5

// RDP lateral movement mapping
index=security EventCode=4624 LogonType=10
| stats count values(src_ip) AS sources by TargetUserName, dest
| where count > 3
```

### Exfiltration Detection

```spl
// Large outbound data transfers
index=network dest_port=443
| stats sum(bytes_out) AS total_bytes by src_ip, dest_ip
| eval total_mb=round(total_bytes/1024/1024, 2)
| where total_mb > 500
| sort -total_mb

// DNS tunneling indicators
index=dns
| eval query_len=len(query)
| where query_len > 50
| stats count avg(query_len) AS avg_len by src_ip
| where count > 100 AND avg_len > 40

// Beaconing detection
index=network
| bin _time span=60s
| stats count by _time, src_ip, dest_ip
| streamstats window=10 stdev(count) AS jitter avg(count) AS avg by src_ip, dest_ip
| where jitter < 2 AND avg > 0
```

## CIM (Common Information Model)

### Key Data Models

| Data Model | Fields | Use Case |
|------------|--------|----------|
| Authentication | action, user, src, dest, app | Login/logout analysis |
| Network Traffic | src_ip, dest_ip, bytes, action | Flow analysis |
| Web | url, http_method, status, dest | Web proxy/WAF logs |
| Endpoint | process_name, parent_process, user | Process execution |
| Malware | signature, action, file_name | AV/EDR alerts |
| Intrusion Detection | signature, severity, src, dest | IDS/IPS alerts |
| Change | object, action, user, result | Change auditing |

### Accelerated Searches with tstats

```spl
// Fast authentication analysis using data model
| tstats count from datamodel=Authentication where Authentication.action=failure
  by Authentication.user Authentication.src _time span=1h
| rename Authentication.* AS *
| where count > 20

// Network traffic summary
| tstats sum(All_Traffic.bytes) AS bytes from datamodel=Network_Traffic
  by All_Traffic.src_ip All_Traffic.dest_ip
| rename All_Traffic.* AS *
| where bytes > 1073741824
```

## Risk-Based Alerting (RBA)

### Concept

Instead of alerting on individual events, accumulate risk scores on entities (users, hosts). Alert only when cumulative risk exceeds threshold.

### Implementation Pattern

```spl
// Risk rule: suspicious process execution
index=endpoint process_name IN ("certutil.exe","bitsadmin.exe","mshta.exe")
| eval risk_score=case(
    process_name="certutil.exe", 25,
    process_name="bitsadmin.exe", 20,
    process_name="mshta.exe", 30
  )
| eval risk_object=user
| eval risk_object_type="user"
| eval risk_message="Suspicious LOLBin execution: ".process_name
| collect index=risk

// Risk threshold alert
index=risk
| stats sum(risk_score) AS total_risk values(risk_message) AS risk_events by risk_object
| where total_risk > 100
```

## Threat Intelligence Integration

```spl
// Lookup against threat intel
index=network
| lookup threat_intel_ip ip AS dest_ip OUTPUT threat_category, confidence
| where isnotnull(threat_category)
| stats count values(threat_category) by src_ip, dest_ip

// IOC sweep across historical data
index=* (dest_ip IN ("1.2.3.4","5.6.7.8") OR url="*malicious-domain.com*" OR
  file_hash IN ("abc123","def456"))
| stats count earliest(_time) AS first_seen latest(_time) AS last_seen by index, sourcetype, src_ip
```

## Notable Events and Investigation

```spl
// Create notable event (Enterprise Security)
| sendalert notable param.security_domain="threat"
  param.severity="high"
  param.rule_title="Credential Stuffing Detected"
  param.rule_description="Multiple failed logins followed by success from $src_ip$"

// Investigation dashboard search
index=security src_ip="$suspect_ip$"
| stats count by sourcetype, EventCode, action
| sort -count
```

## Cross-References

- See `frameworks/defense-layer.md` for detection strategy integration
- See `frameworks/detection-coverage-matrix.md` for MITRE ATT&CK mapping
- See `data/registries/detection-rules-registry.md` for rule management
- See `data/registries/windows-event-ids-registry.md` for Windows event correlation
- See `workflows/detection-engineering-workflow.md` for detection development lifecycle
