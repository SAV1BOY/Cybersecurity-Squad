# Forensics Collection Quality Gate

Checklist de qualidade para coleta forense digital.

## Preparacao
- [ ] Authorization para coleta forense obtida por escrito
- [ ] Forensic toolkit preparado e validado (write blockers, imaging tools)
- [ ] Chain of custody form iniciado
- [ ] Storage midia forense preparada e verificada (limpa, capacidade)
- [ ] Relogio do sistema forense sincronizado com NTP
- [ ] Documentacao fotografica do ambiente antes de qualquer acao

## Volatile Data Collection (Ordem de Volatilidade)
- [ ] Memory dump coletado antes de qualquer outra acao
- [ ] Running processes capturados
- [ ] Network connections ativas documentadas
- [ ] Logged-in users registrados
- [ ] Open files e handles capturados
- [ ] System time e uptime registrados
- [ ] Routing tables e ARP cache preservados
- [ ] Clipboard contents coletados (se aplicavel)

## Disk Imaging
- [ ] Write blocker utilizado para prevenir alteracao
- [ ] Full disk image (bit-for-bit) criada
- [ ] Hash (SHA-256) da source disk calculado antes da imagem
- [ ] Hash da imagem calculado e comparado com source
- [ ] Imagem verificada com ferramenta forense
- [ ] Segunda copia da imagem criada para working copy
- [ ] Imagem armazenada em midia segura com controle de acesso

## Log Collection
- [ ] System logs coletados (syslog, Event Log, journal)
- [ ] Application logs coletados
- [ ] Security logs coletados (auth, audit)
- [ ] Network device logs coletados (firewall, proxy, DNS)
- [ ] Cloud audit logs coletados (CloudTrail, Activity Log)
- [ ] Email logs coletados (se relevante ao incidente)

## Network Forensics
- [ ] Packet captures (PCAP) coletados de pontos relevantes
- [ ] NetFlow/IPFIX data exportado
- [ ] DNS query logs preservados
- [ ] Proxy logs com full URLs coletados
- [ ] IDS/IPS alerts exportados

## Chain of Custody
- [ ] Cada item de evidencia com identificador unico
- [ ] Data/hora de coleta registrada para cada item
- [ ] Coletor identificado (nome, funcao) para cada item
- [ ] Metodo de coleta documentado
- [ ] Storage location registrado
- [ ] Cada transferencia de custodia documentada
- [ ] Evidencias fisicas lacradas e etiquetadas
- [ ] Formulario de chain of custody assinado por todas as partes
