# Network Calculation Utility

## Purpose

Reference for network calculations commonly needed in security operations. Covers CIDR notation, subnet calculations, IP range parsing, private address ranges, and network segmentation analysis for penetration testers, SOC analysts, and network security engineers.

## CIDR Notation Reference

### Quick Reference Table

| CIDR | Subnet Mask | Hosts | Wildcard | Common Use |
|------|------------|-------|----------|------------|
| /32 | 255.255.255.255 | 1 | 0.0.0.0 | Single host |
| /31 | 255.255.255.254 | 2 | 0.0.0.1 | Point-to-point link |
| /30 | 255.255.255.252 | 2 | 0.0.0.3 | Small P2P subnet |
| /29 | 255.255.255.248 | 6 | 0.0.0.7 | Small server subnet |
| /28 | 255.255.255.240 | 14 | 0.0.0.15 | Small department |
| /27 | 255.255.255.224 | 30 | 0.0.0.31 | Medium subnet |
| /26 | 255.255.255.192 | 62 | 0.0.0.63 | Large subnet |
| /25 | 255.255.255.128 | 126 | 0.0.0.127 | Half Class C |
| /24 | 255.255.255.0 | 254 | 0.0.0.255 | Standard LAN |
| /23 | 255.255.254.0 | 510 | 0.0.1.255 | Large LAN |
| /22 | 255.255.252.0 | 1,022 | 0.0.3.255 | Campus segment |
| /21 | 255.255.248.0 | 2,046 | 0.0.7.255 | Large campus |
| /20 | 255.255.240.0 | 4,094 | 0.0.15.255 | Enterprise segment |
| /16 | 255.255.0.0 | 65,534 | 0.0.255.255 | Class B equivalent |
| /12 | 255.240.0.0 | 1,048,574 | 0.15.255.255 | Large enterprise |
| /8 | 255.0.0.0 | 16,777,214 | 0.255.255.255 | Class A equivalent |

### Calculation Formula

```
Usable hosts = 2^(32 - prefix_length) - 2
Network address = IP AND subnet_mask
Broadcast address = IP OR wildcard_mask
First usable = Network address + 1
Last usable = Broadcast address - 1
```

## Private and Reserved Address Ranges

### RFC 1918 Private Ranges

| Range | CIDR | Class | Total IPs | Typical Use |
|-------|------|-------|-----------|-------------|
| 10.0.0.0 - 10.255.255.255 | 10.0.0.0/8 | A | 16,777,216 | Enterprise internal |
| 172.16.0.0 - 172.31.255.255 | 172.16.0.0/12 | B | 1,048,576 | Medium enterprise |
| 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 | C | 65,536 | Home/small office |

### Other Reserved Ranges

| Range | Purpose | Security Relevance |
|-------|---------|-------------------|
| 127.0.0.0/8 | Loopback | SSRF target |
| 169.254.0.0/16 | Link-local (APIPA) | Misconfigured DHCP indicator |
| 169.254.169.254/32 | Cloud metadata | SSRF critical target (AWS, GCP, Azure) |
| 100.64.0.0/10 | Carrier-grade NAT (CGNAT) | ISP shared space |
| 192.0.0.0/24 | IETF Protocol Assignments | |
| 192.0.2.0/24 | TEST-NET-1 (documentation) | |
| 198.51.100.0/24 | TEST-NET-2 (documentation) | |
| 203.0.113.0/24 | TEST-NET-3 (documentation) | |
| 224.0.0.0/4 | Multicast | Network recon via multicast |
| 240.0.0.0/4 | Reserved (future use) | |
| 0.0.0.0/8 | "This network" | SSRF bypass attempts |
| fc00::/7 | IPv6 Unique Local (ULA) | IPv6 private equivalent |
| fe80::/10 | IPv6 Link-Local | |
| ::1/128 | IPv6 Loopback | SSRF target |

## Subnet Calculation Examples

### Calculate Subnet Details

```bash
# Using ipcalc (install: apt install ipcalc)
ipcalc 192.168.1.100/24
# Network:   192.168.1.0/24
# Broadcast: 192.168.1.255
# HostMin:   192.168.1.1
# HostMax:   192.168.1.254
# Hosts:     254

# Using sipcalc
sipcalc 10.0.0.0/22
```

### Python Subnet Calculator

```python
import ipaddress

# Subnet information
network = ipaddress.ip_network('192.168.1.0/24')
print(f"Network:   {network.network_address}")
print(f"Broadcast: {network.broadcast_address}")
print(f"Netmask:   {network.netmask}")
print(f"Hosts:     {network.num_addresses - 2}")
print(f"First:     {list(network.hosts())[0]}")
print(f"Last:      {list(network.hosts())[-1]}")

# Check if IP is in range
ip = ipaddress.ip_address('192.168.1.50')
print(f"In network: {ip in network}")  # True

# Check if IP is private
print(f"Is private: {ip.is_private}")  # True

# Subdivide network
for subnet in network.subnets(prefixlen_diff=2):
    print(f"  {subnet} ({subnet.num_addresses - 2} hosts)")

# List all IPs in a range (for scanning scope)
for ip in ipaddress.ip_network('10.0.0.0/29').hosts():
    print(ip)
```

## IP Range Parsing

### Common Range Formats

| Format | Example | Meaning |
|--------|---------|---------|
| CIDR | 192.168.1.0/24 | 256 addresses |
| Range | 192.168.1.1-192.168.1.50 | 50 addresses |
| Nmap-style | 192.168.1.1-50 | 50 addresses |
| Nmap octet | 192.168.1,2.0-255 | 512 addresses |
| Wildcard | 192.168.1.* | 256 addresses |
| Single host | 192.168.1.1 | 1 address |

### Nmap Target Specification

```bash
# Multiple formats in single scan
nmap 192.168.1.0/24 10.0.0.1-50 172.16.0.5

# Exclude hosts
nmap 192.168.1.0/24 --exclude 192.168.1.1,192.168.1.254

# From file
nmap -iL targets.txt --excludefile exclusions.txt
```

## Security Segmentation Analysis

### Common Network Zones

| Zone | Purpose | Example CIDR | Access Policy |
|------|---------|-------------|---------------|
| DMZ | Internet-facing services | 10.0.1.0/24 | Limited inbound, restricted outbound |
| Production | Business applications | 10.0.10.0/22 | Internal access, controlled internet |
| Database | Data stores | 10.0.20.0/24 | App servers only, no direct user access |
| Management | Admin infrastructure | 10.0.30.0/24 | Jump box only, heavily monitored |
| User | Workstations | 10.0.100.0/20 | Internet via proxy, limited internal |
| Guest | Visitor WiFi | 172.16.0.0/24 | Internet only, no internal access |
| IoT/OT | Devices and sensors | 10.0.200.0/24 | Isolated, minimal internet |

### Segmentation Verification

```bash
# From each zone, test connectivity to other zones
# Expected: only authorized paths succeed

# Quick verification script
for target in 10.0.1.1 10.0.10.1 10.0.20.1 10.0.30.1; do
  echo -n "$target: "
  timeout 2 bash -c "echo >/dev/tcp/$target/443" 2>/dev/null && echo "OPEN" || echo "CLOSED"
done
```

## Cross-References

- See `reference/tools/nmap-reference.md` for network scanning with these ranges
- See `data/registries/common-ports-registry.md` for service identification
- See `frameworks/discovery-layer.md` for network discovery methodology
- See `reference/industries/critical-infrastructure-security.md` for OT network segmentation
- See `lib/utilities/regex-security-patterns.md` for IP extraction patterns
