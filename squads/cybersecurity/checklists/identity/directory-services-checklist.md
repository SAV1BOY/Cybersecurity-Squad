# Directory Services Security Checklist

## Purpose

Security checklist for Active Directory and LDAP environments covering GPO review, trust relationships, Kerberos configuration, and monitoring. Addresses common AD attack vectors and hardening measures.

## Domain Controller Security

### DC Hardening

- [ ] Domain controllers are dedicated servers (no other roles)
- [ ] DCs run latest supported OS version with current patches
- [ ] DCs are physically secured (restricted access rooms)
- [ ] DC backups are encrypted and access-controlled
- [ ] DCs have host-based firewall restricting unnecessary ports
- [ ] USB devices blocked on DCs (GPO or endpoint control)
- [ ] Print spooler service disabled on DCs
- [ ] Remote Desktop restricted to authorized admin workstations only
- [ ] PowerShell Constrained Language Mode enabled on DCs
- [ ] Script Block Logging enabled on DCs
- [ ] AppLocker/WDAC enabled on DCs
- [ ] LSASS configured as Protected Process (RunAsPPL)
- [ ] Credential Guard enabled on DCs (if compatible)

### DC Network Security

- [ ] DCs on dedicated management VLAN/subnet
- [ ] DC-to-DC replication on dedicated network (if possible)
- [ ] No internet access from DCs (proxy for updates only)
- [ ] LDAP signing required (domain controller: LDAP server signing requirements = Require signing)
- [ ] LDAP channel binding required
- [ ] SMB signing required on DCs
- [ ] NTLMv1 disabled (LmCompatibilityLevel = 5)
- [ ] Unnecessary protocols disabled (LLMNR, NetBIOS, WPAD)
- [ ] DNS secured (dynamic update restricted, DNS logging enabled)

## Group Policy (GPO) Security

### GPO Review

- [ ] All GPOs documented with purpose and owner
- [ ] Default Domain Policy limited to password and account lockout only
- [ ] Default Domain Controllers Policy reviewed and hardened
- [ ] No GPOs link to entire domain unless necessary
- [ ] GPO permissions restrict who can modify (GPO creator owners reviewed)
- [ ] GPO delegations reviewed quarterly
- [ ] Unlinked/orphaned GPOs identified and removed
- [ ] GPO backup and versioning in place
- [ ] GPO change monitoring enabled (SIEM alert on GPO modification)

### Critical GPO Settings

| Setting | Recommended Value | Verified |
|---------|-------------------|----------|
| Minimum password length | 14+ characters | [ ] |
| Password complexity | Enabled | [ ] |
| Account lockout threshold | 5-10 attempts | [ ] |
| Account lockout duration | 30 minutes | [ ] |
| Audit logon events | Success and Failure | [ ] |
| Audit account management | Success and Failure | [ ] |
| Audit directory service access | Success and Failure | [ ] |
| Audit policy change | Success and Failure | [ ] |
| Audit privilege use | Success and Failure | [ ] |
| Audit process creation | Success | [ ] |
| Include command line in process creation events | Enabled | [ ] |
| Network access: Do not allow anonymous enumeration of SAM accounts | Enabled | [ ] |
| Network security: LAN Manager authentication level | Send NTLMv2 response only. Refuse LM & NTLM | [ ] |
| Network security: LDAP client signing requirements | Require signing | [ ] |

## Trust Relationships

### Trust Review

- [ ] All domain/forest trusts documented
- [ ] Each trust has a documented business justification
- [ ] Trust directions are correct (one-way where possible)
- [ ] Trust transitivity is appropriate (non-transitive preferred)
- [ ] SID filtering enabled on all trusts (prevent SID history abuse)
- [ ] Selective authentication enabled where appropriate
- [ ] Trust passwords rotated regularly (automated by AD, verify not broken)
- [ ] External trusts minimized and reviewed quarterly
- [ ] Forest trusts reviewed annually with trust owners

### Trust Risk Assessment

| Trust Type | Risk | Review Frequency |
|-----------|------|-----------------|
| Forest trust (same org) | Medium | Annually |
| Forest trust (external org) | High | Quarterly |
| External domain trust | High | Quarterly |
| Realm trust (Kerberos) | Medium-High | Semi-annually |
| Shortcut trust | Low | Annually |

## Kerberos Configuration

### Kerberos Hardening

