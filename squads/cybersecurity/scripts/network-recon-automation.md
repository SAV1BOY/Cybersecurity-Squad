# Network Reconnaissance Automation Scripts

## Purpose

Provide automated network reconnaissance scripts and methodologies for authorized security assessments. These scripts cover host discovery, port scanning, service enumeration, and vulnerability identification. All scripts must be used only with explicit authorization within defined scope.

## Authorization Requirement
These scripts are for authorized security assessments only. Unauthorized scanning of networks is illegal. Ensure written authorization and defined scope before execution.

---

## Phase 1: Host Discovery

### 1.1 Passive Discovery (No Packets Sent to Targets)

**DNS Enumeration:**
```bash
#!/bin/bash
# dns_enum.sh - Comprehensive DNS enumeration
DOMAIN=$1
OUTPUT_DIR="recon/${DOMAIN}"
mkdir -p "$OUTPUT_DIR"

echo "[*] Starting DNS enumeration for $DOMAIN"

# Subdomain enumeration with multiple tools
echo "[+] Running subfinder..."
subfinder -d "$DOMAIN" -silent -o "$OUTPUT_DIR/subfinder.txt"

echo "[+] Running amass (passive)..."
amass enum -passive -d "$DOMAIN" -o "$OUTPUT_DIR/amass.txt"

echo "[+] Running assetfinder..."
assetfinder --subs-only "$DOMAIN" > "$OUTPUT_DIR/assetfinder.txt"

# Merge and deduplicate
echo "[+] Merging results..."
cat "$OUTPUT_DIR"/*.txt | sort -u > "$OUTPUT_DIR/all_subdomains.txt"
echo "[*] Found $(wc -l < "$OUTPUT_DIR/all_subdomains.txt") unique subdomains"

# Resolve live hosts
echo "[+] Resolving live hosts..."
cat "$OUTPUT_DIR/all_subdomains.txt" | httpx -silent -status-code -title -tech-detect -o "$OUTPUT_DIR/live_hosts.txt"

echo "[*] DNS enumeration complete. Results in $OUTPUT_DIR/"
```

**Certificate Transparency Log Search:**
```bash
#!/bin/bash
# ct_search.sh - Certificate transparency log enumeration
DOMAIN=$1
echo "[*] Searching certificate transparency logs for $DOMAIN"

# Using crt.sh
curl -s "https://crt.sh/?q=%25.$DOMAIN&output=json" | \
  jq -r '.[].name_value' | \
  sort -u | \
  grep -v '^\*\.' > "recon/${DOMAIN}/ct_subdomains.txt"

echo "[*] Found $(wc -l < "recon/${DOMAIN}/ct_subdomains.txt") domains from CT logs"
```

### 1.2 Active Host Discovery

**Multi-Method Network Discovery:**
```bash
#!/bin/bash
# host_discovery.sh - Active host discovery
SUBNET=$1
OUTPUT_DIR="recon/network"
mkdir -p "$OUTPUT_DIR"

echo "[*] Starting host discovery on $SUBNET"

# ICMP ping sweep
echo "[+] ICMP ping sweep..."
nmap -sn -PE "$SUBNET" -oG "$OUTPUT_DIR/ping_sweep.gnmap"

# ARP discovery (local subnet only)
echo "[+] ARP discovery..."
nmap -sn -PR "$SUBNET" -oG "$OUTPUT_DIR/arp_discovery.gnmap"

# TCP SYN discovery on common ports (bypasses ICMP blocking)
echo "[+] TCP SYN discovery..."
nmap -sn -PS22,80,443,445,3389,8080,8443 "$SUBNET" -oG "$OUTPUT_DIR/tcp_discovery.gnmap"

# Merge live hosts
echo "[+] Merging live hosts..."
grep "Status: Up" "$OUTPUT_DIR"/*.gnmap | \
  awk '{print $2}' | sort -u > "$OUTPUT_DIR/live_hosts.txt"

echo "[*] Discovered $(wc -l < "$OUTPUT_DIR/live_hosts.txt") live hosts"
```

## Phase 2: Port Scanning

### 2.1 Staged Port Scanning

**Quick Scan (Top Ports):**
```bash
#!/bin/bash
# quick_scan.sh - Fast top-ports scan
TARGETS=$1  # File with IP list
OUTPUT_DIR="recon/portscan"
mkdir -p "$OUTPUT_DIR"

echo "[*] Quick scan: Top 1000 ports"
nmap -sS -sV --top-ports 1000 -T4 --open \
  -iL "$TARGETS" \
  -oA "$OUTPUT_DIR/quick_scan" \
  --min-rate 1000

echo "[*] Quick scan complete"
```

