# Cloud - Network Segmentation

Checklist para auditoria de segmentacao de rede em cloud.

## VPC/VNet Architecture
- [ ] VPCs/VNets segregados por environment (prod, staging, dev)
- [ ] CIDR ranges planejados sem sobreposicao
- [ ] Subnets publicas e privadas claramente separadas
- [ ] Subnets dedicadas para cada tier (web, app, data)
- [ ] Internet Gateway apenas em VPCs que necessitam
- [ ] NAT Gateway configurado para subnets privadas
- [ ] VPC Flow Logs habilitados em todas as VPCs

## Security Groups e NACLs
- [ ] Security groups com regras restritivas (nao 0.0.0.0/0 ingress)
- [ ] Default security group sem regras permissivas
- [ ] NACLs configurados como defense-in-depth
- [ ] Regras de security group referenciando outros SGs (nao IPs)
- [ ] Unused security groups identificados e removidos
- [ ] Overly permissive rules documentadas e justificadas
- [ ] Egress filtering implementado para subnets sensiveis

## Conectividade Inter-VPC
- [ ] VPC peering connections inventariadas e justificadas
- [ ] Transit gateway configuration auditada
- [ ] Routing tables revisadas para least access
- [ ] Cross-account peering aprovado e documentado
- [ ] Peering nao expoe subnets desnecessarias
- [ ] Route propagation controlada e auditada

## Conectividade Hibrida
- [ ] VPN connections inventariadas com endpoints
- [ ] Direct Connect/ExpressRoute configuration auditada
- [ ] On-premise routes propagadas controladamente
- [ ] Split tunneling configuration revisada
- [ ] Firewall entre on-premise e cloud configurado
- [ ] DNS resolution entre ambientes controlada

## Servicos de Seguranca de Rede
- [ ] WAF configurado para web applications publicas
- [ ] DDoS protection habilitada (Shield, Azure DDoS)
- [ ] Network firewall (AWS Network Firewall, Azure Firewall) avaliado
- [ ] IDS/IPS para cloud traffic configurado
- [ ] DNS filtering implementado
- [ ] Private endpoints para servicos PaaS configurados

## Validacao e Teste
- [ ] Network connectivity matrix testada (who can talk to whom)
- [ ] Segmentacao validada via network scanning
- [ ] Unauthorized paths identificados e bloqueados
- [ ] Lateral movement entre environments testado
- [ ] Micro-segmentation avaliada para workloads criticos
- [ ] Report de segmentacao com findings e recommendations
- [ ] Diagrama de rede atualizado com segmentation boundaries
