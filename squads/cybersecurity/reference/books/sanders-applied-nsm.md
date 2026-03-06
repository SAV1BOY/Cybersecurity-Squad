# Applied Network Security Monitoring - Ficha de Referencia

## Metadados
- **Titulo**: Applied Network Security Monitoring: Collection, Detection, and Analysis
- **Autor**: Chris Sanders, Jason Smith
- **Categoria**: Defensive Security / Network Security Monitoring

## Descricao Geral
Guia completo para implementacao de Network Security Monitoring (NSM) em ambientes
corporativos. Cobre todo o ciclo de coleta, deteccao e analise de dados de rede
com foco em operacoes de SOC.

## Conceitos-Chave
- NSM cycle: collection, detection, analysis
- Full packet capture vs metadata-only approaches
- Session data analysis e flow records
- Signature-based vs anomaly-based detection
- Zeek/Bro scripting para custom detections
- SIEM integration e log correlation
- Analyst workflow e investigation methodology
- Escalation criteria e incident handoff
- Capacity planning para NSM infrastructure
- Sensor placement strategy

## Por Que Importa para o Squad
NSM e a espinha dorsal de qualquer operacao de seguranca defensiva. Este livro
fornece o framework conceitual e pratico para montar e operar uma capacidade
robusta de monitoramento de rede.

## Como o Squad Utiliza
- **SOC Design**: referencia para arquitetura de operacoes de seguranca
- **Sensor Deployment**: guia para posicionamento de sensores de rede
- **Detection Rules**: metodologia para criacao de regras de deteccao
- **Analyst Training**: formacao de analistas de SOC nivel 1 e 2
- **Incident Triage**: processo de triagem e escalacao

## Ferramentas Mencionadas
- Zeek/Bro, Suricata, Snort
- Security Onion (plataforma integrada)
- Wireshark, NetworkMiner
- ELK Stack para analise
- Moloch/Arkime para PCAP

## Complementa
- sanders-practical-packet-analysis.md (analise de pacotes)
- bejtlich-practice-nsm.md (fundamentos de NSM)
- sanders-intrusion-detection-honeypots.md (deteccao por deception)

## Nivel de Profundidade
Intermediario a Avancado - ideal para analistas de SOC e engenheiros de deteccao.

## Notas do Squad
Security Onion e a plataforma recomendada para implementacao rapida de NSM.
Integrar com o lab environment do squad para pratica continua.
