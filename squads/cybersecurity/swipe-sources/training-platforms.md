# Security Training Platforms and Labs

## Purpose

This guide catalogs the best security training platforms, hands-on labs, and certification paths organized by skill level and specialization. Continuous skill development is non-negotiable in cybersecurity — the threat landscape evolves faster than any static training program. This guide helps squad members select the right training for their current level and career trajectory.

## Skill Level Definitions

| Level | Description | Experience |
|-------|------------|------------|
| **Beginner** | Learning fundamentals, building core skills | 0-2 years |
| **Intermediate** | Competent practitioner, working independently | 2-5 years |
| **Advanced** | Deep expertise in specialization, mentoring others | 5-10 years |
| **Expert** | Industry-recognized skill, developing new techniques | 10+ years |

## Hands-On Lab Platforms

### Hack The Box (HTB)
- **URL**: https://www.hackthebox.com/
- **Skill Level**: Beginner to Expert
- **Focus**: Penetration testing, privilege escalation, web exploitation, Active Directory attacks, forensics
- **Format**: Vulnerable machines (retired and active), challenges, Pro Labs (multi-machine networks), Academy courses
- **Cost**: Free tier available; VIP subscription for retired machines; Pro Labs are separate purchases
- **Strengths**: Large community, regularly updated machines, career-relevant skill paths, Pro Labs simulate real enterprise networks
- **Best For**: Offensive security skill development, OSCP preparation, staying sharp on current techniques
- **Recommended Path**: Start with Academy "Penetration Tester" path, then Starting Point machines, then Easy/Medium boxes

### TryHackMe (THM)
- **URL**: https://tryhackme.com/
- **Skill Level**: Beginner to Intermediate
- **Focus**: Broad cybersecurity fundamentals, blue team, red team, cloud security, SOC analysis
- **Format**: Guided rooms with step-by-step instructions, learning paths, King of the Hill competitions
- **Cost**: Free tier with limited rooms; Premium for full access
- **Strengths**: Most accessible platform for beginners, excellent guided learning, browser-based (no local setup needed)
- **Best For**: Onboarding new security team members, building foundational skills, introducing non-security IT staff to security concepts
- **Recommended Path**: "Pre-Security" path for complete beginners, "SOC Level 1" for aspiring analysts, "Jr Penetration Tester" for offensive track

### SANS Ranges and NetWars
- **URL**: https://www.sans.org/cyber-ranges/
- **Skill Level**: Intermediate to Expert
- **Focus**: DFIR, penetration testing, ICS/SCADA, cloud security
- **Format**: Competitive challenges, simulated environments, tournament-style events
- **Cost**: Often included with SANS course enrollment; some standalone events
- **Strengths**: Highest-quality scenarios, realistic enterprise environments, world-class instruction
- **Best For**: Advanced skill development, team exercises, certification preparation

### PortSwigger Web Security Academy
- **URL**: https://portswigger.net/web-security
- **Skill Level**: Beginner to Advanced
- **Focus**: Web application security exclusively
- **Format**: Free interactive labs covering OWASP Top 10 and beyond, with explanations and solutions
- **Cost**: Completely free
- **Strengths**: Best free resource for web application security, progressive difficulty, authoritative content from the creators of Burp Suite
- **Best For**: Web application pentesters, developers learning application security, BSCP certification preparation

### Offensive Security Proving Grounds
- **URL**: https://www.offsec.com/labs/
- **Skill Level**: Intermediate to Advanced
- **Focus**: Penetration testing, exploit development
- **Format**: Practice (community-contributed) and Play (OffSec-built) machines
- **Cost**: Subscription-based
- **Strengths**: Closest preparation to the OSCP exam environment
- **Best For**: OSCP preparation, building methodology discipline

### PentesterLab
- **URL**: https://pentesterlab.com/
- **Skill Level**: Beginner to Advanced
- **Focus**: Web security, code review, exploit development
- **Format**: Progressive exercises with badges, real CVE recreations
- **Cost**: Pro subscription for full access
- **Strengths**: Excellent progression system, teaches underlying concepts not just tool usage, real-world CVE exercises
- **Best For**: Understanding vulnerability classes deeply, code review skills

## Blue Team and DFIR Training

