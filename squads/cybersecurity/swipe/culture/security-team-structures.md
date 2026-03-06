# Security Team Structures — Organizational Models

## Purpose
Reference models for building and organizing security teams at different maturity levels, from startup to enterprise.

## Team Structure Models

### Model 1: Startup/Early Stage (1-5 security staff)
```
Security Lead
├── AppSec Engineer (doubles as pentest)
├── Security Operations (doubles as IR)
└── GRC Analyst (doubles as awareness)
```
- **Key principle**: Generalists who can context-switch
- **Outsource**: Pentesting, threat intel, SOC monitoring (MSSP)
- **Focus**: Secure SDLC integration, cloud security basics, incident playbooks

### Model 2: Growth Stage (5-15 security staff)
```
CISO
├── Offensive Security
│   ├── Pentest Lead
│   └── AppSec Engineer (2)
├── Defensive Security
│   ├── SOC Lead
│   ├── Detection Engineer
│   └── IR Analyst
└── GRC
    ├── Compliance Analyst
    ├── Risk Analyst
    └── Security Awareness
```
- **Key principle**: Specialized teams with clear ownership
- **Build**: In-house SOC, detection engineering, vulnerability management
- **Focus**: MITRE ATT&CK coverage, metrics-driven security, red/blue collaboration

### Model 3: Enterprise (15-50+ security staff)
```
CISO
├── VP Offensive Security
│   ├── Red Team
│   ├── AppSec
│   ├── Bug Bounty Program
│   └── Threat Research
├── VP Defensive Security
│   ├── SOC (24/7)
│   ├── Detection Engineering
│   ├── Threat Intelligence
│   ├── Incident Response
│   └── Digital Forensics
├── VP Security Architecture
│   ├── Cloud Security
│   ├── Identity & Access
│   ├── Network Security
│   └── Data Protection
└── VP GRC
    ├── Compliance
    ├── Risk Management
    ├── Privacy
    └── Security Awareness
```

### Model 4: Unit 8200-Inspired (Intelligence-Grade)
```
Director of Cyber Operations
├── SIGINT / Collection
│   ├── Network Intelligence
│   ├── Endpoint Intelligence
│   └── OSINT/HUMINT Fusion
├── CNE (Computer Network Exploitation)
│   ├── Vulnerability Research
│   ├── Exploit Development
│   ├── Implant Engineering
│   └── Access Operations
├── CND (Computer Network Defense)
│   ├── Threat Hunt
│   ├── Detection Engineering
│   ├── Incident Response
│   └── Forensics & Attribution
├── Cyber Research
│   ├── Malware Analysis
│   ├── Protocol Analysis
│   └── Cryptanalysis
└── Mission Support
    ├── Infrastructure
    ├── Training & Simulation
    └── Legal & Policy
```

## Hiring Priorities by Maturity

| Maturity | First Hires | Key Skills |
|----------|-------------|------------|
| Level 1 | Security generalist | Broad knowledge, communication |
| Level 2 | SOC analyst, AppSec | Detection, secure coding |
| Level 3 | Detection engineer, Red team | MITRE mapping, exploit dev |
| Level 4 | Threat intel, Forensics | Attribution, malware RE |
| Level 5 | Vulnerability research, Crypto | Zero-day, protocol analysis |

## Cross-References
- `agents/cyber-chief.md` — Orchestrator and governance
- `frameworks/red-team-maturity-model.md` — Maturity assessment
- `templates/briefs/security-program-brief.md` — Program planning
