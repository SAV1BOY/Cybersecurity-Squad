# MITRE ATT&CK Mapping Examples

Exemplos praticos de mapeamento de deteccoes para o framework MITRE ATT&CK.

## Mapeamento por Tactic

### Initial Access (TA0001)
| Technique | Detection | Data Source |
|-----------|-----------|-------------|
| T1566.001 Spearphishing Attachment | Suspicious attachment types in email gateway | Email logs |
| T1566.002 Spearphishing Link | Click em URL reputacao baixa + download subsequente | Proxy logs |
| T1078 Valid Accounts | Login de localizacao impossivel (impossible travel) | Auth logs |

### Execution (TA0002)
| Technique | Detection | Data Source |
|-----------|-----------|-------------|
| T1059.001 PowerShell | Encoded command execution, bypass flags | EDR, Sysmon |
| T1204.002 Malicious File | Execucao de arquivo de diretorio temp pos-download | EDR |

### Lateral Movement (TA0008)
| Technique | Detection | Data Source |
|-----------|-----------|-------------|
| T1021.001 RDP | RDP de workstation para workstation (nao usual) | Network, Auth |
| T1550.002 Pass the Hash | NTLM auth anomala sem Kerberos previo | DC logs |

## Como Mapear Novos Findings

1. Identificar o comportamento observado
2. Consultar ATT&CK Navigator para technique match
3. Verificar sub-techniques para maior precisao
4. Documentar data sources necessarios
5. Validar cobertura com red team simulation

## Ferramentas de Apoio

- MITRE ATT&CK Navigator para visualizacao de cobertura
- DeTT&CT para modelagem de data sources
- Sigma rules como referencia de detection logic
- Atomic Red Team para validacao de deteccoes
