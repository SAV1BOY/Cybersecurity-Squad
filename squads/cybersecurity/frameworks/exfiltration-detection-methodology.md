# Exfiltration Detection Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de controles de prevencao e deteccao de exfiltracao de dados.
Testa canais comuns de saida de informacoes, incluindo protocolos de rede, cloud storage
e midias fisicas. Foco duplo: simulacao ofensiva e capacidade de deteccao.

## Requisitos de Autorizacao
- Aprovacao para uso de dados sinteticos (nunca dados reais sensiveis)
- Definicao de canais de exfiltracao autorizados para teste
- Coordenacao com equipe de rede e DLP para monitoramento
- Limites de volume de dados para simulacao
- Notificacao previa ao SOC com janela de teste definida

## Etapas da Metodologia

### 1. DNS Tunneling
- Simulacao de exfiltracao via DNS TXT/CNAME queries
- Encoding de dados em subdomains de dominios controlados
- Avaliacao de resolvers internos e capacidade de inspecao DNS
- Teste de rate limiting e tamanho maximo de queries DNS

### 2. HTTP/HTTPS Exfiltration
- Upload de dados via POST requests para endpoints externos
- Utilizacao de servicos legitimos como canal (paste sites, webhooks)
- Steganografia em imagens e arquivos transmitidos via HTTPS
- Avaliacao de SSL/TLS inspection e proxy capabilities

### 3. Cloud Storage Channels
- Upload para servicos de cloud storage pessoal (Drive, Dropbox, OneDrive)
- Utilizacao de APIs de cloud services para transferencia de dados
- Compartilhamento de dados via SaaS collaboration tools
- Teste de DLP policies para deteccao de dados sensiveis em upload

### 4. Email Exfiltration
- Envio de dados como anexos ou no corpo de emails
- Utilizacao de email forwarding rules automaticas
- Teste de controles de DLP em gateway de email
- Avaliacao de limites de tamanho e tipo de anexo

### 5. Physical Media e USB
- Tentativa de copia para dispositivos USB (se autorizado)
- Avaliacao de device control policies e endpoint DLP
- Teste de bloqueio de removable media via Group Policy
- Verificacao de alertas gerados por conexao de dispositivos

### 6. Covert Channels
- ICMP tunneling para exfiltracao de baixo volume
- Exfiltracao via protocolos permitidos (NTP, SMTP headers)
- Timing-based channels e encoding em metadata de protocolos
- Avaliacao de deep packet inspection capabilities

## Ferramentas de Referencia
- dnscat2, iodine (DNS tunneling), PacketWhisper, Cloakify
- DET (Data Exfiltration Toolkit — uso exclusivo em labs autorizados)

## Contrapartida de Deteccao (Blue Team)
- Monitoramento de DNS query volume e tamanho anomalo de subdomains
- Inspecao de HTTPS traffic via SSL termination em proxy corporativo
- DLP policies ativas em endpoints, email gateway e cloud access (CASB)
- Alertas para upload em massa para cloud storage nao corporativo
- Network behavior analysis para deteccao de covert channels
- Baseline de trafego normal para identificacao de anomalias volumetricas

## Integracao com Outros Frameworks
- Recebe de: lateral-movement-methodology.md (acesso a dados sensiveis)
- Correlaciona com: phishing-simulation-methodology.md (vetor de saida via email)
- Alimenta: SIEM rules e playbooks de resposta a incidentes
- Reporta para: DLP dashboard e gestao de risco de dados
