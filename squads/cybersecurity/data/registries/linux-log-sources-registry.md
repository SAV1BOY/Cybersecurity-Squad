# Linux Security Log Sources Registry

## Purpose

Comprehensive reference for Linux security-relevant log sources. Maps log files to security events, provides key patterns to monitor, and covers audit framework configuration for threat detection, incident response, and forensic analysis on Linux systems.

## Core Log Files

### Authentication Logs

| Log File | Distribution | Contents |
|----------|-------------|----------|
| `/var/log/auth.log` | Debian/Ubuntu | SSH, sudo, PAM, su, cron auth |
| `/var/log/secure` | RHEL/CentOS | SSH, sudo, PAM, su, cron auth |
| `/var/log/faillog` | All | Failed login attempts (binary, use `faillog` command) |
| `/var/log/lastlog` | All | Last login per user (binary, use `lastlog` command) |
| `/var/log/btmp` | All | Failed login attempts (binary, use `last -f /var/log/btmp`) |
| `/var/log/wtmp` | All | Login/logout history (binary, use `last`) |

### Key Authentication Patterns

```
# SSH brute force
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn

# Successful SSH logins
grep "Accepted" /var/log/auth.log

# Sudo usage
grep "sudo:" /var/log/auth.log

# User switching (su)
grep "su:" /var/log/auth.log

# Account creation
grep "useradd" /var/log/auth.log
grep "adduser" /var/log/auth.log

# Password changes
grep "passwd" /var/log/auth.log
```

### System Logs

| Log File | Contents | Security Relevance |
|----------|----------|-------------------|
| `/var/log/syslog` (Debian) | General system messages | Service starts/stops, errors, kernel messages |
| `/var/log/messages` (RHEL) | General system messages | Same as above |
| `/var/log/kern.log` | Kernel messages | Kernel exploits, module loading, iptables |
| `/var/log/dmesg` | Boot messages | Hardware and driver issues, tampering indicators |
| `/var/log/boot.log` | Boot process | Service startup failures |
| `/var/log/cron` or `/var/log/cron.log` | Cron execution | Persistence via cron, unauthorized tasks |
| `/var/log/daemon.log` | Daemon messages | Background service behavior |

### Application Logs

| Log File | Service | Security Events |
|----------|---------|----------------|
| `/var/log/apache2/access.log` | Apache | Web access, scanning, exploitation attempts |
| `/var/log/apache2/error.log` | Apache | Application errors, misconfiguration |
| `/var/log/nginx/access.log` | Nginx | Web access patterns |
| `/var/log/nginx/error.log` | Nginx | Backend errors, proxy issues |
| `/var/log/mysql/error.log` | MySQL | Authentication failures, query errors |
| `/var/log/postgresql/` | PostgreSQL | Connection attempts, query failures |
| `/var/log/mail.log` | Mail server | Spam relay, unauthorized sending |

## Linux Audit Framework (auditd)

### Configuration

```bash
# /etc/audit/audit.rules

# Self-auditing (protect audit system)
-w /etc/audit/ -p wa -k auditconfig
-w /etc/libaudit.conf -p wa -k auditconfig
-w /var/log/audit/ -p wa -k audittampering

# Authentication monitoring
-w /etc/passwd -p wa -k identity
-w /etc/group -p wa -k identity
-w /etc/shadow -p wa -k identity
-w /etc/gshadow -p wa -k identity
-w /etc/sudoers -p wa -k sudoers
-w /etc/sudoers.d/ -p wa -k sudoers

# SSH configuration changes
-w /etc/ssh/sshd_config -p wa -k sshconfig

# Cron persistence detection
-w /etc/crontab -p wa -k cron
-w /etc/cron.d/ -p wa -k cron
-w /var/spool/cron/ -p wa -k cron

# Network configuration
-w /etc/hosts -p wa -k hosts
-w /etc/resolv.conf -p wa -k dns
-w /etc/iptables/ -p wa -k firewall
-w /etc/nftables.conf -p wa -k firewall

# Kernel module loading
-w /sbin/insmod -p x -k modules
-w /sbin/modprobe -p x -k modules
-w /sbin/rmmod -p x -k modules
-a always,exit -F arch=b64 -S init_module -S delete_module -k modules

# File access monitoring for sensitive paths
-w /etc/pam.d/ -p wa -k pam
-w /etc/ld.so.conf -p wa -k libpath
-w /etc/ld.so.preload -p wa -k libpreload

# Process execution
-a always,exit -F arch=b64 -S execve -k exec

# Privilege escalation
-a always,exit -F arch=b64 -S setuid -S setgid -k privesc
```

