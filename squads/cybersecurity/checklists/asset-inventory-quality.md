# Asset Inventory Quality Gate

Checklist de qualidade para inventario de ativos e discovery.

## Network Discovery
- [ ] Network ranges identificados via ASN lookup e WHOIS
- [ ] DNS enumeration completa (subdomains, zone transfers)
- [ ] Reverse DNS realizado para todos os ranges
- [ ] Port scanning executado em todos os hosts descobertos
- [ ] Service fingerprinting realizado em portas abertas
- [ ] IPv6 ranges verificados alem de IPv4

## Host Classification
- [ ] Hosts categorizados por funcao (web, DB, mail, DNS)
- [ ] Operating system fingerprinting concluido
- [ ] Software versions documentadas por host
- [ ] Criticality rating atribuido a cada ativo
- [ ] Data classification associada a cada sistema

## Application Discovery
- [ ] Web applications enumeradas com URLs completas
- [ ] API endpoints catalogados
- [ ] Web technologies fingerprinted (frameworks, CMS, libraries)
- [ ] Authentication mechanisms identificados
- [ ] Third-party integrations mapeadas

## Cloud e Infra Complementar
- [ ] Cloud assets enumerados (S3 buckets, Azure blobs, GCP storage)
- [ ] CDN e load balancer configurations mapeadas
- [ ] Container registries e images catalogados
- [ ] Serverless functions identificadas
- [ ] SaaS applications em uso documentadas

## Validacao do Inventario
- [ ] Inventario cruzado com CMDB ou asset management existente
- [ ] Shadow IT identificado e documentado
- [ ] Ativos orphaned ou decommissioned sinalizados
- [ ] Owner atribuido a cada ativo descoberto
- [ ] Inventario exportado em formato estruturado (CSV, JSON)
- [ ] Timestamp de discovery registrado para cada ativo
- [ ] Inventario revisado pelo cliente para confirmar completude
