# Control Taxonomy

Taxonomia de controles de seguranca para categorizacao e mapeamento entre frameworks.

## Classificacao por Funcao

### Preventive Controls
Impedem que ameacas se concretizem.
| Control | Tipo | Exemplos |
|---------|------|---------|
| Access Control | Technical | MFA, RBAC, network ACLs |
| Encryption | Technical | TLS, AES-256, disk encryption |
| Input Validation | Technical | Parameterized queries, sanitization |
| Security Awareness | Administrative | Phishing training, secure coding |
| Physical Security | Physical | Biometria, cameras, locks |

### Detective Controls
Identificam ameacas ativas ou incidentes em andamento.
| Control | Tipo | Exemplos |
|---------|------|---------|
| SIEM | Technical | Log correlation, alerting |
| EDR | Technical | Process monitoring, behavioral analysis |
| IDS/IPS | Technical | Network traffic analysis |
| Vulnerability Scanning | Technical | DAST, SAST, infrastructure scanning |
| Audit Logs | Technical | Access logs, change logs |

### Corrective Controls
Minimizam impacto e restauram operacoes normais.
| Control | Tipo | Exemplos |
|---------|------|---------|
| Incident Response | Administrative | Playbooks, IR team |
| Backup/Restore | Technical | Immutable backups, DR plan |
| Patch Management | Technical | Automated patching, hotfixes |
| Containment | Technical | Network isolation, account lockout |

### Deterrent Controls
Desencorajam atacantes de tentar explorar.
| Control | Tipo | Exemplos |
|---------|------|---------|
| Warning Banners | Administrative | Login banners legais |
| Security Policies | Administrative | AUP, consequence communication |
| Honeypots | Technical | Decoy systems, honey tokens |

## Mapeamento Cross-Framework

| NIST CSF | ISO 27001 | CIS Controls | SOC 2 |
|----------|-----------|-------------|-------|
| PR.AC | A.9 | CIS 5, 6 | CC6.1 |
| PR.DS | A.10, A.18 | CIS 3 | CC6.7 |
| DE.CM | A.12 | CIS 8 | CC7.2 |
| RS.RP | A.16 | CIS 17 | CC7.3 |

## Uso

Ao implementar ou auditar controles, usar esta taxonomia para garantir
cobertura adequada de controles preventivos, detectivos e corretivos.
