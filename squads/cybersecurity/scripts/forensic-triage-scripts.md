# Forensic Triage Automation Scripts

## Purpose

Provide automated triage scripts for rapid evidence collection from potentially compromised systems. Triage scripts collect volatile and key forensic artifacts quickly, enabling analysts to begin investigation without waiting for full disk images. These scripts prioritize speed and breadth of artifact collection during the critical first hours of incident response.

## When to Use
- Initial response to suspected compromise before full forensic imaging
- Rapid assessment of multiple systems during widespread incidents
- Evidence collection when full imaging is not feasible (cloud, large fleet)
- Initial data gathering to determine if full forensic analysis is warranted

## Prerequisites
- Administrative/root access to target system
- External storage or network share for output
- These scripts should be run FROM external media (USB, network share) to minimize target disk modification

---

## Windows Triage Script

```powershell
# windows_triage.ps1 - Windows forensic triage collection
# Run as Administrator from external media
# Usage: .\windows_triage.ps1 -OutputPath E:\evidence\hostname

param(
    [Parameter(Mandatory=$true)]
    [string]$OutputPath
)

$ErrorActionPreference = "Continue"
$Hostname = $env:COMPUTERNAME
$Timestamp = Get-Date -Format "yyyyMMdd_HHmmss"
$EvidencePath = Join-Path $OutputPath "${Hostname}_${Timestamp}"
New-Item -ItemType Directory -Path $EvidencePath -Force | Out-Null

Write-Host "=== Windows Forensic Triage ===" -ForegroundColor Cyan
Write-Host "Host: $Hostname"
Write-Host "Date: $(Get-Date)"
Write-Host "Output: $EvidencePath"
Write-Host "================================"

# --- System Information ---
Write-Host "[1/12] System Information..."
$SysInfo = @{
    Hostname = $env:COMPUTERNAME
    Domain = $env:USERDOMAIN
    OS = (Get-CimInstance Win32_OperatingSystem).Caption
    Version = (Get-CimInstance Win32_OperatingSystem).Version
    BootTime = (Get-CimInstance Win32_OperatingSystem).LastBootUpTime
    CurrentTime = Get-Date
    TimeZone = (Get-TimeZone).Id
    Uptime = ((Get-Date) - (Get-CimInstance Win32_OperatingSystem).LastBootUpTime).ToString()
}
$SysInfo | ConvertTo-Json | Out-File "$EvidencePath\system_info.json"

# --- Running Processes ---
Write-Host "[2/12] Running Processes..."
Get-Process | Select-Object Id, ProcessName, Path, StartTime,
    @{N='ParentId';E={(Get-CimInstance Win32_Process -Filter "ProcessId=$($_.Id)").ParentProcessId}},
    @{N='CommandLine';E={(Get-CimInstance Win32_Process -Filter "ProcessId=$($_.Id)").CommandLine}} |
    Export-Csv "$EvidencePath\processes.csv" -NoTypeInformation

# Process hashes for reputation checking
Get-Process | Where-Object {$_.Path} | ForEach-Object {
    [PSCustomObject]@{
        Name = $_.ProcessName
        PID = $_.Id
        Path = $_.Path
        SHA256 = (Get-FileHash $_.Path -Algorithm SHA256 -ErrorAction SilentlyContinue).Hash
    }
} | Export-Csv "$EvidencePath\process_hashes.csv" -NoTypeInformation

# --- Network Connections ---
Write-Host "[3/12] Network Connections..."
Get-NetTCPConnection | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort,
    State, OwningProcess,
    @{N='ProcessName';E={(Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue).ProcessName}} |
    Export-Csv "$EvidencePath\network_connections.csv" -NoTypeInformation

Get-NetUDPEndpoint | Select-Object LocalAddress, LocalPort, OwningProcess,
    @{N='ProcessName';E={(Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue).ProcessName}} |
    Export-Csv "$EvidencePath\udp_endpoints.csv" -NoTypeInformation

# DNS cache
Get-DnsClientCache | Export-Csv "$EvidencePath\dns_cache.csv" -NoTypeInformation

# ARP table
arp -a | Out-File "$EvidencePath\arp_table.txt"

# --- Logged-in Users ---
Write-Host "[4/12] User Sessions..."
query user 2>$null | Out-File "$EvidencePath\logged_in_users.txt"
qwinsta 2>$null | Out-File "$EvidencePath\sessions.txt"

# --- Autoruns / Persistence ---
Write-Host "[5/12] Persistence Mechanisms..."
$PersistPaths = @(
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run",
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce",
    "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run",
    "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce",
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServices",
    "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"
)
$PersistPaths | ForEach-Object {
    if (Test-Path $_) {
        Get-ItemProperty $_ | Out-File "$EvidencePath\registry_persistence.txt" -Append
    }
}

# Scheduled tasks
Get-ScheduledTask | Where-Object {$_.State -ne 'Disabled'} |
    Select-Object TaskName, TaskPath, State,
    @{N='Action';E={$_.Actions.Execute}},
    @{N='Arguments';E={$_.Actions.Arguments}} |
    Export-Csv "$EvidencePath\scheduled_tasks.csv" -NoTypeInformation

# Services (non-Microsoft)
Get-WmiObject Win32_Service | Where-Object {$_.PathName -and $_.PathName -notmatch 'Windows|Microsoft|svchost'} |
    Select-Object Name, DisplayName, State, StartMode, PathName, StartName |
    Export-Csv "$EvidencePath\services.csv" -NoTypeInformation

# --- Event Logs ---
Write-Host "[6/12] Event Logs (Security, System, PowerShell)..."
# Security events (last 48 hours)
$StartTime = (Get-Date).AddHours(-48)
Get-WinEvent -FilterHashtable @{LogName='Security'; StartTime=$StartTime} -MaxEvents 10000 -ErrorAction SilentlyContinue |
    Select-Object TimeCreated, Id, LevelDisplayName, Message |
    Export-Csv "$EvidencePath\security_events.csv" -NoTypeInformation

# System events
Get-WinEvent -FilterHashtable @{LogName='System'; StartTime=$StartTime} -MaxEvents 5000 -ErrorAction SilentlyContinue |
    Select-Object TimeCreated, Id, LevelDisplayName, Message |
    Export-Csv "$EvidencePath\system_events.csv" -NoTypeInformation

# PowerShell events
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-PowerShell/Operational'; StartTime=$StartTime} -MaxEvents 5000 -ErrorAction SilentlyContinue |
    Select-Object TimeCreated, Id, Message |
    Export-Csv "$EvidencePath\powershell_events.csv" -NoTypeInformation

# Sysmon events (if available)
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-Sysmon/Operational'; StartTime=$StartTime} -MaxEvents 10000 -ErrorAction SilentlyContinue |
    Select-Object TimeCreated, Id, Message |
    Export-Csv "$EvidencePath\sysmon_events.csv" -NoTypeInformation

# --- Prefetch Files ---
Write-Host "[7/12] Prefetch Files..."
if (Test-Path "C:\Windows\Prefetch") {
    Get-ChildItem "C:\Windows\Prefetch" -ErrorAction SilentlyContinue |
        Select-Object Name, CreationTime, LastWriteTime, Length |
        Export-Csv "$EvidencePath\prefetch_files.csv" -NoTypeInformation
}

# --- Recent Files and Downloads ---
Write-Host "[8/12] Recent Files and Downloads..."
Get-ChildItem "$env:USERPROFILE\Downloads" -Recurse -ErrorAction SilentlyContinue |
    Select-Object FullName, CreationTime, LastWriteTime, Length |
    Export-Csv "$EvidencePath\downloads.csv" -NoTypeInformation

Get-ChildItem "$env:TEMP" -ErrorAction SilentlyContinue |
    Select-Object FullName, CreationTime, LastWriteTime, Length |
    Export-Csv "$EvidencePath\temp_files.csv" -NoTypeInformation

# --- Browser History ---
Write-Host "[9/12] Browser History..."
$ChromeHistory = "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\History"
if (Test-Path $ChromeHistory) {
    Copy-Item $ChromeHistory "$EvidencePath\chrome_history.db" -ErrorAction SilentlyContinue
}
$EdgeHistory = "$env:LOCALAPPDATA\Microsoft\Edge\User Data\Default\History"
if (Test-Path $EdgeHistory) {
    Copy-Item $EdgeHistory "$EvidencePath\edge_history.db" -ErrorAction SilentlyContinue
}

# --- Firewall Configuration ---
Write-Host "[10/12] Firewall Configuration..."
Get-NetFirewallProfile | Select-Object Name, Enabled, DefaultInboundAction, DefaultOutboundAction |
    Export-Csv "$EvidencePath\firewall_profiles.csv" -NoTypeInformation

# --- Installed Software ---
Write-Host "[11/12] Installed Software..."
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* |
    Select-Object DisplayName, DisplayVersion, Publisher, InstallDate |
    Export-Csv "$EvidencePath\installed_software.csv" -NoTypeInformation

# --- File Hashes of Evidence ---
Write-Host "[12/12] Generating evidence hashes..."
Get-ChildItem $EvidencePath -File | ForEach-Object {
    [PSCustomObject]@{
        File = $_.Name
        SHA256 = (Get-FileHash $_.FullName -Algorithm SHA256).Hash
    }
} | Export-Csv "$EvidencePath\evidence_hashes.csv" -NoTypeInformation

Write-Host "`n=== Triage Complete ===" -ForegroundColor Green
Write-Host "Evidence collected in: $EvidencePath"
Write-Host "Files collected: $((Get-ChildItem $EvidencePath -File).Count)"
Write-Host "Total size: $([math]::Round((Get-ChildItem $EvidencePath -Recurse | Measure-Object Length -Sum).Sum / 1MB, 2)) MB"
```

## Linux Triage Script

```bash
#!/bin/bash
# linux_triage.sh - Linux forensic triage collection
# Run as root from external media
# Usage: sudo ./linux_triage.sh /mnt/evidence

