# NotPetya Attack (2017)

## Incident Summary

| Field | Details |
|-------|---------|
| Name | NotPetya (also: ExPetr, Nyetya, GoldenEye) |
| Date | June 27, 2017 |
| Attribution | Russian military intelligence (GRU), Sandworm team (Unit 74455) |
| Attack Vector | Supply chain compromise of M.E.Doc (Ukrainian accounting software) |
| Propagation | EternalBlue (MS17-010) + Mimikatz-style credential harvesting + PsExec/WMIC |
| Impact | $10 billion+ in global damage (most destructive cyberattack in history at the time) |
| Nature | Wiper malware disguised as ransomware |
| Major Victims | Maersk ($300M), Merck ($870M), FedEx/TNT ($400M), Saint-Gobain ($384M), Mondelez ($188M) |

---

## Attack Narrative

### Supply Chain Compromise
- M.E.Doc is accounting software used by virtually every company doing business in Ukraine (~400,000 organizations)
- Attackers compromised M.E.Doc's software update infrastructure
- Malicious update pushed via legitimate M.E.Doc update mechanism on June 27, 2017
- Organizations' systems automatically downloaded and executed the payload through trusted update channel

### Propagation Mechanisms
NotPetya was engineered for maximum lateral spread using multiple propagation methods:

1. **EternalBlue (CVE-2017-0144)**: SMB vulnerability leaked from NSA by Shadow Brokers. Enabled worm-like spread without credentials across unpatched Windows systems.

2. **Credential Harvesting**: Mimikatz-equivalent module extracted credentials from memory on compromised hosts, then used those credentials to spread to additional systems.

3. **PsExec and WMIC**: Used harvested admin credentials for remote execution on systems patched against EternalBlue.

4. **DHCP Hijacking**: Manipulated DHCP responses to redirect network traffic.

This multi-vector propagation meant that even organizations with some patching were vulnerable -- a single unpatched system or a single compromised admin credential was sufficient to enable cascading spread.

### Destructive Payload
Despite displaying a ransom demand for $300 in Bitcoin:
- The "ransomware" component was non-functional by design
- The victim ID displayed was randomly generated and not tracked by attackers
- The encryption was irreversible -- there was no actual decryption mechanism
- The MBR (Master Boot Record) was overwritten, destroying boot capability
- The MFT (Master File Table) was encrypted, destroying filesystem structure
- **NotPetya was a wiper designed to destroy data, not a ransomware designed to extort**

### Global Impact Timeline
- **06:00 UTC June 27**: M.E.Doc update mechanism pushes malicious payload
- **Within hours**: Malware spreads through Ukrainian networks and via VPN connections to global networks
- **By end of day**: Major multinational corporations report massive IT outages worldwide
- Maersk (shipping): 49,000 laptops, 4,000+ servers destroyed. 10 days to rebuild IT infrastructure.
- Merck (pharmaceutical): Manufacturing disrupted for months. Unable to fulfill vaccine orders.
- FedEx/TNT Express: Operations crippled for weeks. Legacy TNT systems never fully recovered.
- Ukrainian government: Multiple ministries, state banks, power companies affected.

## Technical Analysis

### Infection Chain
```
M.E.Doc Update Server (compromised)
  |-> Legitimate update mechanism delivers malicious DLL
    |-> DLL executes with SYSTEM privileges
      |-> Enumerates local network (subnet scan)
      |-> Attempts EternalBlue against discovered hosts
      |-> Harvests credentials via Mimikatz-like module
      |-> Spreads via PsExec/WMIC using harvested creds
        |-> On each new host: repeat credential harvest + spread
          |-> After propagation delay: activate wiper payload
            |-> Overwrite MBR
            |-> Encrypt MFT
            |-> Force reboot -> system unrecoverable
```

### Why It Spread So Far, So Fast
- **Supply chain trust**: Organizations trusted M.E.Doc updates implicitly
- **Admin credential reuse**: A single domain admin credential compromised on one host could spread to every system in the domain
- **EternalBlue ubiquity**: Despite MS17-010 patch being available since March 2017, many systems were unpatched
- **Flat networks**: Insufficient segmentation allowed worm-like propagation across entire enterprises
- **VPN connections**: International offices connected via VPN to Ukrainian networks became conduits for global spread

## Lessons for Defensive Operations

### Supply Chain Security
- **Software supply chain is an existential risk vector**
- Validate software update integrity (code signing, hash verification)
- Monitor update mechanisms for anomalous behavior
- Segment systems running critical supply chain software
- Maintain SBOM (Software Bill of Materials) for all deployed software
- Consider application allowlisting to prevent unauthorized code execution

### Patch Management
- **EternalBlue patch was available for 3 months before NotPetya**
- Critical vulnerability patches must be deployed within emergency SLA
- WannaCry (May 2017) should have been sufficient warning to patch MS17-010
- Organizations that had patched EternalBlue still fell victim via credential-based spread

### Credential Security
- **Single domain admin credential compromise = total domain compromise**
- Implement tiered administration (separate admin accounts for workstations, servers, DCs)
- Deploy LAPS (Local Administrator Password Solution) or equivalent
- Enable Credential Guard on Windows endpoints
- Restrict credential caching on endpoints
- Implement PAM with just-in-time access for admin privileges

### Network Segmentation
- Segment networks to limit blast radius of worm-like propagation
- Restrict SMB traffic between workstation subnets (workstations should not need to talk to each other via SMB)
- Implement internal firewalls between business units
- Monitor east-west traffic for anomalous lateral movement

### Backup and Recovery
- Maersk recovered because they found a single domain controller in Ghana that was offline during the attack
- **Air-gapped, offline backups are essential** for recovery from destructive attacks
- Practice bare-metal recovery at scale
- Maintain offline copies of Active Directory
- Test AD forest recovery procedures regularly

### Ransomware vs. Wiper Distinction
- Do not assume ransomware is ransomware -- it may be a wiper in disguise
- Focus on prevention and recovery rather than payment
- The ransom payment mechanism was non-functional; paying would not have helped

## Geopolitical Context
- NotPetya was part of Russia's ongoing cyber campaign against Ukraine
- Launched on the eve of Ukrainian Constitution Day
- Previous attacks included BlackEnergy (power grid, 2015), Industroyer (power grid, 2016)
- Collateral damage to global corporations was likely intentional or accepted
- US, UK, and multiple governments formally attributed NotPetya to Russia's GRU in 2018
- Demonstrated that cyberattacks targeting one nation can cause global economic damage

## Cross-References

- `workflows/ransomware-preparedness.md` — Ransomware/wiper defense
- `workflows/third-party-risk-assessment.md` — Supply chain risk
- `archive/notable-breaches/kaseya-2021.md` — Another supply chain attack
- `frameworks/lateral-movement-methodology.md` — Lateral movement techniques
- `frameworks/credential-attack-methodology.md` — Credential-based attacks
- `workflows/zero-trust-implementation.md` — Segmentation and zero trust
