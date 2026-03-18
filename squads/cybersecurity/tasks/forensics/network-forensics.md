# Network Packet Capture Analysis and Reconstruction

## Purpose

Analyze network traffic captures to identify malicious communications, reconstruct attacker activity, extract transferred files, and build evidence for incident response and legal proceedings. Network forensics provides the ground truth of what data traversed the wire, independent of endpoint tampering.

## Task Owner
Network forensics analyst or senior SOC analyst with packet analysis expertise.

## Prerequisites
- Packet capture files (PCAP/PCAPNG) from network taps, SPAN ports, or NDR systems
- Analysis tools: Wireshark, tshark, tcpdump, NetworkMiner, Zeek (Bro)
- Sufficient storage for captures and extracted artifacts
- Protocol knowledge for common enterprise and attack protocols

---

## Phase 1: Capture Acquisition and Preparation

### 1.1 Capture Sources

| Source | Type | Strengths | Limitations |
|--------|------|-----------|-------------|
| Network TAP | Full packet capture | Complete fidelity, passive | Requires physical access, storage |
| SPAN/Mirror port | Full packet capture | No additional hardware | May drop packets under load |
| NDR system | Full or metadata capture | Long-term storage, enrichment | May not store full payloads |
| Firewall/IDS logs | Flow data + alerts | Long retention, indexed | No payload content |
| Proxy logs | HTTP/HTTPS metadata | URL-level detail | HTTPS payload encrypted |
| DNS logs | Query/response data | Lightweight, high value | No payload content |

### 1.2 Capture Preparation
- [ ] Identify relevant capture timeframe based on incident timeline
- [ ] Extract relevant captures from storage (filter by time, IP, port if possible)
- [ ] Calculate hash of capture files for evidence integrity
- [ ] Document capture source, method, and any known gaps
- [ ] Transfer to forensic analysis workstation

### 1.3 Initial Assessment
```bash
# Capture file statistics
capinfos evidence.pcapng

# Quick protocol breakdown
tshark -r evidence.pcapng -z io,phs

# Conversation summary (top talkers)
tshark -r evidence.pcapng -z conv,ip

# Endpoint summary
tshark -r evidence.pcapng -z endpoints,ip
```

## Phase 2: Protocol Analysis

### 2.1 DNS Analysis
DNS is often the first indicator of compromise and a common C2 channel:
```bash
# Extract all DNS queries
tshark -r evidence.pcapng -Y "dns.flags.response == 0" -T fields -e frame.time -e ip.src -e dns.qry.name | sort | uniq -c | sort -rn

# Look for DNS tunneling indicators
tshark -r evidence.pcapng -Y "dns" -T fields -e dns.qry.name | awk '{print length, $0}' | sort -rn | head -50

# Find unusual DNS record types (TXT, NULL often used in tunneling)
tshark -r evidence.pcapng -Y "dns.qry.type == 16 or dns.qry.type == 10" -T fields -e frame.time -e dns.qry.name

# NXDOMAIN responses (potential DGA activity)
tshark -r evidence.pcapng -Y "dns.flags.rcode == 3" -T fields -e dns.qry.name | sort | uniq -c | sort -rn
```

**Analysis Focus:**
- [ ] High-entropy subdomain queries (DNS tunneling, DGA)
- [ ] Queries to known malicious domains
- [ ] Abnormal query volume from single host
- [ ] TXT record queries with large response sizes
- [ ] DNS responses from non-standard servers

### 2.2 HTTP/HTTPS Analysis
```bash
# HTTP requests summary
tshark -r evidence.pcapng -Y "http.request" -T fields -e frame.time -e ip.src -e http.host -e http.request.uri -e http.request.method

# HTTP POST requests (potential data exfiltration)
tshark -r evidence.pcapng -Y "http.request.method == POST" -T fields -e frame.time -e ip.src -e http.host -e http.content_length_header

# HTTP file downloads
tshark -r evidence.pcapng -Y "http.content_type contains \"application\"" -T fields -e frame.time -e http.content_type -e http.request.uri

# User-Agent strings (identify tools/malware)
tshark -r evidence.pcapng -Y "http.user_agent" -T fields -e http.user_agent | sort | uniq -c | sort -rn
```

**For HTTPS traffic:**
- [ ] Analyze TLS handshake metadata (JA3/JA3S fingerprints, SNI, certificate info)
- [ ] Check certificates for anomalies (self-signed, expired, mismatched CN)
- [ ] If TLS decryption keys available, decrypt and analyze payload
- [ ] Identify TLS connections to unusual ports

