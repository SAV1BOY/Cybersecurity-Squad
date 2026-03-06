# Reconnaissance e Enumeration Tools

## Visao Geral
Ferramentas utilizadas pelo squad para as fases de reconnaissance e enumeration
em penetration tests e red team operations. Organizadas por tipo de atividade.

## Passive Reconnaissance

### Shodan
- **Funcao**: search engine para dispositivos conectados a internet
- **Uso**: identificar servicos expostos, IoT devices, infraestrutura
- **Comandos uteis**: `shodan search`, `shodan host`, `shodan stats`
- **Alternativas**: Censys, ZoomEye, BinaryEdge

### theHarvester
- **Funcao**: coleta de emails, subdomains, hosts, nomes
- **Uso**: OSINT gathering na fase inicial de recon
- **Fontes**: Google, Bing, LinkedIn, Shodan, VirusTotal
- **Dica**: combinar multiplas fontes para cobertura completa

### Maltego
- **Funcao**: plataforma de OSINT e link analysis visual
- **Uso**: mapeamento de relacoes entre entidades (pessoas, dominios, IPs)
- **Transforms**: modulos que automatizam coleta de dados
- **Versao**: Community (gratis) vs Commercial

### SpiderFoot
- **Funcao**: automacao de OSINT com 200+ modulos
- **Uso**: recon automatizado e abrangente
- **Interface**: web UI e CLI disponveis

## Active Reconnaissance

### Nmap
- **Funcao**: network discovery e port scanning
- **Uso**: identificar hosts ativos, portas abertas, servicos, OS
- **Scripts**: NSE (Nmap Scripting Engine) para automacao
- **Scans essenciais**: SYN scan, version detection, OS fingerprint
- **Dica**: usar timing templates adequados ao contexto

### Masscan
- **Funcao**: port scanner de alta velocidade
- **Uso**: varredura rapida de grandes faixas de IP
- **Performance**: pode escanear toda a internet em minutos
- **Dica**: usar com cautela em ambientes de producao

### Amass
- **Funcao**: subdomain enumeration avancada
- **Uso**: descoberta de subdomains via DNS, scraping e APIs
- **Modos**: passive, active, brute force
- **Integracao**: alimenta outras ferramentas de recon

## Service Enumeration

### enum4linux-ng
- **Funcao**: enumeracao de servicos Windows/SMB
- **Uso**: coletar informacoes de dominios, shares, usuarios

### gobuster / ffuf
- **Funcao**: directory e DNS brute forcing
- **Uso**: descoberta de diretorios web, virtual hosts, subdomains
- **Wordlists**: SecLists como referencia padrao

### Nikto
- **Funcao**: web server scanner
- **Uso**: identificar configuracoes inseguras e vulns conhecidas

## Workflow do Squad
1. Passive recon com theHarvester + SpiderFoot
2. Subdomain enumeration com Amass
3. Port scanning com Nmap (targeted) ou Masscan (broad)
4. Service enumeration com ferramentas especificas
5. Consolidar resultados em plataforma de gestao

## Notas do Squad
Sempre obter autorizacao por escrito antes de scanning ativo. Documentar
todo o processo de recon para inclusao no relatorio final.