**Comprehensive Scan (All TCP Ports):**
```bash
#!/bin/bash
# full_scan.sh - All TCP ports with service detection
TARGETS=$1
OUTPUT_DIR="recon/portscan"
mkdir -p "$OUTPUT_DIR"

echo "[*] Full TCP port scan"

# Stage 1: Fast SYN scan of all ports
echo "[+] Stage 1: Port discovery (all 65535 ports)..."
nmap -sS -p- -T4 --open --min-rate 1000 \
  -iL "$TARGETS" \
  -oG "$OUTPUT_DIR/all_ports.gnmap"

# Extract open ports
PORTS=$(grep -oP '\d+/open' "$OUTPUT_DIR/all_ports.gnmap" | \
  cut -d/ -f1 | sort -un | paste -sd,)

echo "[+] Open ports found: $PORTS"

# Stage 2: Detailed scan of discovered ports only
echo "[+] Stage 2: Service detection and scripts..."
nmap -sS -sV -sC -p"$PORTS" \
  -iL "$TARGETS" \
  -oA "$OUTPUT_DIR/detailed_scan"

echo "[*] Full scan complete"
```

**UDP Scan (Top Ports):**
```bash
#!/bin/bash
# udp_scan.sh - Top UDP ports
TARGETS=$1
OUTPUT_DIR="recon/portscan"

echo "[*] UDP scan: Top 100 ports"
nmap -sU --top-ports 100 -T4 --open \
  -iL "$TARGETS" \
  -oA "$OUTPUT_DIR/udp_scan"
```

## Phase 3: Service Enumeration

### 3.1 Web Service Enumeration

```bash
#!/bin/bash
# web_enum.sh - Web service enumeration
TARGET=$1
OUTPUT_DIR="recon/web/${TARGET}"
mkdir -p "$OUTPUT_DIR"

echo "[*] Web enumeration for $TARGET"

# Technology detection
echo "[+] Technology detection..."
whatweb "$TARGET" -v > "$OUTPUT_DIR/whatweb.txt"

# Directory and file discovery
echo "[+] Directory brute force..."
feroxbuster -u "https://$TARGET" \
  -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt \
  -x php,asp,aspx,jsp,html,js,json,txt,bak \
  -t 50 -d 2 --status-codes 200,301,302,403 \
  -o "$OUTPUT_DIR/directories.txt"

# Virtual host discovery
echo "[+] Virtual host discovery..."
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
  -u "https://$TARGET" -H "Host: FUZZ.$TARGET" \
  -mc 200,301,302 -fs 0 \
  -o "$OUTPUT_DIR/vhosts.json"

# Screenshot
echo "[+] Taking screenshots..."
gowitness single "https://$TARGET" -P "$OUTPUT_DIR/screenshots/"

# SSL/TLS assessment
echo "[+] SSL/TLS assessment..."
testssl --html "$TARGET" > "$OUTPUT_DIR/testssl.html"

echo "[*] Web enumeration complete"
```

### 3.2 SMB Enumeration

```bash
#!/bin/bash
# smb_enum.sh - SMB service enumeration
TARGET=$1
OUTPUT_DIR="recon/smb/${TARGET}"
mkdir -p "$OUTPUT_DIR"

echo "[*] SMB enumeration for $TARGET"

# Anonymous access check
echo "[+] Checking anonymous access..."
smbclient -L "//$TARGET" -N > "$OUTPUT_DIR/shares.txt" 2>&1

# Enum4linux
echo "[+] Running enum4linux-ng..."
enum4linux-ng "$TARGET" -oA "$OUTPUT_DIR/enum4linux"

# CrackMapExec share enumeration
echo "[+] Share enumeration..."
crackmapexec smb "$TARGET" --shares -u '' -p '' > "$OUTPUT_DIR/cme_shares.txt"

# SMB signing check
echo "[+] SMB signing check..."
crackmapexec smb "$TARGET" --gen-relay-list "$OUTPUT_DIR/no_signing.txt"

echo "[*] SMB enumeration complete"
```

### 3.3 Active Directory Enumeration (Authorized Assessment)

