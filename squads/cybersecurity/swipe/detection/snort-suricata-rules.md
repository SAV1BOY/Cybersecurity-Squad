# Snort / Suricata Network IDS Rules

## Purpose

Network intrusion detection rules for protocol anomalies, exploit signatures, and command-and-control traffic patterns. Compatible with both Snort 3 and Suricata rule syntax.

## Rule Structure Reference

```
action protocol src_ip src_port -> dst_ip dst_port (options;)

Key Options:
  msg:"Description"           - Alert message
  content:"string"            - Content match (case-sensitive)
  nocase;                     - Case-insensitive content match
  flow:established,to_server  - Flow direction
  sid:N                       - Signature ID
  rev:N                       - Revision number
  classtype:type              - Classification
  reference:url,ref           - External reference
  metadata:key value          - Metadata tags
```

## Protocol Anomaly Rules

### Rule 1: HTTP Tunneling over Non-Standard Port

```
# Detect HTTP traffic on non-standard ports (potential tunneling/C2)
alert tcp $HOME_NET any -> $EXTERNAL_NET !$HTTP_PORTS (
    msg:"POLICY HTTP traffic on non-standard port - possible tunneling";
    flow:established,to_server;
    content:"GET "; depth:4;
    content:"HTTP/1"; distance:0;
    content:"Host:"; nocase;
    threshold:type limit, track by_src, count 1, seconds 300;
    classtype:policy-violation;
    sid:3000001; rev:2;
    metadata:attack_target Client_Endpoint, mitre_tactic Command_And_Control, mitre_technique T1071;
)

alert tcp $HOME_NET any -> $EXTERNAL_NET !$HTTP_PORTS (
    msg:"POLICY HTTP POST on non-standard port - possible data exfiltration";
    flow:established,to_server;
    content:"POST "; depth:5;
    content:"HTTP/1"; distance:0;
    content:"Content-Length:"; nocase;
    threshold:type limit, track by_src, count 1, seconds 300;
    classtype:policy-violation;
    sid:3000002; rev:2;
    metadata:mitre_tactic Exfiltration, mitre_technique T1048;
)
```

**Tuning Notes:**
- Define $HTTP_PORTS to include all legitimate HTTP ports (80, 8080, 8443, etc.)
- High-volume environments may need higher threshold values
- Correlate with proxy logs for full URL context
- Alternative ports for web apps should be added to $HTTP_PORTS

### Rule 2: DNS over HTTPS (DoH) to External Resolvers

```
# Detect DNS-over-HTTPS to known public DoH resolvers
# Bypasses organizational DNS monitoring

alert tls $HOME_NET any -> $EXTERNAL_NET 443 (
    msg:"POLICY DNS-over-HTTPS to Google DNS detected";
    flow:established,to_server;
    tls.sni; content:"dns.google"; nocase;
    classtype:policy-violation;
    sid:3000010; rev:1;
    metadata:mitre_technique T1071.004;
)

alert tls $HOME_NET any -> $EXTERNAL_NET 443 (
    msg:"POLICY DNS-over-HTTPS to Cloudflare DNS detected";
    flow:established,to_server;
    tls.sni; content:"cloudflare-dns.com"; nocase;
    classtype:policy-violation;
    sid:3000011; rev:1;
    metadata:mitre_technique T1071.004;
)

alert tls $HOME_NET any -> $EXTERNAL_NET 443 (
    msg:"POLICY DNS-over-HTTPS to Quad9 DNS detected";
    flow:established,to_server;
    tls.sni; content:"dns.quad9.net"; nocase;
    classtype:policy-violation;
    sid:3000012; rev:1;
    metadata:mitre_technique T1071.004;
)
```

**Tuning Notes:**
- Requires TLS inspection or SNI-based matching (Suricata tls.sni keyword)
- Legitimate use exists; alert rather than block initially
- Add all known DoH providers to detection
- Consider blocking DoH at DNS/firewall level instead of alerting

### Rule 3: SMB Traffic to Internet (Anomalous)

```
# SMB traffic should never traverse to the internet
# Indicates misconfiguration or exploitation attempt

alert tcp $HOME_NET any -> $EXTERNAL_NET 445 (
    msg:"ATTACK Outbound SMB to Internet - possible exploitation or misconfiguration";
    flow:established,to_server;
    content:"|ff|SMB"; depth:4; offset:4;
    classtype:bad-unknown;
    sid:3000020; rev:1;
    metadata:mitre_tactic Lateral_Movement, mitre_technique T1021.002;
)

alert tcp $HOME_NET any -> $EXTERNAL_NET 139 (
    msg:"ATTACK Outbound NetBIOS to Internet";
    flow:established,to_server;
    classtype:bad-unknown;
    sid:3000021; rev:1;
)
```

