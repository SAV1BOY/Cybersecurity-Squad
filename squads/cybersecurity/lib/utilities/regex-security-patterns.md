# Security-Focused Regex Patterns

## Purpose

Library of regex patterns for security operations. Covers email validation, URL parsing, injection detection, XSS pattern matching, IP extraction, and log analysis patterns for detection engineering, WAF rules, and security tool development.

## Important Caveats

1. Regex-based detection is a defense layer, not a complete solution
2. Attackers actively evade regex patterns; layer with other controls
3. Test patterns against bypass techniques before deployment
4. Consider performance: catastrophic backtracking can cause ReDoS
5. Always combine with proper output encoding and parameterized queries

## Input Validation Patterns

### Email Validation

```regex
# Basic email validation (covers 99% of legitimate addresses)
^[a-zA-Z0-9._%+\-]+@[a-zA-Z0-9.\-]+\.[a-zA-Z]{2,}$

# Note: RFC 5322 compliant email regex is extremely complex
# For production, use a validated library, not regex alone
```

### URL Validation and Parsing

```regex
# Basic URL with protocol enforcement
^https?:\/\/[a-zA-Z0-9\-\.]+\.[a-zA-Z]{2,}(\/[^\s]*)?$

# Extract domain from URL
https?:\/\/([^\/\?#:]+)

# Detect protocol-relative URLs (potential open redirect)
^\/\/[^\/]

# Detect javascript: or data: URI schemes (XSS vectors)
(?i)^(javascript|data|vbscript):
```

### IP Address Patterns

```regex
# IPv4 address (basic)
\b(?:\d{1,3}\.){3}\d{1,3}\b

# IPv4 address (strict validation, 0-255 per octet)
\b(?:(?:25[0-5]|2[0-4]\d|[01]?\d\d?)\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d\d?)\b

# IPv4 with CIDR
\b(?:\d{1,3}\.){3}\d{1,3}\/(?:3[0-2]|[12]?\d)\b

# IPv6 address (simplified)
(?:[0-9a-fA-F]{1,4}:){7}[0-9a-fA-F]{1,4}|::(?:[0-9a-fA-F]{1,4}:){0,6}[0-9a-fA-F]{1,4}

# Private IPv4 ranges
\b(?:10\.\d{1,3}\.\d{1,3}\.\d{1,3}|172\.(?:1[6-9]|2\d|3[01])\.\d{1,3}\.\d{1,3}|192\.168\.\d{1,3}\.\d{1,3})\b
```

## Injection Detection Patterns

### SQL Injection Indicators

```regex
# Common SQL injection patterns
(?i)(\b(union|select|insert|update|delete|drop|alter|create|exec|execute)\b.*\b(from|into|table|database|where|set)\b)

# SQL comment injection
(--|#|\/\*|\*\/)

# Tautology attacks
(?i)(\bor\b|\band\b)\s+[\'\"]?\d+[\'\"]?\s*=\s*[\'\"]?\d+

# UNION-based injection
(?i)union\s+(all\s+)?select

# Stacked queries
;\s*(select|insert|update|delete|drop|alter|exec)

# Common SQL functions in input
(?i)(concat|char|ascii|substring|benchmark|sleep|waitfor|pg_sleep)\s*\(

# WARNING: These catch common patterns but are easily bypassed.
# Parameterized queries are the real defense.
```

### XSS Detection Patterns

```regex
# Script tag injection
(?i)<\s*script[^>]*>

# Event handler injection
(?i)\bon\w+\s*=

# JavaScript URI
(?i)javascript\s*:

# Data URI with HTML/JS content
(?i)data\s*:[^,]*(?:text\/html|application\/javascript)

# SVG with script
(?i)<\s*svg[^>]*\bon\w+

# Expression/eval patterns
(?i)(eval|expression|javascript|vbscript|livescript)\s*\(

# Encoded variations (double encoding, HTML entities)
(?i)(%3c|&lt;|&#60;|&#x3c;)\s*(script|img|svg|iframe|object|embed|link|style)

# WARNING: XSS detection via regex is inherently incomplete.
# Content Security Policy + output encoding are the real defenses.
```

