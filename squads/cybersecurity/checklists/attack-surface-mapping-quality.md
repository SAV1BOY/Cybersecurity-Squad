# Attack Surface Mapping Quality Gate

Checklist de qualidade para mapeamento da superficie de ataque.

## External Attack Surface
- [ ] Todos os domains e subdomains enumerados e validados
- [ ] Exposed services catalogados com versao e configuracao
- [ ] Public-facing APIs documentadas com endpoints
- [ ] SSL/TLS certificates analisados (expiry, chain, misconfig)
- [ ] Email security records verificados (SPF, DKIM, DMARC)
- [ ] DNS misconfigurations identificadas (zone transfer, dangling)

## Web Application Surface
- [ ] Entry points mapeados (forms, uploads, query params)
- [ ] Authentication flows documentados
- [ ] Authorization boundaries identificadas
- [ ] File upload endpoints catalogados com restricoes
- [ ] WebSocket e real-time endpoints mapeados
- [ ] Client-side JavaScript analisado para endpoints ocultos

## Infrastructure Surface
- [ ] Network segmentation boundaries documentadas
- [ ] VPN e remote access entry points identificados
- [ ] Management interfaces expostas catalogadas (SSH, RDP, admin panels)
- [ ] Default credentials verificados em servicos expostos
- [ ] SNMP, IPMI e out-of-band management verificados

## Cloud Attack Surface
- [ ] Public cloud storage (S3, Blob, GCS) verificado para exposicao
- [ ] Cloud metadata endpoints testados
- [ ] IAM policies revisadas para over-permission
- [ ] Serverless function triggers mapeados
- [ ] Container image registries verificados para acesso publico

## Supply Chain Surface
- [ ] Third-party dependencies catalogadas
- [ ] External integrations e webhooks mapeados
- [ ] CDN e proxy configurations revisadas
- [ ] Open-source components com known vulnerabilities sinalizados

## Documentacao e Priorizacao
- [ ] Attack surface diagram criado e atualizado
- [ ] Risk scoring aplicado a cada entry point
- [ ] High-value targets priorizados para teste
- [ ] Attack surface comparado com baseline anterior (se existente)
- [ ] Relatorio de attack surface entregue ao cliente
