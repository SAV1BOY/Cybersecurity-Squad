# Splunk SPL Hunting Queries

## Purpose

Splunk Search Processing Language (SPL) queries for threat hunting covering process chains, network beaconing, DNS anomalies, credential abuse, and lateral movement. Optimized for performance in large-scale environments.

## Process Chain Analysis

### Query 1: Suspicious Process Spawning from Office Applications

```spl
index=sysmon sourcetype=sysmon EventCode=1
(ParentImage="*\\WINWORD.EXE" OR ParentImage="*\\EXCEL.EXE"
 OR ParentImage="*\\POWERPNT.EXE" OR ParentImage="*\\OUTLOOK.EXE"
 OR ParentImage="*\\MSACCESS.EXE")
(Image="*\\cmd.exe" OR Image="*\\powershell.exe" OR Image="*\\wscript.exe"
 OR Image="*\\cscript.exe" OR Image="*\\mshta.exe" OR Image="*\\regsvr32.exe"
 OR Image="*\\rundll32.exe" OR Image="*\\certutil.exe"
 OR Image="*\\bitsadmin.exe" OR Image="*\\schtasks.exe")
| eval suspicion_score=case(
    like(CommandLine, "%encodedcommand%"), 10,
    like(CommandLine, "%bypass%"), 8,
    like(CommandLine, "%hidden%"), 8,
    like(CommandLine, "%downloadstring%"), 9,
    like(CommandLine, "%invoke-webrequest%"), 9,
    like(CommandLine, "%Net.WebClient%"), 9,
    like(CommandLine, "%-enc %"), 10,
    1=1, 5)
| table _time, host, User, ParentImage, Image, CommandLine, suspicion_score
| sort - suspicion_score

``` Tuning Notes:
| - Filter known macros that legitimately spawn processes
| - Score-based approach reduces false positive fatigue
| - Correlate with file creation events for dropped payloads
| - OUTLOOK.EXE spawning processes may indicate preview pane exploitation
```

### Query 2: Living-off-the-Land Binary (LOLBin) Execution

```spl
index=sysmon sourcetype=sysmon EventCode=1
(Image="*\\certutil.exe" AND (CommandLine="*-urlcache*" OR CommandLine="*-decode*" OR CommandLine="*-encode*"))
OR (Image="*\\mshta.exe" AND CommandLine="*http*")
OR (Image="*\\regsvr32.exe" AND CommandLine="*/s /n /u /i:http*")
OR (Image="*\\rundll32.exe" AND CommandLine="*javascript*")
OR (Image="*\\bitsadmin.exe" AND CommandLine="*/transfer*")
OR (Image="*\\msiexec.exe" AND CommandLine="*http*")
OR (Image="*\\wmic.exe" AND CommandLine="*process call create*")
OR (Image="*\\cmstp.exe" AND CommandLine="*/ni*" AND CommandLine="*/s*")
OR (Image="*\\msxsl.exe")
OR (Image="*\\xwizard.exe" AND CommandLine="*RunWizard*")
| eval technique=case(
    like(Image, "%certutil%"), "T1140/T1105 - Deobfuscation/Ingress Tool Transfer",
    like(Image, "%mshta%"), "T1218.005 - Mshta",
    like(Image, "%regsvr32%"), "T1218.010 - Regsvr32",
    like(Image, "%rundll32%"), "T1218.011 - Rundll32",
    like(Image, "%bitsadmin%"), "T1197 - BITS Jobs",
    like(Image, "%msiexec%"), "T1218.007 - Msiexec",
    like(Image, "%wmic%"), "T1047 - WMI",
    like(Image, "%cmstp%"), "T1218.003 - CMSTP",
    1=1, "LOLBin")
| table _time, host, User, ParentImage, Image, CommandLine, technique
| sort - _time

``` Tuning Notes:
| - certutil -urlcache is the most common LOLBin for download
| - Filter IT admin workstations that legitimately use these tools
| - Parent process context is critical for reducing FPs
| - mshta with HTTP URLs is almost always malicious
```

## Network Beaconing Detection

### Query 3: C2 Beaconing Detection via Timing Analysis

