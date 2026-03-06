# MITRE ATT&CK e Frameworks - Indice de Referencia

## Visao Geral
MITRE Corporation mantem frameworks essenciais para cybersecurity, sendo o
ATT&CK o mais influente. O squad utiliza frameworks MITRE como linguagem
comum para descrever ameacas e avaliar cobertura de deteccao.

## MITRE ATT&CK
Knowledge base de taticas, tecnicas e procedimentos (TTPs) de adversarios
baseada em observacoes do mundo real.

### Matrizes Principais
- **Enterprise**: Windows, macOS, Linux, Cloud, Network, Containers
- **Mobile**: Android, iOS
- **ICS**: Industrial Control Systems

### Taticas (Enterprise)
1. Reconnaissance (TA0043)
2. Resource Development (TA0042)
3. Initial Access (TA0001)
4. Execution (TA0002)
5. Persistence (TA0003)
6. Privilege Escalation (TA0004)
7. Defense Evasion (TA0005)
8. Credential Access (TA0006)
9. Discovery (TA0007)
10. Lateral Movement (TA0008)
11. Collection (TA0009)
12. Command and Control (TA0011)
13. Exfiltration (TA0010)
14. Impact (TA0040)

## MITRE D3FEND
Knowledge graph de contramedidas defensivas mapeadas para ATT&CK.
- Uso: identificar defesas apropriadas para cada tecnica de ataque

## MITRE CALDERA
Plataforma de adversary emulation automatizada.
- Uso: simular ataques de forma automatizada usando ATT&CK

## MITRE ENGAGE
Framework para adversary engagement operations.
- Uso: planejar operacoes de deception e denial

## Como o Squad Aplica
- **Detection Engineering**: mapear regras de deteccao para ATT&CK
- **Threat Hunting**: priorizar hunts por tecnica ATT&CK
- **Red Team**: planejar operacoes usando ATT&CK como guia
- **Gap Analysis**: identificar tecnicas sem cobertura de deteccao
- **Reporting**: usar ATT&CK como taxonomia em relatorios
- **Purple Team**: exercicios estruturados por tecnica

## Ferramentas Complementares
- ATT&CK Navigator: visualizacao de cobertura
- Atomic Red Team: testes atomicos por tecnica
- SIGMA rules: deteccoes mapeadas para ATT&CK

## Notas do Squad
Manter um heat map de cobertura de deteccao no ATT&CK Navigator atualizado.
Priorizar tecnicas mais observadas em threat intel relevante ao contexto.