```bash
#!/bin/bash
# ad_enum.sh - AD enumeration with valid credentials
DOMAIN=$1
DC=$2
USER=$3
PASS=$4
OUTPUT_DIR="recon/ad/${DOMAIN}"
mkdir -p "$OUTPUT_DIR"

echo "[*] AD enumeration for $DOMAIN"

# BloodHound collection
echo "[+] BloodHound data collection..."
bloodhound-python -d "$DOMAIN" -u "$USER" -p "$PASS" -ns "$DC" \
  -c All --zip -o "$OUTPUT_DIR/bloodhound/"

# LDAP enumeration
echo "[+] LDAP enumeration..."
ldapsearch -H "ldap://$DC" -D "$USER@$DOMAIN" -w "$PASS" \
  -b "DC=$(echo $DOMAIN | sed 's/\./,DC=/g')" \
  "(objectClass=user)" sAMAccountName memberOf > "$OUTPUT_DIR/users.txt"

# Group Policy enumeration
echo "[+] Group Policy enumeration..."
crackmapexec smb "$DC" -u "$USER" -p "$PASS" -M gpp_password > "$OUTPUT_DIR/gpp.txt"

echo "[*] AD enumeration complete"
```

## Phase 4: Automated Reconnaissance Pipeline

### 4.1 Full Recon Orchestration

```bash
#!/bin/bash
# full_recon.sh - Orchestrate complete reconnaissance
# Usage: ./full_recon.sh <target_file> <output_dir>
TARGETS=$1
OUTPUT_DIR=${2:-"recon/$(date +%Y%m%d)"}
mkdir -p "$OUTPUT_DIR"

echo "======================================"
echo " Automated Reconnaissance Pipeline"
echo " Targets: $TARGETS"
echo " Output: $OUTPUT_DIR"
echo " Started: $(date)"
echo "======================================"

# Stage 1: Host discovery
echo "[STAGE 1] Host Discovery"
nmap -sn -iL "$TARGETS" -oG "$OUTPUT_DIR/discovery.gnmap"
grep "Status: Up" "$OUTPUT_DIR/discovery.gnmap" | awk '{print $2}' > "$OUTPUT_DIR/live.txt"
LIVE_COUNT=$(wc -l < "$OUTPUT_DIR/live.txt")
echo "[*] $LIVE_COUNT live hosts discovered"

# Stage 2: Port scanning
echo "[STAGE 2] Port Scanning"
nmap -sS -sV --top-ports 1000 -T4 --open -iL "$OUTPUT_DIR/live.txt" \
  -oA "$OUTPUT_DIR/portscan"

# Stage 3: Web service identification
echo "[STAGE 3] Web Service Identification"
grep -E "80/|443/|8080/|8443/" "$OUTPUT_DIR/portscan.gnmap" | \
  awk '{print $2}' | sort -u > "$OUTPUT_DIR/web_targets.txt"

# Run httpx on web targets
cat "$OUTPUT_DIR/web_targets.txt" | httpx -silent -status-code -title -tech-detect \
  -o "$OUTPUT_DIR/web_services.txt"

# Stage 4: Screenshots
echo "[STAGE 4] Screenshots"
gowitness file -f "$OUTPUT_DIR/web_targets.txt" -P "$OUTPUT_DIR/screenshots/"

# Stage 5: Vulnerability scanning (NSE scripts)
echo "[STAGE 5] Vulnerability Assessment"
nmap -sV --script=vuln -iL "$OUTPUT_DIR/live.txt" \
  -oA "$OUTPUT_DIR/vulnscan"

echo "======================================"
echo " Reconnaissance Complete"
echo " Finished: $(date)"
echo " Results: $OUTPUT_DIR/"
echo "======================================"
```

## Output Processing

### Parse Nmap Results
```bash
# Extract open ports per host
grep "Ports:" portscan.gnmap | while read line; do
  IP=$(echo "$line" | awk '{print $2}')
  PORTS=$(echo "$line" | grep -oP '\d+/open' | cut -d/ -f1 | paste -sd,)
  echo "$IP: $PORTS"
done
```

### Generate Report Summary
```bash
# Quick stats from scan results
echo "=== Recon Summary ==="
echo "Live hosts: $(wc -l < live.txt)"
echo "Web servers: $(wc -l < web_targets.txt)"
echo "Open ports breakdown:"
grep -oP '\d+/open/tcp' portscan.gnmap | cut -d/ -f1 | sort | uniq -c | sort -rn | head -20
```

## Safety and Ethics

- Always verify scope authorization before scanning
- Use rate limiting to avoid disrupting production systems
- Log all scanning activity for accountability
- Do not scan third-party infrastructure without explicit permission
- Respect cloud provider acceptable use policies
- Stop immediately if unintended impact is observed

## Cross-References

- `tasks/discovery/attack-surface-mapping.md` — Attack surface methodology
- `tasks/discovery/asset-discovery.md` — Asset discovery procedures
- `tasks/red-team/recon-and-enumeration.md` — Red team recon
- `docs/security-testing-methodology.md` — Testing methodology
- `frameworks/discovery-layer.md` — Discovery framework