OUTPUT_DIR="${1:-/tmp/evidence}/$(hostname)_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$OUTPUT_DIR"

echo "=== Linux Forensic Triage ==="
echo "Host: $(hostname)"
echo "Date: $(date)"
echo "Output: $OUTPUT_DIR"
echo "============================="

# System Information
echo "[1/10] System Information..."
{
  echo "Hostname: $(hostname)"
  echo "Date: $(date)"
  echo "Uptime: $(uptime)"
  echo "Kernel: $(uname -a)"
  echo "OS: $(cat /etc/os-release 2>/dev/null | head -5)"
} > "$OUTPUT_DIR/system_info.txt"

# Running Processes
echo "[2/10] Running Processes..."
ps auxwwf > "$OUTPUT_DIR/processes.txt"
ps -eo pid,ppid,user,args --sort=start_time > "$OUTPUT_DIR/processes_sorted.txt"

# Network Connections
echo "[3/10] Network Connections..."
ss -tulnp > "$OUTPUT_DIR/listening_sockets.txt"
ss -tnp > "$OUTPUT_DIR/established_connections.txt"
ip neighbor > "$OUTPUT_DIR/arp_table.txt"
ip route > "$OUTPUT_DIR/routing_table.txt"
cat /etc/resolv.conf > "$OUTPUT_DIR/dns_config.txt"
iptables -L -n -v > "$OUTPUT_DIR/iptables.txt" 2>/dev/null