```spl
index=firewall sourcetype=pan:traffic action=allowed
dest_port IN (80, 443, 8080, 8443)
| bin _time span=10m
| stats count as connections,
        dc(src_ip) as unique_sources,
        values(src_ip) as sources
        by dest_ip, dest_port, _time
| streamstats count as interval_count,
              avg(connections) as avg_connections,
              stdev(connections) as stdev_connections
              by dest_ip, dest_port
| where interval_count > 12  | comment("At least 2 hours of data")
| where stdev_connections < (avg_connections * 0.3)  | comment("Low variance = regular interval")
| where avg_connections < 5  | comment("Low volume per interval = beacon, not bulk traffic")
| stats latest(_time) as last_seen,
        earliest(_time) as first_seen,
        avg(avg_connections) as avg_conn_per_interval,
        avg(stdev_connections) as consistency_score,
        values(sources) as beacon_sources
        by dest_ip, dest_port
| where consistency_score < 1.5
| sort + consistency_score
| table dest_ip, dest_port, first_seen, last_seen,
        avg_conn_per_interval, consistency_score, beacon_sources

``` Tuning Notes:
| - Low stdev relative to mean indicates regular timing (beacon behavior)
| - Filter known CDN, update services, and monitoring endpoints
| - Tune span and thresholds based on expected beacon intervals
| - Cross-reference dest_ip with threat intelligence
| - JA3/JA3S hash analysis adds confidence for TLS beacons
```

### Query 4: Long-Duration Connections (Potential Tunnel)

```spl
index=firewall sourcetype=pan:traffic action=allowed
| eval duration_minutes = duration / 60
| where duration_minutes > 60
| where dest_port IN (80, 443, 53, 8080)
| where NOT (dest_ip IN ("known.update.server", "known.vpn.endpoint"))
| stats count as session_count,
        avg(duration_minutes) as avg_duration,
        max(duration_minutes) as max_duration,
        sum(bytes_sent) as total_bytes_sent,
        sum(bytes_received) as total_bytes_received
        by src_ip, dest_ip, dest_port
| where session_count > 3
| eval bytes_ratio = total_bytes_sent / (total_bytes_received + 1)
| where bytes_ratio > 0.8 OR bytes_ratio < 0.01  | comment("Near-equal or very asymmetric")
| sort - max_duration
| table src_ip, dest_ip, dest_port, session_count,
        avg_duration, max_duration,
        total_bytes_sent, total_bytes_received, bytes_ratio

``` Tuning Notes:
| - DNS over port 53 with long duration = likely DNS tunnel
| - Near-equal send/receive ratio may indicate interactive session
| - Very low send ratio may indicate data exfiltration
| - Filter legitimate long-lived connections (WebSocket, streaming)
```

## DNS Anomaly Detection

### Query 5: High-Entropy DNS Queries (DGA Detection)

```spl
index=dns sourcetype=dns
| rex field=query "(?<subdomain>[^\.]+)\.(?<domain>[^\.]+\.[^\.]+)$"
| eval subdomain_length = len(subdomain)
| where subdomain_length > 12
| eval char_set = mvjoin(mvmap(split(subdomain, ""), if(match(mvindex(split(subdomain,""),0), "[a-z]"), "a", if(match(mvindex(split(subdomain,""),0), "[0-9]"), "n", "s"))), "")
| eval consonant_ratio = (subdomain_length - len(replace(subdomain, "[aeiou]", ""))) / subdomain_length
| eval digit_ratio = len(replace(subdomain, "[^0-9]", "")) / subdomain_length
| where consonant_ratio > 0.7 OR digit_ratio > 0.3 OR subdomain_length > 24
| stats count as query_count,
        dc(subdomain) as unique_subdomains,
        dc(src_ip) as unique_sources,
        values(src_ip) as sources,
        avg(subdomain_length) as avg_length
        by domain
| where unique_subdomains > 20 OR query_count > 50
| sort - unique_subdomains
| table domain, query_count, unique_subdomains,
        avg_length, unique_sources, sources

``` Tuning Notes:
| - Allowlist CDN domains (*.akamaiedge.net, *.cloudfront.net)
| - High consonant ratio + high unique subdomains = strong DGA indicator
| - Cross-reference domain age (newly registered domains)
| - TXT query types with base64 content are C2 indicators
```

### Query 6: DNS Query to Newly Registered Domain

```spl
index=dns sourcetype=dns query_type IN ("A", "AAAA", "CNAME")
| rex field=query "(?<domain>[^\.]+\.[^\.]+)$"
| lookup domain_age_lookup domain OUTPUT registration_date, age_days
| where age_days < 30
| stats count as query_count,
        dc(src_ip) as unique_clients,
        values(src_ip) as client_ips,
        earliest(_time) as first_query,
        latest(_time) as last_query
        by domain, age_days