### 2.3 SMB/CIFS Analysis (Lateral Movement)
```bash
# SMB traffic (common in lateral movement)
tshark -r evidence.pcapng -Y "smb2" -T fields -e frame.time -e ip.src -e ip.dst -e smb2.cmd -e smb2.filename

# File transfers via SMB
tshark -r evidence.pcapng -Y "smb2.cmd == 5" -T fields -e frame.time -e ip.src -e ip.dst -e smb2.filename
```

### 2.4 Beaconing Detection
Identify periodic C2 communication patterns:
```bash
# Extract timestamps for connections to specific destination
tshark -r evidence.pcapng -Y "ip.dst == [SUSPICIOUS_IP]" -T fields -e frame.time_epoch | sort -n > beacon_times.txt

# Calculate inter-arrival times (using Python or awk)
# Look for consistent intervals (jitter < 20% = likely beaconing)
```

**Beaconing indicators:**
- [ ] Regular interval connections (every 30s, 60s, 300s, etc.)
- [ ] Consistent packet sizes in both directions
- [ ] Low data volume per connection (small commands, small responses)
- [ ] Connections persisting across business hours and non-business hours

### 2.5 Data Exfiltration Detection
```bash
# Large outbound data transfers
tshark -r evidence.pcapng -z conv,ip | sort -k6 -rn | head -20

# Outbound connections by data volume (bytes sent)
tshark -r evidence.pcapng -Y "ip.src == [INTERNAL_SUBNET]" -z io,stat,60,"BYTES()ip.src"
```

**Exfiltration indicators:**
- [ ] Unusual volume of data to external IP addresses
- [ ] Data transfers to cloud storage services (Mega, Dropbox, rclone endpoints)
- [ ] FTP/SCP/SFTP transfers to unknown destinations
- [ ] ICMP or DNS tunneling with high data volume
- [ ] Encrypted traffic to non-standard ports

## Phase 3: Artifact Extraction

### 3.1 File Carving
```bash
# Extract files from HTTP streams using NetworkMiner or Wireshark
# Wireshark: File > Export Objects > HTTP

# Using tcpflow for TCP stream extraction
tcpflow -r evidence.pcapng -o /evidence/extracted_files/

# Using Zeek for file extraction
zeek -r evidence.pcapng frameworks/files/extract-all-files.zeek
```

### 3.2 Stream Reconstruction
```bash
# Follow specific TCP stream
tshark -r evidence.pcapng -z follow,tcp,ascii,0

# Export all TCP streams
for i in $(seq 0 100); do
    tshark -r evidence.pcapng -z follow,tcp,raw,$i > /evidence/streams/stream_$i.raw 2>/dev/null
done
```

### 3.3 Credential Extraction
```bash
# Cleartext credentials in HTTP
tshark -r evidence.pcapng -Y "http.authbasic" -T fields -e http.authbasic

# NTLM authentication (for hash extraction)
tshark -r evidence.pcapng -Y "ntlmssp.auth" -T fields -e ntlmssp.auth.username -e ntlmssp.auth.domain

# FTP credentials
tshark -r evidence.pcapng -Y "ftp.request.command == USER or ftp.request.command == PASS" -T fields -e ftp.request.arg
```

## Phase 4: Zeek Log Analysis

### 4.1 Zeek Processing
```bash
# Process capture with Zeek for structured log generation
zeek -r evidence.pcapng

# Generated logs: conn.log, dns.log, http.log, ssl.log, files.log, etc.
```

### 4.2 Zeek Log Analysis
```bash
# Long connections (potential C2)
cat conn.log | zeek-cut id.orig_h id.resp_h id.resp_p duration | sort -t$'\t' -k4 -rn | head -20

# DNS queries to unique domains
cat dns.log | zeek-cut query | sort | uniq -c | sort -rn | head -50

# SSL/TLS connections with unusual certificates
cat ssl.log | zeek-cut id.orig_h id.resp_h server_name validation_status | grep -v "ok"
```

## Phase 5: Reporting

### 5.1 Network Forensics Report
- [ ] Executive summary of network-based findings
- [ ] Timeline of malicious network activity
- [ ] C2 communications identified (protocols, destinations, patterns)
- [ ] Data exfiltration evidence (volume, destination, data types)
- [ ] Lateral movement evidence (internal connections, protocols)
- [ ] Extracted IOCs (IPs, domains, URLs, JA3 hashes, user agents)
- [ ] Extracted files and their analysis results
- [ ] Network diagram showing attacker infrastructure and communication flow

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Disk evidence correlation
- `tasks/forensics/memory-forensics.md` — Memory evidence correlation
- `workflows/incident-response-workflow.md` — IR process integration
- `scripts/log-analysis-queries.md` — SIEM query examples
- `tasks/threat-intel/ioc-enrichment.md` — IOC enrichment for network indicators

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
