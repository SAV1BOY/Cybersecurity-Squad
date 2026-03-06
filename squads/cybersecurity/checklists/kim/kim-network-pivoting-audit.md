# Kim - Network Pivoting Audit

Checklist para auditoria de pivoting e movimentacao lateral em rede.

## Preparacao para Pivoting
- [ ] Network topology mapeada com subnets e segmentacao
- [ ] Compromised host(s) identificados como pivot points
- [ ] Interfaces de rede do pivot host enumeradas
- [ ] Routing table do pivot host analisada
- [ ] ARP cache do pivot host coletado para host discovery
- [ ] Firewall rules locais do pivot host revisadas
- [ ] Ferramentas de pivoting preparadas (Chisel, ligolo, SSH tunneling)

## Host Discovery via Pivot
- [ ] Ping sweep realizado em subnets acessiveis via pivot
- [ ] ARP scan executado em segments diretamente conectados
- [ ] Port scanning via pivot em hosts descobertos
- [ ] Service enumeration realizada em hosts de interesse
- [ ] Domain controllers e high-value targets identificados
- [ ] Subnets adicionais descobertas e documentadas

## Tecnicas de Pivoting
- [ ] SSH tunneling (local/remote/dynamic) testado
- [ ] SOCKS proxy configurado para acesso transparente
- [ ] Port forwarding configurado para servicos especificos
- [ ] Multi-hop pivoting testado (chaining pivots)
- [ ] DNS tunneling testado como canal alternativo
- [ ] ICMP tunneling avaliado para ambientes restritivos
- [ ] VPN pivoting via compromised gateway testado

## Lateral Movement
- [ ] Credential reuse testada entre hosts
- [ ] Pass-the-hash/pass-the-ticket executados (se credenciais disponiveis)
- [ ] WMI/DCOM lateral movement testado
- [ ] PSExec e alternativas testados
- [ ] RDP/SSH lateral movement documentado
- [ ] Admin shares (C$, ADMIN$) acessibilidade verificada
- [ ] Cada movimento lateral registrado com timestamp

## Segmentacao e Controles
- [ ] Network segmentation effectiveness avaliada
- [ ] Micro-segmentation bypass paths documentados
- [ ] Firewall rules entre segments testadas para gaps
- [ ] VLAN hopping tentado (se aplicavel)
- [ ] East-west traffic monitoring coverage avaliada
- [ ] Detection de lateral movement pelo blue team avaliada

## Documentacao e Cleanup
- [ ] Cada hop documentado com source, destination, method
- [ ] Network diagram atualizado com paths explorados
- [ ] Pivoting tools e tunnels removidos apos teste
- [ ] Temporary accounts removidos
- [ ] Recommendations de segmentacao documentadas
- [ ] Report de lateral movement paths entregue