### Audit Log Analysis

```bash
# Search audit logs
ausearch -k identity -ts today          # Identity file changes today
ausearch -m USER_AUTH -ts recent         # Recent authentication events
ausearch -m EXECVE -ts today             # Process executions today
ausearch -k modules -ts this-week       # Kernel module changes this week

# Generate audit reports
aureport --auth --summary               # Authentication summary
aureport --login --summary              # Login summary
aureport --failed --summary             # Failed events summary
aureport --key --summary                # Events by audit key
```

## Systemd Journal

```bash
# Security-relevant journal queries
journalctl -u sshd --since "1 hour ago"          # SSH service events
journalctl _TRANSPORT=audit --since today          # Audit events via journal
journalctl -p err --since "24 hours ago"           # All error-level messages
journalctl --unit=systemd-logind --since today     # Login manager events
journalctl -b -1                                    # Previous boot logs
journalctl _UID=0 --since "1 hour ago"             # Root activity
journalctl -k                                       # Kernel messages
```

## Key Security Events to Monitor

### Critical Alerts (Immediate Investigation)

| Event | Log Source | Pattern |
|-------|-----------|---------|
| Root login from network | auth.log | `Accepted.*root.*from` |
| SSH login from new IP | auth.log | Source IP not in baseline |
| New user created | auth.log | `useradd` or `adduser` |
| Sudoers modified | audit.log | Key=sudoers |
| Kernel module loaded | audit.log | Key=modules |
| Binary in /tmp executed | audit.log | execve with path=/tmp/ |
| Audit log cleared | audit.log | Audit daemon restart/config change |
| Cron job added | audit.log | Key=cron |
| /etc/passwd modified | audit.log | Key=identity |
| SSH config changed | audit.log | Key=sshconfig |

### Persistence Detection Points

| Mechanism | Files/Dirs to Monitor |
|-----------|----------------------|
| Cron jobs | `/etc/crontab`, `/etc/cron.*`, `/var/spool/cron/` |
| Systemd services | `/etc/systemd/system/`, `/usr/lib/systemd/system/` |
| Init scripts | `/etc/init.d/`, `/etc/rc.local` |
| Shell profiles | `/etc/profile`, `/etc/profile.d/`, `~/.bashrc`, `~/.bash_profile` |
| SSH authorized keys | `~/.ssh/authorized_keys`, `/etc/ssh/` |
| LD_PRELOAD | `/etc/ld.so.preload`, `LD_PRELOAD` env variable |
| PAM modules | `/etc/pam.d/`, `/lib/security/` |
| At jobs | `/var/spool/at/` |

## Log Integrity and Forwarding

### Best Practices

1. Forward logs to centralized SIEM in real time (rsyslog, Fluentd, Filebeat)
2. Enable log signing/hashing for tamper evidence
3. Set `immutable` attribute on audit rules after deployment: `-e 2`
4. Monitor for log gap (absence of expected logs = tampering indicator)
5. Retain logs per compliance requirements (typically 1-7 years)
6. Compress and archive rotated logs with checksums

## Cross-References

- See `data/registries/windows-event-ids-registry.md` for Windows equivalent
- See `reference/tools/splunk-reference.md` for log analysis queries
- See `frameworks/defense-layer.md` for detection strategy
- See `frameworks/persistence-analysis-methodology.md` for persistence detection
- See `workflows/detection-engineering-workflow.md` for detection development
