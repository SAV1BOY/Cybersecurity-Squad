# Kim - Recon Checklist

Checklist de reconhecimento seguindo a abordagem metodica de Peter Kim.

## Passive Reconnaissance
- [ ] OSINT framework aplicado de forma sistematica
- [ ] Domain WHOIS e registrant history pesquisados
- [ ] DNS records enumerados (A, AAAA, MX, TXT, NS, SOA, SRV)
- [ ] Subdomain enumeration via multiple sources (crt.sh, SecurityTrails, Amass)
- [ ] Google dorking executado para information disclosure
- [ ] Shodan/Censys queries para exposed services
- [ ] GitHub/GitLab dorking para credentials e configs vazados
- [ ] Social media profiling de funcionarios-chave
- [ ] LinkedIn enumeration para org chart e tecnologias
- [ ] Pastebin e leak databases consultados

## Active Reconnaissance
- [ ] Port scanning (TCP SYN + UDP top ports) em todos os targets
- [ ] Service version detection executada em portas abertas
- [ ] OS fingerprinting realizado por host
- [ ] Web technology fingerprinting (Wappalyzer, WhatWeb)
- [ ] Virtual host enumeration testada
- [ ] Directory/file brute-forcing em web applications
- [ ] Email address enumeration e validation
- [ ] WAF detection e identification realizada

## Correlacao e Analise
- [ ] Resultados de passive e active recon correlacionados
- [ ] Network topology inferida e documentada
- [ ] High-value targets identificados com justificativa
- [ ] Attack surface diagram atualizado com novos findings
- [ ] Potential entry points priorizados por probabilidade de sucesso
- [ ] Recon data organizado em formato estruturado

## Qualidade e Completude
- [ ] Nenhum target in-scope ficou sem recon coverage
- [ ] Multiple tools usados para validacao cruzada
- [ ] Timestamp registrado para cada discovery
- [ ] Recon report entregue com IOCs e insights
- [ ] Resultados revisados por peer antes de prosseguir
- [ ] Recon notes acessiveis para referencia durante exploitation
