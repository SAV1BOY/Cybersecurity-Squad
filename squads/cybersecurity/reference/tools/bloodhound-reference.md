# BloodHound / SharpHound Reference

## Purpose

Operational reference for BloodHound and its data collection component SharpHound, the essential Active Directory attack path analysis platform. Covers collection methods, graph analysis, privilege escalation path identification, and Cypher query techniques for authorized AD security assessments.

## Architecture

BloodHound uses a Neo4j graph database to map relationships between AD objects (users, groups, computers, GPOs, OUs) and identify attack paths from compromised positions to high-value targets.

### Components

| Component | Role |
|-----------|------|
| BloodHound GUI | Graph visualization and query interface |
| SharpHound | C# data collector for AD enumeration |
| AzureHound | Azure AD data collector |
| Neo4j | Graph database backend |
| BloodHound CE | Community Edition with API-first architecture |

## SharpHound Collection Methods

### Collection Flags

| Method | Flag | Data Collected | Noise Level |
|--------|------|---------------|-------------|
| Default | `-c Default` | Group memberships, sessions, ACLs, trusts | Medium |
| All | `-c All` | Everything including GPO, container, cert | High |
| Session | `-c Session` | Active logon sessions only | Low |
| LoggedOn | `-c LoggedOn` | Privileged logon session enumeration | Medium |
| Group | `-c Group` | Group memberships only | Low |
| ACL | `-c ACL` | Access control entries | Medium |
| ObjectProps | `-c ObjectProps` | Object properties (descriptions, SPNs) | Low |
| DCOnly | `-c DCOnly` | Queries only DCs via LDAP (stealthiest) | Very Low |
| CertServices | `-c CertServices` | AD Certificate Services configuration | Low |

### Collection Commands

```powershell
# Standard collection (domain-joined machine)
.\SharpHound.exe -c All --outputdirectory C:\temp

# DCOnly for stealth (LDAP only, no SMB)
.\SharpHound.exe -c DCOnly --outputdirectory C:\temp

# Target specific domain
.\SharpHound.exe -c All -d target.local --ldapusername user --ldappassword pass

# Loop collection for session data over time
.\SharpHound.exe -c Session --loop --loopduration 08:00:00 --loopinterval 00:10:00

# Stealth mode (slower, avoids detection)
.\SharpHound.exe -c All --stealth --throttle 1000 --jitter 30
```

### Python Collector (Linux)

```bash
# bloodhound-python for remote collection
bloodhound-python -u user -p password -d domain.local -ns dc_ip -c all
bloodhound-python -u user -p password -d domain.local -c DCOnly --dns-tcp
```

## Attack Path Analysis

### Pre-Built Analytics (BloodHound GUI)

| Query | Finds |
|-------|-------|
| Find all Domain Admins | Maps DA group membership |
| Find Shortest Paths to Domain Admins | Critical attack chains |
| Find Principals with DCSync Rights | Replication privilege abuse |
| Find Computers with Unsupported OS | Legacy system risk |
| Find Kerberoastable Users | SPN-based hash extraction targets |
| Find AS-REP Roastable Users | Pre-auth disabled accounts |
| Find Shortest Paths to High-Value Targets | Paths to HVTs |
| Show All GPO Permissions | GPO-based privilege escalation |

### Key Attack Path Types

1. **Group Membership Chains**: User -> Group -> Nested Group -> Domain Admins
2. **ACL-Based Paths**: User has GenericAll/WriteDacl on target -> Modify permissions -> Escalate
3. **Session-Based Paths**: Admin logged into compromised machine -> Token theft -> Lateral movement
4. **GPO Abuse**: Write access to GPO linked to privileged OU -> Deploy malicious settings
5. **Certificate Abuse (ESC1-ESC8)**: Misconfigured templates -> Certificate-based privilege escalation
6. **Kerberos Delegation**: Unconstrained/constrained delegation -> Ticket forwarding abuse

## Custom Cypher Queries

### Reconnaissance Queries

```cypher
// Find all users with admin count set
MATCH (u:User {admincount: true}) RETURN u.name

// Find all computers running specific OS
MATCH (c:Computer) WHERE c.operatingsystem =~ "(?i).*windows server 2012.*"
RETURN c.name, c.operatingsystem

// Find users with passwords not required
MATCH (u:User {passwordnotreqd: true}) RETURN u.name

// Find users with passwords that never expire
MATCH (u:User {pwdneverexpires: true, enabled: true}) RETURN u.name

// Find all user descriptions (may contain passwords)
MATCH (u:User) WHERE u.description IS NOT NULL
RETURN u.name, u.description
```

### Privilege Escalation Queries

```cypher
// Shortest path from owned principals to Domain Admins
MATCH p=shortestPath((n {owned: true})-[*1..]->(m:Group {name: "DOMAIN ADMINS@DOMAIN.LOCAL"}))
RETURN p

// Users with DCSync rights
MATCH (n)-[:MemberOf|GetChanges*1..]->(d:Domain)
MATCH (n)-[:MemberOf|GetChangesAll*1..]->(d)
RETURN n.name

// Find all GenericAll permissions to Domain Admins
MATCH p=(n)-[:GenericAll]->(m:Group {name: "DOMAIN ADMINS@DOMAIN.LOCAL"})
RETURN p

// Kerberoastable users with path to high-value targets
MATCH (u:User {hasspn: true, enabled: true})
MATCH p=shortestPath((u)-[*1..]->(g:Group {highvalue: true}))
RETURN u.name, LENGTH(p)
ORDER BY LENGTH(p) ASC

// Computers with unconstrained delegation
MATCH (c:Computer {unconstraineddelegation: true})
WHERE NOT c.name STARTS WITH "DC"
RETURN c.name
```

### Lateral Movement Queries

```cypher
// Find all sessions on a specific computer
MATCH (u:User)-[:HasSession]->(c:Computer {name: "TARGET.DOMAIN.LOCAL"})
RETURN u.name

// Find computers where Domain Admins have sessions
MATCH (u:User)-[:MemberOf*1..]->(g:Group {name: "DOMAIN ADMINS@DOMAIN.LOCAL"})
MATCH (u)-[:HasSession]->(c:Computer)
RETURN DISTINCT c.name

// Shortest path between two nodes
MATCH p=shortestPath((a {name: "OWNED_USER@DOMAIN.LOCAL"})-[*1..]->(b {name: "TARGET@DOMAIN.LOCAL"}))
RETURN p
```

## Marking and Tracking

```
# In BloodHound GUI:
# Right-click node > Mark as Owned (compromised principals)
# Right-click node > Mark as High Value (custom HVTs)

# Track attack progress by marking owned nodes
# Re-run shortest path queries from owned to targets
```

## OPSEC Considerations

| Collection Type | Detection Risk | Mitigations |
|----------------|---------------|-------------|
| LDAP queries | Low (normal AD traffic) | Use DCOnly |
| SMB session enum | Medium (touches all machines) | Use Session loop at low frequency |
| ACL enumeration | Medium | Avoid during business hours |
| Full All collection | High | Break into targeted collections |

## Cross-References

- See `frameworks/active-directory-attack-defense.md` for AD methodology
- See `reference/tools/metasploit-reference.md` for exploitation of discovered paths
- See `frameworks/credential-attack-methodology.md` for credential harvesting
- See `frameworks/lateral-movement-methodology.md` for movement techniques
- See `frameworks/privilege-escalation-methodology.md` for escalation strategies