### Command Injection Indicators

```regex
# Shell metacharacters
[;&|`$]

# Command chaining
(\|\||&&|;)\s*\w+

# Backtick execution
`[^`]+`

# Process substitution
\$\([^)]+\)

# Common dangerous commands after injection
(?i)(cat|ls|pwd|whoami|id|uname|wget|curl|nc|ncat|bash|sh|python|perl|ruby)\b
```

### Path Traversal Patterns

```regex
# Directory traversal
(?:\.\.\/|\.\.\\|%2e%2e%2f|%2e%2e\/|\.\.%2f|%2e%2e%5c)

# Null byte injection
%00|\\x00|\\0

# Absolute path references
^(\/|[a-zA-Z]:\\)
```

### SSRF Indicators

```regex
# Internal IP addresses in URL parameters
(?i)(127\.\d+\.\d+\.\d+|localhost|0\.0\.0\.0|10\.\d+\.\d+\.\d+|172\.(1[6-9]|2\d|3[01])\.\d+\.\d+|192\.168\.\d+\.\d+)

# Cloud metadata endpoints
(?i)(169\.254\.169\.254|metadata\.google|metadata\.azure)

# DNS rebinding indicators (short hostnames, unusual TLDs)
# Best detected with actual DNS resolution, not regex
```

## Log Analysis Patterns

### Windows Log Patterns

```regex
# Failed RDP login
(?i)An account failed to log on.*Logon Type:\s*10

# Service installation (Sysmon)
(?i)Event ID:\s*7045.*Service File Name:

# PowerShell encoded command
(?i)powershell.*\-[eE](?:nc|ncodedcommand)\s+[A-Za-z0-9+/=]{20,}
```

### Linux Log Patterns

```regex
# SSH brute force
Failed password for .* from ([\d\.]+) port \d+ ssh2

# Successful SSH root login
Accepted .* for root from ([\d\.]+)

# Sudo command execution
sudo:.*COMMAND=(.+)

# Cron job modification
CRON.*EDIT.*\((\w+)\)
```

### Web Server Log Patterns

```regex
# Directory scanning
(?:\/\.env|\/\.git|\/wp-admin|\/phpinfo|\/actuator|\/swagger|\/graphql|\/\.well-known)

# Web shell indicators in URL
(?i)(cmd=|exec=|shell=|eval=|system=|passthru=|c99|r57|b374k)

# Large response to non-file endpoint (data exfiltration)
# Analyze response sizes in access logs for anomalies
```

## IOC Extraction Patterns

```regex
# MD5 hash
\b[a-fA-F0-9]{32}\b

# SHA-1 hash
\b[a-fA-F0-9]{40}\b

# SHA-256 hash
\b[a-fA-F0-9]{64}\b

# Domain name
\b(?:[a-zA-Z0-9](?:[a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?\.)+[a-zA-Z]{2,}\b

# Windows file path
[a-zA-Z]:\\(?:[^\\/:*?"<>|\r\n]+\\)*[^\\/:*?"<>|\r\n]+

# Registry key
(?i)(HKEY_LOCAL_MACHINE|HKEY_CURRENT_USER|HKLM|HKCU)\\[^\s]+
```

## ReDoS Prevention

```
DANGEROUS patterns that cause catastrophic backtracking:
  (a+)+$           # Nested quantifiers
  (a|a)+$          # Overlapping alternatives with quantifier
  (.*a){10}        # Greedy quantifier with constraint

SAFE alternatives:
  a+$              # Simple quantifier (no nesting)
  (?:a)+$          # Non-capturing with single option
  [^b]*a           # Character class instead of .*

Rule: Avoid nested quantifiers on overlapping patterns.
Test with regex performance tools before deployment.
```

## Cross-References

- See `lib/patterns/input-validation-patterns.md` for validation strategy
- See `lib/utilities/encoding-decoding-utility.md` for encoding bypass awareness
- See `reference/tools/splunk-reference.md` for regex in SPL queries
- See `reference/tools/burp-suite-reference.md` for web testing with regex
- See `data/registries/http-status-codes-security.md` for response analysis
