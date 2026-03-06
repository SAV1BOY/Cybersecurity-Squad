# Critical Infrastructure Security

## Purpose

Industry-specific security reference for critical infrastructure sectors. Covers ICS/SCADA security, NERC CIP compliance, TSA security directives, the Purdue model for network architecture, and OT/IT convergence challenges for protecting industrial control systems and operational technology.

## ICS/SCADA Security Fundamentals

### OT vs IT Security Priorities

| Priority | IT Systems | OT/ICS Systems |
|----------|-----------|----------------|
| #1 | Confidentiality | Safety (human life) |
| #2 | Integrity | Availability (process continuity) |
| #3 | Availability | Integrity (process accuracy) |
| Patching | Regular, automated | Rare, planned, vendor-approved |
| Downtime tolerance | Minutes (failover) | Zero (some processes cannot stop) |
| Lifecycle | 3-5 years | 15-30 years |
| Protocols | TCP/IP, HTTP, TLS | Modbus, DNP3, OPC, Profinet, EtherNet/IP |
| Authentication | Standard (AD, MFA) | Often none or weak (legacy) |

### Common ICS Components

| Component | Function | Security Risk |
|-----------|----------|--------------|
| PLC (Programmable Logic Controller) | Controls physical processes | Logic manipulation, firmware attacks |
| RTU (Remote Terminal Unit) | Remote monitoring/control | Communication interception, spoofing |
| HMI (Human-Machine Interface) | Operator visualization | Unauthorized access, display manipulation |
| SCADA Server | Centralized monitoring | Single point of compromise |
| Historian | Process data storage | Data exfiltration, integrity attacks |
| Engineering Workstation | PLC programming | Logic bomb injection, configuration change |
| Safety Instrumented System (SIS) | Emergency shutdown | Disabling safety = catastrophic risk |

### ICS Attack Categories

| Category | Example | Impact |
|----------|---------|--------|
| Process manipulation | Stuxnet (centrifuge destruction) | Physical damage |
| View manipulation | HMI spoofing (show normal while abnormal) | Delayed response |
| Safety system attack | TRITON/TRISIS (SIS controller attack) | Remove safety net |
| Denial of control | Ransomware on SCADA (Colonial Pipeline) | Operational shutdown |
| Data exfiltration | Historian data theft | Intellectual property loss |

## Purdue Model (Reference Architecture)

### Network Zones

| Level | Name | Components | Security Controls |
|-------|------|-----------|-------------------|
| 5 | Enterprise | Corporate IT, email, ERP | Standard IT security |
| 4 | Site Business Planning | Production scheduling, MES | Firewall with application inspection |
| 3.5 | DMZ | Historian mirror, patch server, AV relay | Data diode or unidirectional gateway |
| 3 | Site Operations | SCADA server, historian, engineering workstations | Application whitelisting, dedicated AD |
| 2 | Area Supervisory | HMI, supervisory control | Network monitoring, access control |
| 1 | Basic Control | PLC, RTU, DCS controllers | Physical security, serial isolation |
| 0 | Process | Sensors, actuators, field devices | Physical security, safety systems |

### Key Architectural Principles

1. **No direct connectivity between Level 5 and Levels 0-3**
2. **DMZ (Level 3.5) mediates all IT/OT data exchange**
3. **Unidirectional gateways preferred over firewalls for Level 3.5**
4. **Separate Active Directory for OT network**
5. **No internet access from Levels 0-3**
6. **Remote access via jump server in DMZ only, with MFA and session recording**

## NERC CIP (North American Electric Reliability Corporation)

### Critical Standards

| Standard | Focus |
|----------|-------|
| CIP-002 | BES Cyber System Categorization (identify high/medium/low impact) |
| CIP-003 | Security Management Controls (policies, plans, responsibilities) |
| CIP-004 | Personnel and Training (background checks, training, access management) |
| CIP-005 | Electronic Security Perimeters (network segmentation, remote access) |
| CIP-006 | Physical Security (physical access control to BES cyber systems) |
| CIP-007 | System Security Management (ports/services, patching, malware, logging) |
| CIP-008 | Incident Reporting and Response Planning |
| CIP-009 | Recovery Plans (backup, recovery testing) |
| CIP-010 | Configuration Change Management and Vulnerability Assessment |
| CIP-011 | Information Protection (BES Cyber System Information handling) |
| CIP-013 | Supply Chain Risk Management |
| CIP-014 | Physical Security (transmission stations, substations) |

## TSA Security Directives

### Pipeline Security (Post-Colonial Pipeline)

| Directive | Requirements |
|-----------|-------------|
| SD-01 | Report cybersecurity incidents to CISA within 12 hours |
| SD-02 | Designate Cybersecurity Coordinator, report to TSA within 24 hours |
| SD-02 Rev | Network segmentation (OT/IT), access control, continuous monitoring, secure-by-design |

### Key Requirements

- Develop and implement cybersecurity incident response plan
- Cybersecurity Architecture Design Review
- Network segmentation policies and controls
- Access control measures (MFA, account management)
- Continuous monitoring and detection capabilities
- Patch management program with risk-based timelines
- Annual cybersecurity assessment plan

## OT/IT Convergence Challenges

| Challenge | Risk | Mitigation |
|-----------|------|------------|
| Shared networks | IT compromise reaches OT | Strict segmentation, unidirectional gateways |
| Cloud connectivity | OT data in cloud expands attack surface | Edge processing, encrypted tunnels, minimal cloud exposure |
| Remote access | VPN compromise = OT access | Dedicated OT remote access with MFA, session recording, time-limited |
| Patch management | IT patches break OT processes | OT-specific patch testing lab, vendor-approved patches only |
| Skill gap | IT security teams lack OT knowledge | Cross-training, OT-specific security roles |
| Legacy protocols | No authentication, no encryption | Protocol-aware firewalls, network monitoring, virtual patching |

## ICS Security Assessment Approach

### Safe Testing Principles

1. **Never actively scan OT networks without explicit authorization and vendor guidance**
2. **Use passive network monitoring for discovery**
3. **Test in lab environments that replicate production where possible**
4. **Coordinate all testing with process engineers and operators**
5. **Have rollback and emergency procedures pre-approved**
6. **Understand physical consequences of every action**

## Cross-References

- See `reference/industries/government-security.md` for government CI protection mandates
- See `frameworks/defense-layer.md` for detection in OT environments
- See `data/registries/common-ports-registry.md` for ICS protocol ports
- See `reference/tools/wireshark-reference.md` for OT protocol analysis
- See `templates/runbooks/ransomware-response-runbook.md` for OT ransomware response