- [ ] AES encryption enforced for Kerberos (RC4/DES disabled)
- [ ] Kerberos ticket lifetime: TGT maximum 10 hours
- [ ] Kerberos ticket renewal: Maximum 7 days
- [ ] Pre-authentication required for all accounts
- [ ] Kerberos delegation reviewed (no unconstrained delegation except DCs)
- [ ] Constrained delegation uses protocol transition only where needed
- [ ] Resource-based constrained delegation reviewed
- [ ] KRBTGT password rotated twice (at least annually)
- [ ] Service accounts with SPNs reviewed (Kerberoasting targets)
- [ ] Service accounts with SPNs use AES encryption and long passwords (30+)

### Kerberos Attack Prevention

| Attack | Prevention | Detection | Verified |
|--------|-----------|-----------|----------|
| Kerberoasting | AES encryption, long SPN passwords, gMSA | 4769 with RC4 encryption type | [ ] |
| AS-REP Roasting | Pre-authentication required on all accounts | 4768 without pre-auth | [ ] |
| Golden Ticket | KRBTGT rotation, Credential Guard | Anomalous TGT lifetime/renewal | [ ] |
| Silver Ticket | Service account password rotation, PAC validation | Anomalous service ticket | [ ] |
| DCSync | Restrict Replicating Directory Changes right | 4662 with replication GUIDs | [ ] |
| Pass-the-Hash | Credential Guard, admin tiering | 4624 Type 9 with admin accounts | [ ] |
| Pass-the-Ticket | Session isolation, short ticket lifetime | Ticket reuse from different host | [ ] |
| Skeleton Key | LSASS protection, DC integrity monitoring | LSASS modification detection | [ ] |

## Administrative Tiering

### Tier Model

| Tier | Assets | Admin Account Type | Verified |
|------|--------|-------------------|----------|
| Tier 0 | Domain controllers, AD, PKI, SIEM | Tier 0 admin (most restricted) | [ ] |
| Tier 1 | Servers, applications, databases | Tier 1 admin (server-level) | [ ] |
| Tier 2 | Workstations, end-user devices | Tier 2 admin (workstation-level) | [ ] |

### Tiering Enforcement

- [ ] Tier 0 admins can only log on to Tier 0 systems
- [ ] Tier 1 admins cannot log on to Tier 0 or Tier 2 systems
- [ ] Tier 2 admins cannot log on to Tier 0 or Tier 1 systems
- [ ] Privileged Access Workstations (PAWs) used for Tier 0 administration
- [ ] Authentication silos/policies enforce tiering
- [ ] Admin accounts do not have email or internet access
- [ ] Admin accounts are separate from daily-use accounts
- [ ] Protected Users security group used for admin accounts

## Monitoring

### AD Security Monitoring

| Event ID | Description | Alert Level |
|----------|-------------|-------------|
| 4720 | User account created | Medium |
| 4726 | User account deleted | Medium |
| 4728/4732/4756 | Member added to security group | High (privileged groups: Critical) |
| 4729/4733/4757 | Member removed from security group | Medium |
| 4738 | User account changed | Medium |
| 4662 | Operation performed on directory object | High (monitor for DCSync) |
| 4768 | Kerberos TGT requested | Monitor (AS-REP roasting) |
| 4769 | Kerberos service ticket requested | Monitor (Kerberoasting) |
| 4771 | Kerberos pre-authentication failed | Medium |
| 4776 | NTLM authentication | Medium (should be decreasing) |
| 5136 | Directory object modified | High (schema/config changes) |
| 5141 | Directory object deleted | High |
| 4670 | Permissions changed on object | High |

### Critical Group Monitoring

- [ ] Domain Admins membership changes alert immediately
- [ ] Enterprise Admins membership changes alert immediately
- [ ] Schema Admins membership changes alert immediately
- [ ] Account Operators membership changes alert
- [ ] Server Operators membership changes alert
- [ ] Backup Operators membership changes alert
- [ ] Group Policy Creator Owners membership changes alert
- [ ] DNSAdmins membership changes alert (DLL injection risk)

## Operational Security

- [ ] AD recovery plan documented and tested (bare metal, backup-based)
- [ ] AD recovery tested semi-annually
- [ ] AD schema changes require change management board approval
- [ ] AD forest recovery plan addresses ransomware scenario
- [ ] AD replication health monitored
- [ ] Time synchronization verified across all DCs
- [ ] Certificate services (if present) secured and monitored
- [ ] Azure AD Connect security reviewed (if hybrid)
- [ ] SYSVOL permissions reviewed (no sensitive data in GPO preferences)

## Cross-References

- [Active Directory Attack Defense](../../frameworks/active-directory-attack-defense.md) -- attack methodology
- [Privileged Access Checklist](privileged-access-checklist.md) -- PAM for AD admins
- [Service Account Checklist](service-account-checklist.md) -- AD service accounts
- [Credential Attack Methodology](../../frameworks/credential-attack-methodology.md) -- credential attacks
