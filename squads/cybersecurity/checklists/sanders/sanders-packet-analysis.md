# Sanders - Packet Analysis

Checklist para analise de pacotes de rede conforme metodologia de Chris Sanders.

## Preparacao da Captura
- [ ] Ponto de captura definido (TAP, SPAN port, inline)
- [ ] Captura posicionada para visibilidade do trafego alvo
- [ ] Filtro de captura aplicado para reduzir volume (se necessario)
- [ ] Storage suficiente para duracao planejada da captura
- [ ] Timestamp sincronizado via NTP no sistema de captura
- [ ] Interface de captura em modo promiscuo
- [ ] Snaplen configurado adequadamente (full packet vs headers only)

## Analise de Protocolos
- [ ] TCP handshakes analisados para anomalias (SYN floods, resets)
- [ ] DNS queries analisadas (tunneling, DGA, suspicious domains)
- [ ] HTTP/HTTPS traffic analisado (user-agent, URLs, methods)
- [ ] TLS handshakes inspecionados (versions, ciphers, certificates)
- [ ] SMB/CIFS traffic analisado para lateral movement indicators
- [ ] SMTP/POP/IMAP traffic revisado para data exfiltration
- [ ] ICMP traffic analisado para tunneling indicators

## Identificacao de Anomalias
- [ ] Beaconing patterns identificados (regular intervals, jitter)
- [ ] Data exfiltration indicators buscados (large uploads, encoding)
- [ ] Protocol anomalies detectadas (non-standard ports, malformed packets)
- [ ] Encrypted traffic em portas nao-standard analisado
- [ ] Long-duration connections identificadas
- [ ] Geographic anomalies em destinos de trafego
- [ ] Bandwidth anomalies detectadas por host/flow

## Correlacao e Contexto
- [ ] Traffic correlacionado com IOCs conhecidos
- [ ] Flow data cruzada com logs de firewall/proxy
- [ ] Endpoints envolvidos identificados e contextualizados
- [ ] Timeline de eventos reconstruida via packet analysis
- [ ] Payload extraction realizado para arquivos suspeitos
- [ ] Certificates extraidos e analisados

## Ferramentas e Tecnicas
- [ ] Wireshark display filters aplicados eficientemente
- [ ] Tshark/tcpdump para bulk analysis utilizado
- [ ] Zeek/Bro logs gerados para analise de metadados
- [ ] NetworkMiner para artifact extraction (se aplicavel)
- [ ] Statistical analysis aplicada (conversations, endpoints, IO graphs)
- [ ] Expert info do Wireshark revisada para alertas

## Documentacao
- [ ] PCAP files preservados com hash integrity
- [ ] Findings documentados com packet references (frame numbers)
- [ ] Screenshots de Wireshark incluidos como evidencia
- [ ] Timeline de network events documentada
- [ ] IOCs extraidos e catalogados
- [ ] Report de analise entregue com conclusoes e recomendacoes