## Exploit Signature Rules

### Rule 4: Log4Shell Exploitation Attempt (CVE-2021-44228)

```
# Detect Log4Shell JNDI injection attempts in HTTP traffic
# Covers common obfuscation patterns

alert http any any -> $HOME_NET any (
    msg:"EXPLOIT Log4Shell JNDI Injection Attempt (${jndi:ldap)";
    flow:established,to_server;
    content:"${jndi:"; nocase;
    content:"ldap"; nocase; distance:0; within:10;
    classtype:attempted-admin;
    sid:3000030; rev:3;
    reference:cve,2021-44228;
    metadata:mitre_technique T1190, severity critical;
)

alert http any any -> $HOME_NET any (
    msg:"EXPLOIT Log4Shell JNDI Injection Attempt (obfuscated)";
    flow:established,to_server;
    content:"${"; nocase;
    content:"jndi"; nocase; distance:0; within:20;
    pcre:"/\$\{[^\}]*j[^\}]*n[^\}]*d[^\}]*i[^\}]*:/i";
    classtype:attempted-admin;
    sid:3000031; rev:2;
    reference:cve,2021-44228;
    metadata:mitre_technique T1190, severity critical;
)

# Log4Shell via User-Agent header
alert http any any -> $HOME_NET any (
    msg:"EXPLOIT Log4Shell in User-Agent header";
    flow:established,to_server;
    http.user_agent; content:"${jndi:"; nocase;
    classtype:attempted-admin;
    sid:3000032; rev:1;
    reference:cve,2021-44228;
    metadata:mitre_technique T1190, severity critical;
)
```

**Tuning Notes:**
- PCRE-based rule catches obfuscation (${${lower:j}ndi:...})
- Check all HTTP headers, not just URI and body
- Performance impact of PCRE is moderate; use content pre-filter
- Still relevant as Log4j remains widely deployed

### Rule 5: ProxyShell/ProxyNotShell Exchange Exploitation

```
# Detect ProxyShell exploitation attempts against Exchange

alert http any any -> $HOME_NET $HTTP_PORTS (
    msg:"EXPLOIT ProxyShell - Autodiscover SSRF Attempt";
    flow:established,to_server;
    content:"/autodiscover/autodiscover.json"; nocase; http_uri;
    content:"@"; http_uri;
    content:"/mapi/"; nocase; http_uri;
    classtype:attempted-admin;
    sid:3000040; rev:2;
    reference:cve,2021-34473;
    metadata:mitre_technique T1190, severity critical;
)

alert http any any -> $HOME_NET $HTTP_PORTS (
    msg:"EXPLOIT ProxyNotShell - Exchange SSRF via Autodiscover";
    flow:established,to_server;
    content:"/autodiscover/autodiscover.json"; nocase; http_uri;
    content:"Email=autodiscover/autodiscover.json"; nocase; http_uri;
    classtype:attempted-admin;
    sid:3000041; rev:1;
    reference:cve,2022-41040;
    metadata:mitre_technique T1190, severity critical;
)
```

## Command and Control Detection

### Rule 6: Cobalt Strike Default HTTP C2 Patterns

```
# Detect default Cobalt Strike malleable C2 HTTP patterns
# Note: Custom profiles will evade these; they catch defaults

alert http $HOME_NET any -> $EXTERNAL_NET any (
    msg:"C2 Cobalt Strike default beacon checksum URI";
    flow:established,to_server;
    content:"GET"; http_method;
    pcre:"/^\/[a-zA-Z0-9]{4}$/U";
    content:!"Referer:"; nocase;
    content:!"Accept-Language:"; nocase;
    threshold:type both, track by_src, count 5, seconds 600;
    classtype:trojan-activity;
    sid:3000050; rev:2;
    metadata:mitre_tactic Command_And_Control, mitre_technique T1071.001;
)

alert http $HOME_NET any -> $EXTERNAL_NET any (
    msg:"C2 Cobalt Strike default POST beacon";
    flow:established,to_server;
    content:"POST"; http_method;
    content:"/submit.php"; http_uri;
    content:"Content-Type: application/octet-stream"; nocase;
    classtype:trojan-activity;
    sid:3000051; rev:1;
    metadata:mitre_tactic Command_And_Control;
)

# Cobalt Strike DNS beacon
alert dns $HOME_NET any -> any 53 (
    msg:"C2 Cobalt Strike DNS beacon - suspicious subdomain pattern";
    content:"|01|"; offset:2; depth:1;  # Standard query
    pcre:"/^.{12}(.{32,})\./";  # Very long subdomain label
    threshold:type both, track by_src, count 10, seconds 60;
    classtype:trojan-activity;
    sid:3000052; rev:1;
    metadata:mitre_technique T1071.004;
)
```

