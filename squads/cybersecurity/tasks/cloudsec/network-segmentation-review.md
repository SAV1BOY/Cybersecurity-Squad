# Task: Network Segmentation Review

## Objetivo
Revisar a segmentacao de rede em ambientes cloud, verificando isolamento entre workloads, enforcement de zero trust e eficacia dos controles de rede.

## Agents
- **omar-santos** (lead) — Avalia segmentacao de rede cloud
- **cartographer** (support) — Mapeia topologia de rede

## Inputs
- Arquitetura de rede cloud (VPCs, subnets, peering)
- Security groups e NACLs/NSGs existentes
- Network diagrams e data flow maps
- Zero Trust Architecture como referencia

## Steps
1. Mapear topologia de rede: VPCs, subnets, peering, transit gateway
2. Revisar security groups e network ACLs por workload
3. Identificar regras excessivamente permissivas (0.0.0.0/0, any:any)
4. Verificar isolamento entre ambientes (prod, staging, dev)
5. Avaliar segmentacao entre workloads de diferentes trust levels
6. Verificar enforcement de private endpoints para servicos cloud
7. Auditar DNS resolution e egress filtering
8. Testar lateral movement paths entre segmentos
9. Documentar findings com recomendacoes de hardening
10. Registrar findings no `findings-registry`

## Output
- Mapa de segmentacao de rede com analise de gaps
- Lista de regras excessivamente permissivas
- Recomendacoes de segmentacao e isolamento
- Registro no `findings-registry`

## Quality Gates
- [ ] Topologia de rede completamente mapeada
- [ ] Security groups e ACLs revisados por workload
- [ ] Regras permissivas identificadas e documentadas
- [ ] Isolamento entre ambientes verificado
- [ ] Private endpoints avaliados para servicos criticos
- [ ] Checklist `cloud-network-segmentation` 100% atendido
