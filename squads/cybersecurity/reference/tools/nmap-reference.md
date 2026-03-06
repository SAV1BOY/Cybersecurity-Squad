# Nmap Complete Reference

## Purpose

Comprehensive operational reference for Nmap (Network Mapper), the foundational network reconnaissance and security auditing tool. Covers scan types, NSE scripting, timing optimization, firewall evasion, and service/version detection strategies for authorized security assessments.

## Core Scan Types

### TCP Scans

| Scan | Flag | Description | Use Case |
|------|------|-------------|----------|
| TCP Connect | `-sT` | Full TCP handshake | When SYN scan unavailable (no raw socket access) |
| SYN Stealth | `-sS` | Half-open scan (default with root) | Standard fast port discovery |
| FIN | `-sF` | FIN flag only | Bypass simple stateless firewalls |
| Xmas | `-sX` | FIN+PSH+URG flags | Fingerprint OS/firewall behavior |
| NULL | `-sN` | No flags set | Firewall evasion on Unix targets |
| ACK | `-sA` | ACK flag only | Map firewall rulesets (filtered vs unfiltered) |
| Window | `-sW` | ACK with window analysis | Distinguish open/closed on some stacks |
| Maimon | `-sM` | FIN+ACK | Rare; works against specific BSD stacks |

### UDP Scans

```bash
# Basic UDP scan (slow; combine with version detection)
nmap -sU -sV --version-intensity 0 -T4 target

# Top UDP ports only (faster)
nmap -sU --top-ports 100 target

# Combined TCP+UDP
nmap -sS -sU -T4 target
```

### Host Discovery

| Method | Flag | Best For |
|--------|------|----------|
| ARP ping | `-PR` | Local network (fastest, most reliable) |
| ICMP echo | `-PE` | Networks allowing ICMP |
| TCP SYN ping | `-PS80,443` | Filtered networks |
| TCP ACK ping | `-PA80,443` | Stateful firewall bypass |
| UDP ping | `-PU53,161` | Supplementary discovery |
| No ping | `-Pn` | Force scan when host discovery blocked |
| List scan | `-sL` | DNS resolution only, no packets sent |

## Timing Templates

| Template | Flag | Packets/sec | Use Case |
|----------|------|-------------|----------|
| Paranoid | `-T0` | Serial, 5 min delay | IDS evasion (extremely slow) |
| Sneaky | `-T1` | Serial, 15 sec delay | IDS evasion |
| Polite | `-T2` | Serial, 0.4 sec delay | Bandwidth-sensitive networks |
| Normal | `-T3` | Default | Standard assessment |
| Aggressive | `-T4` | Parallel, short timeouts | Fast internal scans |
| Insane | `-T5` | Max parallel, minimal timeouts | Lab/CTF environments only |

### Custom Timing

```bash
# Fine-grained control
nmap --min-rate 1000 --max-retries 2 --host-timeout 30m \
     --max-rtt-timeout 200ms --initial-rtt-timeout 100ms target
```

## NSE (Nmap Scripting Engine)

### Script Categories

| Category | Description |
|----------|-------------|
| `auth` | Authentication bypass and credential testing |
| `broadcast` | Network service discovery via broadcast |
| `brute` | Brute-force credential attacks |
| `default` | Safe scripts run with `-sC` |
| `discovery` | Service and network enumeration |
| `dos` | Denial of service (use with caution) |
| `exploit` | Active exploitation scripts |
| `external` | Queries external services (whois, virustotal) |
| `fuzzer` | Protocol fuzzing |
| `intrusive` | Potentially disruptive checks |
| `malware` | Backdoor and malware detection |
| `safe` | Non-intrusive information gathering |
| `version` | Enhanced version detection |
| `vuln` | Vulnerability detection |

### Critical NSE Scripts

```bash
# Vulnerability scanning
nmap --script vuln target

# SMB enumeration suite
nmap --script smb-enum-shares,smb-enum-users,smb-os-discovery -p 445 target

# HTTP enumeration
nmap --script http-title,http-headers,http-methods,http-enum -p 80,443,8080 target

# SSL/TLS analysis
nmap --script ssl-enum-ciphers,ssl-cert,ssl-heartbleed -p 443 target

# DNS enumeration
nmap --script dns-brute,dns-zone-transfer --script-args dns-brute.threads=10 -p 53 target

# Default credentials check
nmap --script http-default-accounts -p 80,443,8080 target
```

### Custom NSE Script Arguments

```bash
# Pass arguments to scripts
nmap --script http-brute --script-args \
  http-brute.path=/admin,userdb=users.txt,passdb=pass.txt target
```

## Service and Version Detection

```bash
# Standard version detection
nmap -sV target

# Aggressive version detection (all probes)
nmap -sV --version-all target

# Light version detection (fast)
nmap -sV --version-light target

# OS detection
nmap -O --osscan-guess target

# Combined comprehensive scan
nmap -sS -sV -O -sC -T4 -p- target
```

## Firewall Evasion Techniques

```bash
# Fragment packets
nmap -f target                    # 8-byte fragments
nmap --mtu 16 target              # Custom fragment size

# Decoy scan
nmap -D RND:10 target             # 10 random decoys
nmap -D decoy1,decoy2,ME target   # Specific decoys

# Spoof source port (DNS, HTTP)
nmap --source-port 53 target

# Randomize target order
nmap --randomize-hosts -iL targets.txt

# Append random data
nmap --data-length 50 target

# Idle scan (zombie)
nmap -sI zombie_host target
```

## Output Formats

```bash
# All major formats simultaneously
nmap -oA scan_results target

# Individual formats
nmap -oN normal.txt target        # Normal text
nmap -oX results.xml target       # XML (for parsers)
nmap -oG results.gnmap target     # Grepable
nmap -oS results.txt target       # Script kiddie (joke format)

# Verbose and debug
nmap -v target                    # Verbose
nmap -vv target                   # Very verbose
nmap -d target                    # Debug
nmap --reason target              # Show port state reasons
nmap --packet-trace target        # Full packet trace
```

## Common Engagement Patterns

### External Perimeter Scan

```bash
nmap -sS -sV -sC -O -T4 -p- --open -oA external_full target_range
nmap -sU --top-ports 50 -sV -T4 -oA external_udp target_range
```

### Internal Network Sweep

```bash
# Fast host discovery
nmap -sn -T4 10.0.0.0/16 -oG alive_hosts.gnmap
# Full port scan on discovered hosts
grep "Up" alive_hosts.gnmap | awk '{print $2}' | \
  nmap -sS -sV -sC -T4 -p- -iL - -oA internal_full
```

### Targeted Service Hunt

```bash
# Find all web servers
nmap -sS -p 80,443,8080,8443,8000,3000,5000 -T4 --open 10.0.0.0/16
# Find all databases
nmap -sS -p 1433,3306,5432,27017,6379,9200 -T4 --open 10.0.0.0/16
```

## Cross-References

- See `reference/tools/metasploit-reference.md` for post-discovery exploitation
- See `frameworks/discovery-layer.md` for reconnaissance methodology
- See `tasks/discovery/asset-discovery.md` for asset discovery workflows
- See `data/registries/common-ports-registry.md` for port/service mappings
- See `reference/tools/wireshark-reference.md` for packet-level analysis
