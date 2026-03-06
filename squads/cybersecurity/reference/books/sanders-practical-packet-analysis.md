# Practical Packet Analysis - Ficha de Referencia

## Metadados
- **Titulo**: Practical Packet Analysis: Using Wireshark to Solve Real-World Network Problems
- **Autor**: Chris Sanders
- **Categoria**: Network Security / Traffic Analysis

## Descricao Geral
Guia pratico para analise de trafego de rede utilizando Wireshark. O livro ensina
a interpretar pacotes de rede para resolver problemas reais de seguranca e
troubleshooting, desde cenarios basicos ate investigacoes forenses.

## Conceitos-Chave
- Fundamentos de protocolos TCP/IP e modelo OSI
- Wireshark interface e capture filters vs display filters
- TCP handshake analysis e connection troubleshooting
- HTTP/HTTPS traffic inspection
- DNS analysis e deteccao de anomalias
- Wireless packet analysis
- Network forensics e evidence collection
- Performance analysis e latency troubleshooting
- VoIP traffic analysis
- Custom protocol dissection

## Por Que Importa para o Squad
Analise de pacotes e uma habilidade fundamental tanto para blue team quanto para
red team. Permite identificar ataques em andamento, validar regras de deteccao
e entender o comportamento real do trafego na rede.

## Como o Squad Utiliza
- **Incident Response**: analise de capturas durante incidentes
- **Detection Engineering**: validacao de regras de deteccao via pcap
- **Forensics**: coleta e analise de evidencias de rede
- **Training**: exercicios praticos com pcaps de referencia
- **Threat Hunting**: busca proativa de anomalias em trafego

## Ferramentas Mencionadas
- Wireshark (foco principal)
- tshark (linha de comando)
- tcpdump para captura
- NetworkMiner
- Zeek/Bro (complementar)

## Complementa
- sanders-applied-nsm.md (network security monitoring abrangente)
- bejtlich-practice-nsm.md (NSM como disciplina)
- sanders-intrusion-detection-honeypots.md (deteccao de intrusao)

## Nivel de Profundidade
Iniciante a Intermediario - acessivel para quem tem nocoes basicas de redes.

## Notas do Squad
Manter uma biblioteca de pcaps anotados para referencia e treinamento. Cada
membro do squad deve ser capaz de analisar capturas basicas de trafego
independente de sua especializacao.