# Logged-in Users
echo "[4/10] User Sessions..."
who > "$OUTPUT_DIR/who.txt"
w > "$OUTPUT_DIR/w.txt"
last -50 > "$OUTPUT_DIR/last_logins.txt"
lastb -50 > "$OUTPUT_DIR/failed_logins.txt" 2>/dev/null

# Persistence Mechanisms
echo "[5/10] Persistence Mechanisms..."
crontab -l > "$OUTPUT_DIR/root_crontab.txt" 2>/dev/null
ls -la /etc/cron.* > "$OUTPUT_DIR/cron_dirs.txt" 2>/dev/null
cat /etc/crontab > "$OUTPUT_DIR/etc_crontab.txt"
systemctl list-unit-files --type=service --state=enabled > "$OUTPUT_DIR/enabled_services.txt"
ls -la /etc/systemd/system/ > "$OUTPUT_DIR/systemd_custom.txt" 2>/dev/null

# User crontabs
for user in $(cut -f1 -d: /etc/passwd); do
  crontab -u "$user" -l 2>/dev/null >> "$OUTPUT_DIR/user_crontabs.txt"
done

# SSH authorized keys
echo "[6/10] SSH Keys..."
find /home -name "authorized_keys" -exec echo "=== {} ===" \; -exec cat {} \; > "$OUTPUT_DIR/authorized_keys.txt" 2>/dev/null
find /root -name "authorized_keys" -exec echo "=== {} ===" \; -exec cat {} \; >> "$OUTPUT_DIR/authorized_keys.txt" 2>/dev/null
cat /etc/ssh/sshd_config > "$OUTPUT_DIR/sshd_config.txt"