| where query_count > 5
| sort + age_days
| table domain, age_days, query_count, unique_clients,
        client_ips, first_query, last_query

``` Tuning Notes:
| - Requires domain_age_lookup enrichment (WHOIS data feed)
| - Alternative: Use threat intelligence feed with domain age
| - Newly registered domains used by single client are more suspicious
| - Correlate with process creation for the querying application
```

## Credential Access Detection

### Query 7: Kerberoasting Detection

```spl
index=wineventlog sourcetype=WinEventLog:Security EventCode=4769
Ticket_Encryption_Type=0x17  | comment("RC4 encryption = legacy, used in Kerberoasting")
Service_Name!="krbtgt"
Service_Name!="*$"  | comment("Exclude machine accounts")
| where NOT match(Service_Name, "^(CIFS|HTTP|LDAP|DNS|HOST|RestrictedKrbHost|MSOMSdksvc)")
| stats count as request_count,
        dc(Service_Name) as unique_services,
        values(Service_Name) as targeted_services,
        values(Client_Address) as source_ips
        by Account_Name
| where unique_services > 3  | comment("Multiple service tickets = likely Kerberoasting")
| sort - unique_services
| table Account_Name, unique_services, request_count,
        targeted_services, source_ips

``` Tuning Notes:
| - RC4 (0x17) is the key indicator -- AES requests (0x12) are normal
| - Single user requesting many service tickets in short time = Kerberoasting
| - Filter known service accounts that legitimately request multiple tickets
| - Correlate with T1558.003 in ATT&CK
| - Consider enforcing AES-only for service accounts to prevent this attack
```

### Query 8: Credential Dumping via Suspicious Process Access

```spl
index=sysmon sourcetype=sysmon EventCode=10
TargetImage="*\\lsass.exe"
NOT SourceImage IN ("*\\MsMpEng.exe", "*\\csrss.exe", "*\\svchost.exe",
                     "*\\lsass.exe", "*\\services.exe", "*\\winlogon.exe",
                     "*\\taskmgr.exe")
NOT SourceImage="C:\\Program Files\\*"
NOT SourceImage="C:\\Program Files (x86)\\*"
| eval access_type=case(
    GrantedAccess="0x1fffff", "PROCESS_ALL_ACCESS (critical)",
    GrantedAccess="0x1010", "PROCESS_QUERY_LIMITED+VM_READ (suspicious)",
    GrantedAccess="0x1410", "PROCESS_QUERY+VM_READ (suspicious)",
    GrantedAccess="0x143a", "Multiple access rights (suspicious)",
    1=1, "Other: ".GrantedAccess)
| table _time, host, SourceImage, SourceUser, TargetImage,
        GrantedAccess, access_type, CallTrace
| sort - _time

``` Tuning Notes:
| - Add your EDR/AV process paths to the NOT SourceImage filter
| - PROCESS_ALL_ACCESS to LSASS is almost always malicious
| - CallTrace field shows the DLL call stack -- look for unknown DLLs
| - Correlate with Sysmon EventCode=7 (image loaded) for injected DLLs
```

## SPL Performance Best Practices

| Technique | Impact | Example |
|-----------|--------|---------|
| Specify index and sourcetype | Critical | `index=sysmon sourcetype=sysmon` |
| Time range at search level | Critical | Use time picker, not `where _time >` |
| Filter early in pipeline | Major | Put restrictive `where` clauses first |
| Use `tstats` for indexed fields | Major | `| tstats count where index=sysmon by host` |
| `stats` over `transaction` | Major | `stats` is far more efficient |
| Avoid wildcards at start | Moderate | `Image="*\\cmd.exe"` over `Image="*cmd*"` |
| `fields` command | Moderate | Limit fields early in pipeline |
| Accelerated data models | Major | Use data model searches where available |

## Cross-References

- [Sigma Rule Examples](sigma-rule-examples.md) -- platform-agnostic rules
- [KQL Hunting Queries](kql-hunting-queries.md) -- Microsoft Sentinel equivalent
- [Snort/Suricata Rules](snort-suricata-rules.md) -- network-level detection
- [Detection Engineering Workflow](../../workflows/detection-engineering-workflow.md) -- rule lifecycle
