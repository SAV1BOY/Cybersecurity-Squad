# Network Analysis Tools

## Visao Geral
Ferramentas para analise, monitoramento e testes de seguranca de redes.
Utilizadas tanto em operacoes defensivas quanto ofensivas pelo squad.

## Packet Capture e Analysis

### Wireshark
- **Tipo**: GUI packet analyzer
- **Uso**: analise detalhada de trafego de rede
- **Filtros**: display filters e capture filters
- **Dica**: dominar filtros e essencial para eficiencia

### tshark
- **Tipo**: CLI packet analyzer (Wireshark CLI)
- **Uso**: captura e analise automatizada via scripts
- **Integracao**: pipes com outras ferramentas Unix

### tcpdump
- **Tipo**: CLI packet capture tool
- **Uso**: captura leve de trafego em servidores
- **Dica**: capturar com tcpdump, analisar com Wireshark

## Network Monitoring

### Zeek (formerly Bro)
- **Tipo**: network security monitor
- **Uso**: gerar logs estruturados de trafego (conn, http, dns, ssl)
- **Scripts**: linguagem propria para analise custom
- **Diferencial**: metadata rica sem full packet capture

### Suricata
- **Tipo**: IDS/IPS e network security monitor
- **Uso**: deteccao de ameacas baseada em assinaturas e anomalias
- **Regras**: ET Open, ET Pro, custom rules
- **Modos**: IDS, IPS, NSM

### Snort
- **Tipo**: IDS/IPS classico
- **Uso**: deteccao de intrusao baseada em assinaturas
- **Regras**: Snort Community, Talos rules

## Network Scanning e Discovery

### Nmap
- **Tipo**: network scanner
- **Uso**: host discovery, port scanning, service detection
- **NSE**: scripts para automacao de checks

### Masscan
- **Tipo**: high-speed port scanner
- **Uso**: varredura rapida de grandes redes

### Netcat (nc/ncat)
- **Tipo**: TCP/UDP utility tool
- **Uso**: banner grabbing, port testing, file transfer, reverse shells

## Traffic Manipulation

### mitmproxy
- **Tipo**: interactive HTTPS proxy
- **Uso**: interceptar e modificar trafego HTTP/S
- **Interface**: CLI, Web UI, Python API
- **Dica**: ideal para analise de APIs mobile

### Responder
- **Tipo**: LLMNR/NBT-NS/mDNS poisoner
- **Uso**: captura de credentials em redes Windows
- **Ataques**: NTLM relay, credential harvesting

### Bettercap
- **Tipo**: network attack e monitoring framework
- **Uso**: MITM attacks, network recon, WiFi attacks
- **Interface**: web UI interativa

## DNS Tools

### dig / nslookup
- **Tipo**: DNS query utilities
- **Uso**: consultas DNS, zone transfer tests

### dnsrecon
- **Tipo**: DNS enumeration tool
- **Uso**: brute force, zone transfer, cache snooping

## Workflow do Squad
- Defensivo: Zeek + Suricata + Wireshark para monitoramento e analise
- Ofensivo: Nmap + Responder + Bettercap para recon e exploitation
- Forense: tcpdump/Wireshark + Zeek para analise de evidencias

## Notas do Squad
Manter sensores de rede (Zeek + Suricata) em pontos estrategicos da rede.
Armazenar metadata de trafego para threat hunting retroativo.