# Log Files
echo "[7/10] Log Files..."
cp /var/log/auth.log "$OUTPUT_DIR/auth.log" 2>/dev/null
cp /var/log/secure "$OUTPUT_DIR/secure.log" 2>/dev/null
cp /var/log/syslog "$OUTPUT_DIR/syslog" 2>/dev/null
journalctl --since "48 hours ago" --no-pager > "$OUTPUT_DIR/journal_48h.txt" 2>/dev/null
dmesg > "$OUTPUT_DIR/dmesg.txt"

# Shell History
echo "[8/10] Shell History..."
for user_home in /home/* /root; do
  username=$(basename "$user_home")
  for hist in .bash_history .zsh_history .sh_history; do
    if [ -f "$user_home/$hist" ]; then
      cp "$user_home/$hist" "$OUTPUT_DIR/${username}_${hist}" 2>/dev/null
    fi
  done
done

# Suspicious Files
echo "[9/10] Suspicious File Locations..."
find /tmp /dev/shm /var/tmp -type f -newer /etc/passwd -exec ls -la {} \; > "$OUTPUT_DIR/tmp_files.txt" 2>/dev/null
find / -name "*.sh" -newer /etc/passwd -not -path "/proc/*" -not -path "/sys/*" 2>/dev/null | head -100 > "$OUTPUT_DIR/recent_scripts.txt"
find / -perm -4000 -type f 2>/dev/null > "$OUTPUT_DIR/suid_files.txt"

# User Accounts
echo "[10/10] User Accounts..."
cat /etc/passwd > "$OUTPUT_DIR/passwd.txt"
cat /etc/group > "$OUTPUT_DIR/group.txt"
cat /etc/shadow > "$OUTPUT_DIR/shadow.txt" 2>/dev/null
awk -F: '$3 == 0 {print}' /etc/passwd > "$OUTPUT_DIR/uid0_accounts.txt"

# Generate evidence hashes
echo "[*] Generating evidence hashes..."
find "$OUTPUT_DIR" -type f -exec sha256sum {} \; > "$OUTPUT_DIR/evidence_hashes.txt"

echo ""
echo "=== Triage Complete ==="
echo "Evidence: $OUTPUT_DIR"
echo "Files: $(find "$OUTPUT_DIR" -type f | wc -l)"
echo "Size: $(du -sh "$OUTPUT_DIR" | cut -f1)"
```

## Timeline Generation

```bash
#!/bin/bash
# timeline_gen.sh - Generate timeline from triage artifacts
# Requires: plaso (log2timeline)

IMAGE_OR_DIR=$1
OUTPUT_DIR=$2

echo "[*] Generating forensic timeline..."

# Create Plaso timeline
log2timeline.py "$OUTPUT_DIR/timeline.plaso" "$IMAGE_OR_DIR"

# Convert to CSV
psort.py -o l2tcsv "$OUTPUT_DIR/timeline.plaso" -w "$OUTPUT_DIR/timeline.csv"

# Filter for investigation timeframe
echo "[*] Filtering timeline for investigation window..."
# Adjust dates as needed
psort.py -o l2tcsv "$OUTPUT_DIR/timeline.plaso" \
  --slice "2026-03-01T00:00:00" --slice_size 604800 \
  -w "$OUTPUT_DIR/timeline_filtered.csv"

echo "[*] Timeline generation complete"
```

## Cross-References

- `tasks/forensics/disk-image-analysis.md` — Full disk analysis
- `tasks/forensics/memory-forensics.md` — Memory acquisition and analysis
- `tasks/forensics/network-forensics.md` — Network evidence
- `workflows/incident-response-workflow.md` — IR process integration
- `scripts/log-analysis-queries.md` — SIEM queries for correlation
