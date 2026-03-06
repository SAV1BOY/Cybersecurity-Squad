# Threat Taxonomy

Taxonomia de ameacas para classificacao de threat actors, motivacoes e capacidades.

## Threat Actor Categories

### Nation-State (APT)
- **Motivacao**: Espionagem, sabotagem, vantagem geopolitica
- **Capacidade**: Alta - recursos ilimitados, zero-days, supply chain
- **Persistencia**: Muito alta - meses a anos de dwell time
- **Exemplos**: APT28 (Fancy Bear), APT29 (Cozy Bear), Lazarus Group
- **Alvos tipicos**: Governo, defesa, infraestrutura critica, tech

### Cybercrime Organizations
- **Motivacao**: Financeira - ransomware, fraude, extorsao
- **Capacidade**: Media-alta - RaaS, exploit kits, social engineering
- **Persistencia**: Media - suficiente para monetizar acesso
- **Exemplos**: LockBit, ALPHV/BlackCat, Cl0p
- **Alvos tipicos**: Qualquer organizacao com capacidade de pagamento

### Hacktivists
- **Motivacao**: Ideologica, politica, protesto social
- **Capacidade**: Baixa-media - DDoS, defacement, data leaks
- **Persistencia**: Baixa - acoes pontuais e oportunistas
- **Exemplos**: Anonymous, Lulzsec
- **Alvos tipicos**: Governos, corporacoes controversas

### Insider Threat
- **Motivacao**: Financeira, vinganca, negligencia, recrutamento
- **Capacidade**: Variavel - acesso privilegiado ja existente
- **Persistencia**: Alta - acesso legitimo dificulta deteccao
- **Tipos**: Malicioso, negligente, comprometido

### Script Kiddies
- **Motivacao**: Curiosidade, reconhecimento, diversao
- **Capacidade**: Baixa - ferramentas publicas, exploits conhecidos
- **Persistencia**: Baixa - desistem ante resistencia minima

## Threat Classification por MITRE ATT&CK

| Tactic | Descricao | Tecnicas Comuns |
|--------|-----------|----------------|
| Initial Access | Entrada no ambiente | Phishing, Exploit Public App |
| Execution | Execucao de codigo | PowerShell, Command Line |
| Persistence | Manter acesso | Registry Keys, Scheduled Tasks |
| Privilege Escalation | Elevar privilegios | Exploitation, Token Manipulation |
| Defense Evasion | Evitar deteccao | Obfuscation, Rootkits |
| Credential Access | Obter credenciais | Brute Force, Credential Dumping |
| Lateral Movement | Mover-se internamente | SMB, RDP, WMI |
| Exfiltration | Extrair dados | DNS Tunneling, Cloud Storage |

## Uso

Classificar ameacas consistentemente para priorizar defesas conforme
o threat landscape relevante ao setor e perfil da organizacao.