**Tuning Notes:**
- Default CS profiles are easily changed; these rules catch lazy operators
- JA3/JA3S fingerprinting is more reliable for TLS-based CS
- DNS beacon rule may fire on CDN traffic; tune threshold
- Combine with IP/domain reputation for higher confidence

### Rule 7: Reverse Shell Detection

```
# Detect common reverse shell patterns

alert tcp $HOME_NET any -> $EXTERNAL_NET any (
    msg:"ATTACK Potential reverse shell - /bin/sh or /bin/bash in TCP stream";
    flow:established;
    content:"/bin/sh"; nocase;
    classtype:trojan-activity;
    sid:3000060; rev:1;
    metadata:mitre_technique T1059.004;
)

alert tcp $HOME_NET any -> $EXTERNAL_NET any (
    msg:"ATTACK Potential PowerShell reverse shell";
    flow:established,to_server;
    content:"powershell"; nocase;
    content:"Net.Sockets.TCPClient"; nocase; distance:0;
    classtype:trojan-activity;
    sid:3000061; rev:1;
    metadata:mitre_technique T1059.001;
)

alert tcp $HOME_NET any -> $EXTERNAL_NET any (
    msg:"ATTACK Potential Python reverse shell";
    flow:established;
    content:"import socket"; nocase;
    content:"subprocess"; nocase; distance:0;
    classtype:trojan-activity;
    sid:3000062; rev:1;
    metadata:mitre_technique T1059.006;
)
```

### Rule 8: Data Exfiltration via DNS TXT Records

```
# Detect potential data exfiltration via DNS TXT queries
# High volume of TXT queries to single domain is anomalous

alert dns $HOME_NET any -> any 53 (
    msg:"EXFIL Potential DNS TXT record exfiltration";
    content:"|00 10|";  # TXT query type
    pcre:"/^.{12}[a-zA-Z0-9+\/]{20,}\./";  # Base64-like subdomain
    threshold:type both, track by_src, count 20, seconds 60;
    classtype:trojan-activity;
    sid:3000070; rev:1;
    metadata:mitre_tactic Exfiltration, mitre_technique T1048.003;
)

# Large DNS responses (potential DNS tunneling download)
alert dns any 53 -> $HOME_NET any (
    msg:"EXFIL Large DNS TXT response - possible DNS tunnel";
    content:"|00 10|";  # TXT response
    dsize:>500;
    threshold:type both, track by_dst, count 10, seconds 60;
    classtype:trojan-activity;
    sid:3000071; rev:1;
    metadata:mitre_technique T1071.004;
)
```

## Rule Management Guidelines

### Classification Types

| classtype | Description | Priority |
|-----------|-------------|----------|
| attempted-admin | Attempted administrator privilege gain | 1 |
| trojan-activity | Trojan/C2 activity | 1 |
| attempted-user | Attempted user privilege gain | 2 |
| bad-unknown | Potentially bad traffic | 2 |
| policy-violation | Policy violation | 3 |
| misc-activity | Miscellaneous activity | 3 |

### SID Ranges (Organizational Convention)

| Range | Purpose |
|-------|---------|
| 3000001-3000099 | Protocol anomalies |
| 3000100-3000199 | Exploit signatures |
| 3000200-3000299 | Malware/C2 |
| 3000300-3000399 | Exfiltration |
| 3000400-3000499 | Policy violations |
| 3000500-3000599 | Custom/environment-specific |

### Performance Considerations

| Technique | Impact | Notes |
|-----------|--------|-------|
| Content match before PCRE | Major | Pre-filter with content to limit PCRE evaluation |
| Depth/offset limits | Moderate | Limit search area in packet |
| flow:established | Moderate | Skip connection setup packets |
| Threshold/rate limits | Major | Prevent alert flooding |
| Avoid negated content alone | Major | Negation without positive match is expensive |

## Cross-References

- [Sigma Rule Examples](sigma-rule-examples.md) -- host-based detection
- [YARA Rule Examples](yara-rule-examples.md) -- file-based detection
- [Network Segmentation Framework](../../frameworks/network-segmentation-framework.md) -- sensor placement
- [Network Monitoring Checklist](../../checklists/network/network-monitoring-checklist.md) -- monitoring setup
