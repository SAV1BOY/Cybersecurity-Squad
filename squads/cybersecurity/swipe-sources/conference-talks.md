# Security Conference Talks

## Purpose

This curated list highlights must-watch security conference talks organized by topic and skill level. Conference talks are where cutting-edge research is first presented, novel attack techniques are demonstrated, and industry leaders share hard-won operational experience. This list prioritizes talks with lasting educational value over time-sensitive news.

## Major Conferences

### DEF CON
- **URL**: https://www.defcon.org/ | Recordings: https://www.youtube.com/@DEFCONConference
- **Profile**: The largest and longest-running hacker conference. Talks range from highly technical exploit development to policy and social engineering.
- **Skill Level**: Beginner to Expert (varies by talk and village)
- **Best For**: Offensive security, hardware hacking, social engineering, IoT security, village-specific deep dives

### Black Hat
- **URL**: https://www.blackhat.com/ | Recordings: https://www.youtube.com/@BlackHatOfficialYT
- **Profile**: More corporate and polished than DEF CON. Briefings are peer-reviewed and tend toward novel research. Training sessions are world-class but expensive.
- **Skill Level**: Intermediate to Expert
- **Best For**: Cutting-edge vulnerability research, enterprise security, emerging attack surfaces

### BSides (Various Cities)
- **URL**: http://www.securitybsides.com/
- **Profile**: Community-organized, regional conferences. More accessible and diverse in topics. BSides Las Vegas, San Francisco, and London are particularly strong.
- **Skill Level**: Beginner to Advanced
- **Best For**: Practical operational talks, career development, community building, blue team content

### Chaos Communication Congress (CCC)
- **URL**: https://www.ccc.de/en/ | Recordings: https://media.ccc.de/
- **Profile**: European hacker conference with strong political and philosophical dimensions alongside deeply technical content.
- **Skill Level**: Intermediate to Expert
- **Best For**: Privacy, surveillance, infrastructure security, European perspective, hardware security

### ShmooCon
- **URL**: https://www.shmoocon.org/
- **Profile**: Smaller, community-focused conference in Washington, D.C.
- **Skill Level**: Intermediate
- **Best For**: Government/policy intersection with security, practical offensive and defensive talks

### SANS Summits
- **URL**: https://www.sans.org/cyber-security-summit/
- **Profile**: Focused summits on specific topics (threat hunting, cloud security, ICS, etc.)
- **Skill Level**: Intermediate to Advanced
- **Best For**: Topic-specific deep dives, practitioner-focused content, blue team operations

## Must-Watch Talks by Topic

### Offensive Security and Exploitation

| Talk | Speaker | Conference | Why Watch |
|------|---------|------------|-----------|
| "Hacking Google" (series) | Various | Google/YouTube | Inside look at Google's security operations and red teaming |
| "An Ice-Cold Boot to Break Full Disk Encryption" | J. Alex Halderman | Princeton/USENIX | Foundational cold boot attack research |
| "Breaking the x86 ISA" | Domas | Black Hat | Undocumented x86 processor behavior exploitation |
| "Subverting Trust in Windows" | Matt Graeber | DerbyCon | Living-off-the-land and code signing abuse |
| "Hacking Embedded Devices" (various) | Travis Goodspeed, Joe Grand | DEF CON | Hardware hacking fundamentals and advanced techniques |

### Defense, Detection, and IR

| Talk | Speaker | Conference | Why Watch |
|------|---------|------------|-----------|
| "Hunting with Jupyter Notebooks" | Various | SANS Summit | Practical threat hunting with data science tools |
| "The Cycle of Cyber Threat Intelligence" | Various | SANS CTI Summit | Structured intelligence analysis for security teams |
| "Detecting the Elusive: Active Directory Threat Hunting" | Sean Metcalf | BSides/DerbyCon | AD attack detection strategies |
| "Purple Team Exercise Framework" | Various | MITRE ATT&CKcon | Structured approach to adversary emulation |
| "Incident Response is Dead, Long Live Incident Response" | Various | BSides | Modern IR challenges and approaches |

### Cloud and Modern Infrastructure

| Talk | Speaker | Conference | Why Watch |
|------|---------|------------|-----------|
| "Breaking and Fixing Kubernetes" | Various | KubeCon/Black Hat | Container and orchestration security |
| "Serverless Security: What's Left to Protect" | Various | Black Hat/BSides | Serverless attack surface analysis |
| "Identity is the New Perimeter" | Various | Fal.Con/RSA | Identity-centric security architecture |
| "Cloud Forensics: Nuts and Bolts" | Various | SANS Cloud Summit | Practical cloud IR methodology |

### Social Engineering and Human Factors

| Talk | Speaker | Conference | Why Watch |
|------|---------|------------|-----------|
| "Social Engineering: The Art of Human Hacking" | Christopher Hadnagy | DEF CON | Foundational social engineering concepts |
| "How I Rob Banks" | Various | DEF CON | Physical penetration testing and social engineering in practice |
| "The Science of Social Engineering" | Various | BSides | Psychological principles behind SE attacks |

### Policy, Privacy, and Strategy

| Talk | Speaker | Conference | Why Watch |
|------|---------|------------|-----------|
| "Cyberwar Is Not Coming" / "Cyberwar Is Here" | Thomas Rid / Various | CCC/Black Hat | Cyber conflict policy debate |
| "The Ethics of Vulnerability Disclosure" | Various | Black Hat | Responsible disclosure frameworks and debates |
| "Surveillance Capitalism and Security" | Various | CCC | Intersection of commercial surveillance and security |

## Viewing Recommendations by Role

### SOC Analyst (First 6 Months)
1. MITRE ATT&CK framework overview talks from ATT&CKcon
2. SANS blue team summit talks on detection engineering
3. Threat hunting methodology talks from SANS Threat Hunting Summit
4. Active Directory security talks from DerbyCon/BSides archives

### Penetration Tester (Skill Development)
1. DEF CON and Black Hat offensive talks in your specialty area
2. SANS Pen Test HackFest presentations
3. Wild West Hackin' Fest talks on practical offensive techniques
4. IppSec YouTube walkthroughs for hands-on technique learning

### Security Leader / Manager
1. RSA Conference keynotes and strategy tracks
2. SANS Leadership Summit presentations
3. BSides talks on building security programs
4. CCC talks for broader perspective on technology and society

## How to Get the Most from Conference Talks

1. **Watch actively**: Take notes, pause to research unfamiliar concepts, try to reproduce demonstrations in a lab
2. **Focus on methodology, not just tools**: Tools change; thinking frameworks persist
3. **Watch talks outside your specialty**: Offensive people should watch defensive talks and vice versa
4. **Organize watch parties**: Schedule team viewing sessions followed by discussion of applicability to your environment
5. **Build a library**: Maintain a shared playlist of talks that represent the team's baseline knowledge

## Free Recording Archives

| Source | URL | Notes |
|--------|-----|-------|
| DEF CON Media | https://media.defcon.org/ | Full archives including villages |
| CCC Media | https://media.ccc.de/ | Comprehensive European conference archive |
| Black Hat YouTube | https://www.youtube.com/@BlackHatOfficialYT | Selected briefings |
| BSides YouTube | Various per city | Search "BSides [city] [year]" |
| SANS Summit YouTube | https://www.youtube.com/@SANSInstitute | Summit recordings and webcasts |

## Cross-References

- See `swipe-sources/security-blogs-and-research.md` for written research sources
- See `swipe-sources/training-platforms.md` for hands-on learning to complement talk viewing
- See `swipe-sources/open-source-tools.md` for tools referenced in conference talks
