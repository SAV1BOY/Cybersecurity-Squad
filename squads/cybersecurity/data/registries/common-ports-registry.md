# Common Ports and Protocols Registry

## Purpose

Comprehensive port and protocol reference for security operations. Maps well-known ports to services, identifies security implications, highlights common misconfigurations, and provides detection guidance for suspicious port usage.

## Well-Known Ports (0-1023)

### Critical Service Ports

| Port | Protocol | Service | Security Notes |
|------|----------|---------|---------------|
| 20 | TCP | FTP Data | Cleartext transfer; should be replaced with SFTP |
| 21 | TCP | FTP Control | Cleartext credentials; often targeted for brute force |
| 22 | TCP | SSH | Key-based auth preferred; brute force target |
| 23 | TCP | Telnet | Cleartext everything; must be disabled |
| 25 | TCP | SMTP | Open relays abused for spam; STARTTLS required |
| 53 | TCP/UDP | DNS | Zone transfer (TCP); DNS tunneling detection needed |
| 67-68 | UDP | DHCP | Rogue DHCP server attacks |
| 69 | UDP | TFTP | No authentication; used in device provisioning attacks |
| 80 | TCP | HTTP | Cleartext; redirect to 443 |
| 88 | TCP/UDP | Kerberos | Kerberoasting, AS-REP roasting target |
| 110 | TCP | POP3 | Cleartext credentials; use 995 (POP3S) |
| 111 | TCP/UDP | RPCbind | Information disclosure; restrict to internal |
| 135 | TCP | MS-RPC | Lateral movement vector; restrict between segments |
| 137-139 | TCP/UDP | NetBIOS | Legacy; information disclosure, null sessions |
| 143 | TCP | IMAP | Cleartext; use 993 (IMAPS) |
| 161-162 | UDP | SNMP | v1/v2c cleartext community strings; use v3 |
| 389 | TCP/UDP | LDAP | Cleartext; use LDAPS (636) or STARTTLS |
| 443 | TCP | HTTPS | Verify TLS version and cipher suites |
| 445 | TCP | SMB | Ransomware propagation, lateral movement |
| 464 | TCP/UDP | Kerberos kpasswd | Password change protocol |
| 500 | UDP | IKE/IPsec | VPN endpoint; verify configuration |
| 514 | UDP | Syslog | Cleartext log transport; use TLS (6514) |
| 587 | TCP | SMTP Submission | Authenticated email sending |
| 636 | TCP | LDAPS | Encrypted LDAP; verify certificate |
| 993 | TCP | IMAPS | Encrypted IMAP |
| 995 | TCP | POP3S | Encrypted POP3 |

## Registered Ports (1024-49151)

### Database Ports

| Port | Service | Security Notes |
|------|---------|---------------|
| 1433 | MS SQL Server | Never expose externally; SQL injection target |
| 1521 | Oracle DB | TNS listener attacks |
| 3306 | MySQL/MariaDB | Remote root access if misconfigured |
| 5432 | PostgreSQL | Verify pg_hba.conf restrictions |
| 6379 | Redis | Default: no authentication; bind to localhost |
| 9200 | Elasticsearch | Default: no authentication; data exposure |
| 27017 | MongoDB | Historically exposed without auth |
| 9042 | Cassandra | CQL native transport |

### Web and Application Ports

| Port | Service | Security Notes |
|------|---------|---------------|
| 3000 | Grafana/Node apps | Development servers often exposed |
| 3389 | RDP | Brute force target; NLA required, MFA preferred |
| 5000 | Flask/Docker Registry | Development ports in production |
| 5601 | Kibana | Dashboard access may expose sensitive data |
| 8080 | HTTP Alternate | Common for proxies, Tomcat, Jenkins |
| 8443 | HTTPS Alternate | Management interfaces |
| 8888 | Jupyter Notebook | Code execution if exposed |
| 9090 | Prometheus | Metrics exposure |

### Remote Access and Management

| Port | Service | Security Notes |
|------|---------|---------------|
| 2222 | SSH alternate | Honeypot common port |
| 4444 | Metasploit default | Indicator of compromise |
| 5555 | Android ADB | Remote code execution if exposed |
| 5900-5901 | VNC | Weak authentication common |
| 5985-5986 | WinRM | PowerShell remoting; lateral movement |
| 8291 | MikroTik Winbox | Router management; targeted by botnets |

### C2 and Suspicious Ports

| Port | Common C2/Malware Use | Detection Notes |
|------|----------------------|-----------------|
| 4443 | Cobalt Strike default | HTTPS on non-standard port |
| 4444 | Meterpreter default | Alert on any traffic |
| 5555 | Android backdoor | Internal traffic unexpected |
| 6666-6669 | IRC | Legacy C2 channel |
| 8081 | Various malware | HTTP on non-standard port |
| 9001 | Tor default | Anonymization |
| 9050 | Tor SOCKS proxy | Data exfiltration |

## ICS/SCADA Ports

| Port | Protocol | Service |
|------|----------|---------|
| 502 | TCP | Modbus |
| 2404 | TCP | IEC 60870-5-104 |
| 4840 | TCP | OPC UA |
| 20000 | TCP/UDP | DNP3 |
| 44818 | TCP | EtherNet/IP |
| 47808 | UDP | BACnet |

## Port Security Assessment

### External Exposure Rules

| Category | Policy |
|----------|--------|
| Always block externally | 23, 135, 137-139, 445, 1433, 3306, 3389, 5432, 6379 |
| Restrict with MFA | 22, 443 (admin), 3389, 5985-5986 |
| Monitor closely | 53, 80, 443, 8080, 8443 |
| Investigate if seen | 4444, 5555, 6666-6669, 9001 |

### Quick Nmap Verification

```bash
# Check for common dangerous exposed services
nmap -sS -p 21,23,135,139,445,1433,3306,3389,5432,6379,9200,27017 --open target_range
```

## Cross-References

- See `reference/tools/nmap-reference.md` for port scanning methodology
- See `reference/tools/wireshark-reference.md` for protocol analysis
- See `frameworks/discovery-layer.md` for asset and service discovery
- See `reference/industries/critical-infrastructure-security.md` for ICS ports
- See `data/registries/windows-event-ids-registry.md` for connection event monitoring
