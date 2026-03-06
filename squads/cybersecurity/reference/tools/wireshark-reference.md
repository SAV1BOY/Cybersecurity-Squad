# Wireshark Reference

## Purpose

Operational reference for Wireshark, the premier network protocol analyzer. Covers capture and display filters, protocol dissection, stream reconstruction, statistical analysis, and expert diagnostics for network security analysis, incident response, and forensic investigations.

## Capture Filters (BPF Syntax)

Capture filters use Berkeley Packet Filter syntax and are applied before packets are stored.

### Common Capture Filters

```
# By host
host 10.0.0.5
src host 10.0.0.5
dst host 10.0.0.5

# By network
net 10.0.0.0/24
src net 192.168.0.0/16

# By port
port 443
dst port 80
portrange 8000-9000

# By protocol
tcp
udp
icmp
arp

# Compound filters
host 10.0.0.5 and port 443
tcp and not port 22
(dst port 80 or dst port 443) and src net 10.0.0.0/24

# Capture only SYN packets (connection initiations)
tcp[tcpflags] & (tcp-syn) != 0 and tcp[tcpflags] & (tcp-ack) == 0
```

## Display Filters

Display filters are applied to already-captured traffic and use Wireshark's protocol dissector field names.

### Protocol Filters

```
# HTTP analysis
http.request.method == "POST"
http.response.code >= 400
http.host contains "example.com"
http.request.uri contains "admin"
http.content_type contains "json"
http.cookie contains "session"
http.authorization

# TLS/SSL
tls.handshake.type == 1           # Client Hello
tls.handshake.extensions_server_name contains "target.com"
ssl.alert_message                  # SSL alerts
tls.record.version == 0x0301      # TLS 1.0 (deprecated)

# DNS
dns.qry.name contains "evil.com"
dns.qry.type == 1                 # A record queries
dns.qry.type == 28                # AAAA queries
dns.flags.rcode != 0              # DNS errors
dns.resp.len > 512                # Possible DNS tunneling

# SMB
smb2.cmd == 5                     # Create (file access)
smb2.filename contains ".exe"
smb.access.generic_all            # Full access attempts

# Kerberos
kerberos.CNameString              # Principal names
kerberos.error_code               # Authentication failures
```

### Security-Focused Filters

```
# Suspicious activity
tcp.flags.syn == 1 and tcp.flags.ack == 0    # SYN scan detection
icmp.type == 8                                # ICMP echo (ping sweep)
tcp.dstport == 4444 or tcp.dstport == 5555    # Common backdoor ports
dns.qry.name matches "^[a-z0-9]{30,}"        # DNS tunneling indicator

# Data exfiltration indicators
frame.len > 1400 and ip.dst != 10.0.0.0/8    # Large packets leaving network
dns.qry.name matches "\\..*\\."              # Subdomain encoding
icmp.data.len > 64                            # ICMP tunneling

# Credential exposure
http.authorization                            # Basic auth (cleartext)
ftp.request.command == "PASS"                 # FTP passwords
telnet                                        # Cleartext terminal
pop.request.command == "PASS"                 # POP3 passwords

# Anomalies
tcp.analysis.retransmission                   # Network issues
tcp.analysis.zero_window                      # Buffer problems
tcp.analysis.duplicate_ack_num > 3            # Possible packet loss
```

## Stream Following

### TCP Stream Reconstruction

Right-click packet > Follow > TCP Stream (or `tcp.stream eq N`)

Use cases:
- Reconstruct HTTP sessions without TLS
- View command-and-control communications
- Extract transferred files
- Read plaintext protocol exchanges (FTP, Telnet, SMTP)

### HTTP Stream

Follow > HTTP Stream shows request-response pairs with content decompression.

### TLS Stream

Requires session keys for decryption:

```
# Set TLS key log file
Edit > Preferences > Protocols > TLS > (Pre)-Master-Secret log filename

# Browser key logging (set env var before launching browser)
export SSLKEYLOGFILE=/tmp/tlskeys.log
```

## Statistics and Analysis

### Key Statistics Tools

| Tool | Menu Path | Security Use |
|------|-----------|-------------|
| Conversations | Statistics > Conversations | Identify top talkers, unusual pairs |
| Endpoints | Statistics > Endpoints | Map active hosts |
| Protocol Hierarchy | Statistics > Protocol Hierarchy | Detect unusual protocols |
| I/O Graphs | Statistics > I/O Graphs | Visualize traffic patterns, spikes |
| Flow Graph | Statistics > Flow Graph | Visualize connection sequences |
| DNS | Statistics > DNS | Query volume, response analysis |
| HTTP Requests | Statistics > HTTP > Requests | URL enumeration |

### Expert Information

Analyze > Expert Information provides automated detection of:

- **Errors**: Malformed packets, checksum failures, reassembly issues
- **Warnings**: Connection resets, retransmissions, window problems
- **Notes**: Duplicate ACKs, keep-alive, TCP window updates
- **Chats**: Normal protocol operations (SYN, FIN)

## File Extraction

### Export Objects

File > Export Objects supports:
- HTTP objects (files transferred via web)
- SMB objects (files transferred via file shares)
- TFTP objects
- IMF (email messages)
- DICOM (medical imaging)

### Manual Extraction

For protocols without built-in export:
1. Follow TCP stream of the transfer
2. Switch to "Raw" display
3. Save the stream content
4. Trim protocol headers if necessary

## Command-Line (tshark)

```bash
# Capture with filter
tshark -i eth0 -f "port 80" -w capture.pcap

# Read and display filter
tshark -r capture.pcap -Y "http.request.method == POST"

# Extract specific fields
tshark -r capture.pcap -Y "dns" -T fields -e dns.qry.name -e dns.resp.addr

# Statistics
tshark -r capture.pcap -z conv,tcp
tshark -r capture.pcap -z io,stat,1,"COUNT(frame)frame"

# Ring buffer capture (rotate files)
tshark -i eth0 -b filesize:100000 -b files:10 -w /capture/ring.pcap
```

## Cross-References

- See `reference/tools/nmap-reference.md` for network scanning that generates analyzable traffic
- See `reference/books/sanders-practical-packet-analysis.md` for methodology depth
- See `frameworks/defense-layer.md` for network monitoring integration
- See `frameworks/exfiltration-detection-methodology.md` for data loss detection
- See `data/registries/common-ports-registry.md` for port-service correlation
