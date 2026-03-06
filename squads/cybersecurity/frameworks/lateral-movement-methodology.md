# Lateral Movement Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de capacidade de movimentacao lateral em redes corporativas.
Abrange tecnicas baseadas em credenciais, protocolos de gerenciamento remoto e
ambientes hibridos (on-premises e cloud). Requer autorizacao explicita para cada segmento.

## Requisitos de Autorizacao
- Aprovacao para movimentacao entre segmentos de rede especificos
- Lista de sistemas autorizados para tentativas de acesso lateral
- Janela de teste acordada com equipes de operacao e monitoramento
- Notificacao previa ao SOC para evitar falsos positivos operacionais
- Limites claros de profundidade e amplitude de movimentacao

## Etapas da Metodologia

### 1. Reconhecimento de Rede Interna
- Mapeamento de subnets, VLANs e segmentacao de rede
- Identificacao de sistemas acessiveis a partir do foothold inicial
- Enumeracao de servicos expostos internamente (SMB, RDP, WinRM, SSH)
- Descoberta de relacoes de confianca entre dominios e florestas

### 2. Pass-the-Hash / Pass-the-Ticket
- Reutilizacao de NTLM hashes para autenticacao em hosts remotos
- Utilizacao de TGT/TGS tickets para acesso Kerberos-based
- Overpass-the-Hash para obter tickets a partir de hashes NTLM
- Validacao de acesso em cada host antes de prosseguir

### 3. Remote Execution Protocols
- PsExec: execucao remota via SMB (requer admin share access)
- WMI: execucao via Windows Management Instrumentation
- WinRM: PowerShell remoting para execucao de comandos
- SSH: movimentacao em ambientes Linux e dispositivos de rede
- DCOM: Distributed COM para execucao remota alternativa

### 4. RDP e Remote Access
- Sessoes RDP com credenciais obtidas ou hashes (Restricted Admin mode)
- Hijacking de sessoes RDP ativas (requer SYSTEM privileges)
- VNC e outros protocolos de acesso remoto identificados

### 5. Service Account Pivoting
- Identificacao de service accounts com acesso a multiplos sistemas
- Reutilizacao de credenciais de servico para pivoteamento
- Exploracao de managed service accounts e group managed accounts

### 6. Cloud Cross-Account Movement
- Abuso de roles com trust relationships entre contas cloud
- Pivoteamento via shared resources (S3, Azure Blob, GCS)
- Exploracao de VPC peering e service endpoints compartilhados
- Movimentacao entre ambientes on-premises e cloud via federation

## Ferramentas de Referencia
- CrackMapExec, Impacket (psexec/wmiexec/smbexec), Mimikatz, Rubeus
- Evil-WinRM, Chisel (tunneling), Ligolo-ng, SSH, BloodHound

## Contrapartida de Deteccao (Blue Team)
- Monitoramento de Event ID 4648 (explicit credential logon) e 4624 type 3
- Deteccao de uso anomalo de administrative shares (C$, ADMIN$)
- Alertas para PsExec service creation (Event ID 7045)
- Correlacao de logons simultaneos de mesma conta em multiplos hosts
- Network traffic analysis para tunneling e protocolos inesperados

## Integracao com Outros Frameworks
- Recebe de: credential-attack-methodology.md (credenciais validas)
- Recebe de: privilege-escalation-methodology.md (privilegios elevados)
- Alimenta: persistence-analysis-methodology.md (acesso sustentado)
- Alimenta: exfiltration-detection-methodology.md (acesso a dados)