### Blue Team Labs Online (BTLO)
- **URL**: https://blueteamlabs.online/
- **Skill Level**: Beginner to Advanced
- **Focus**: SOC analysis, DFIR, threat hunting, reverse engineering
- **Format**: Investigation challenges, realistic scenarios
- **Cost**: Free and paid tiers
- **Best For**: SOC analysts, incident responders, threat hunters

### CyberDefenders
- **URL**: https://cyberdefenders.org/
- **Skill Level**: Intermediate to Advanced
- **Focus**: Digital forensics, incident response, threat hunting
- **Format**: Challenge-based labs using real-world artifacts (pcaps, memory dumps, disk images)
- **Cost**: Free
- **Best For**: DFIR skill validation, forensic analysis practice

### LetsDefend
- **URL**: https://letsdefend.io/
- **Skill Level**: Beginner to Intermediate
- **Focus**: SOC operations, alert triage, incident response
- **Format**: Simulated SOC environment with realistic alerts
- **Cost**: Free tier available
- **Best For**: SOC analyst onboarding, alert triage practice

## Certification Paths

### Offensive Security Certifications
| Certification | Focus | Prereq Level | Exam Format |
|--------------|-------|--------------|-------------|
| OSCP (PEN-200) | Penetration Testing | Intermediate | 24-hour hands-on exam |
| OSWE (WEB-300) | Web Exploitation | Advanced | 48-hour hands-on exam |
| OSEP (PEN-300) | Advanced Evasion | Advanced | 48-hour hands-on exam |
| OSED (EXP-301) | Exploit Development | Advanced | 48-hour hands-on exam |

### SANS/GIAC Certifications
| Certification | Focus | Course |
|--------------|-------|--------|
| GSEC | Security Essentials | SEC401 |
| GCIH | Incident Handler | SEC504 |
| GPEN | Penetration Tester | SEC560 |
| GCFA | Forensic Analyst | FOR508 |
| GREM | Reverse Engineering Malware | FOR610 |
| GCIA | Intrusion Analyst | SEC503 |

### Other Notable Certifications
| Certification | Focus | Organization |
|--------------|-------|-------------|
| CISSP | Security Management | (ISC)2 |
| CISM | Security Management | ISACA |
| CISA | Audit | ISACA |
| CCSP | Cloud Security | (ISC)2 |
| BSCP | Web Security | PortSwigger |
| BTL1/BTL2 | Blue Team | Security Blue Team |
| PNPT | Penetration Testing | TCM Security |

## Training Budget Allocation Recommendations

| Role | Primary Platform | Secondary | Certification Target |
|------|-----------------|-----------|---------------------|
| SOC Analyst (Junior) | TryHackMe | LetsDefend | GSEC or BTL1 |
| SOC Analyst (Senior) | BTLO, CyberDefenders | SANS courses | GCIH, GCIA |
| Penetration Tester | Hack The Box | PortSwigger Academy | OSCP, then OSWE/OSEP |
| Incident Responder | CyberDefenders | SANS courses | GCFA, GCIH |
| Security Engineer | TryHackMe, Hack The Box | Cloud provider training | Platform-specific certs + GSEC |
| Security Leader | SANS Leadership courses | Industry conferences | CISSP, CISM |

## Self-Directed Learning Resources

### YouTube Channels
- **IppSec** — Hack The Box machine walkthroughs with expert commentary
- **John Hammond** — CTF walkthroughs, malware analysis, security concepts
- **NetworkChuck** — Beginner-friendly networking and security
- **LiveOverflow** — Binary exploitation and vulnerability research
- **David Bombal** — Networking and ethical hacking

### Books (Foundational)
- "The Web Application Hacker's Handbook" (Stuttard, Pinto) — Web security bible
- "Practical Malware Analysis" (Sikorski, Honig) — Malware RE fundamentals
- "The Art of Exploitation" (Erickson) — Low-level exploitation concepts
- "Blue Team Handbook: Incident Response Edition" (Murdoch) — IR reference
- "Threat Modeling: Designing for Security" (Shostack) — Threat modeling methodology

## Cross-References

- See `swipe-sources/open-source-tools.md` for tools used in training exercises
- See `swipe-sources/conference-talks.md` for educational conference content
- See `swipe-sources/community-forums.md` for study groups and peer learning
