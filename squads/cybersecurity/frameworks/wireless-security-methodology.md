# Wireless Security Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de seguranca de redes wireless corporativas. Abrange
reconhecimento de infraestrutura WiFi, deteccao de rogue access points, avaliacao
de protocolos de criptografia e validacao de segmentacao de rede.

## Requisitos de Autorizacao
- Autorizacao especifica para testes wireless com localizacao fisica definida
- Coordenacao com equipe de infraestrutura de rede
- Frequencias e canais autorizados para teste documentados
- Acordo sobre impacto aceitavel em usuarios da rede
- Conformidade com regulamentacoes locais de telecomunicacoes (ANATEL)

## Etapas da Metodologia

### 1. Reconhecimento Wireless
- Wardriving/walking controlado nas instalacoes autorizadas
- Mapeamento de SSIDs visiveis e ocultos no perimetro
- Identificacao de canais, potencia de sinal e tipos de criptografia
- Catalogacao de BSSIDs e correlacao com inventario de ativos

### 2. Rogue Access Point Detection
- Identificacao de APs nao autorizados conectados a rede corporativa
- Deteccao de evil twin APs que imitam SSIDs corporativos
- Verificacao de wireless IDS/IPS (WIDS/WIPS) deployment
- Teste de alertas automaticos para rogue AP detection

### 3. Avaliacao de Criptografia
- Verificacao de protocolos em uso (WPA2-Enterprise, WPA3)
- Identificacao de redes com WEP ou WPA-PSK (vulneraveis)
- Teste de robustez de pre-shared keys quando aplicavel
- Avaliacao de configuracao EAP (PEAP, EAP-TLS, EAP-TTLS)
- Verificacao de validacao de certificado no supplicant

### 4. Ataques de Autenticacao
- Captura de handshakes WPA2 para analise de robustez de PSK
- PMKID capture como alternativa ao full handshake
- Teste de downgrade attacks em protocolos de autenticacao
- Avaliacao de resistencia a brute force em RADIUS authentication

### 5. Segmentacao e Isolamento
- Verificacao de client isolation entre dispositivos wireless
- Teste de segmentacao entre SSID corporativo e guest
- Validacao de ACLs entre rede wireless e segmentos internos
- Avaliacao de VLAN assignment dinamico baseado em autenticacao

### 6. Captive Portal e Guest Network
- Teste de bypass em captive portal authentication
- Avaliacao de isolamento de rede guest do ambiente corporativo
- Verificacao de rate limiting e controle de banda em guest
- Analise de politicas de retencao de logs de acesso guest

## Ferramentas de Referencia
- Aircrack-ng suite, Kismet, Wireshark, hcxdumptool, hcxtools
- WiFi Pineapple (uso controlado), Fluxion (lab environment only)

## Contrapartida de Deteccao (Blue Team)
- Deployment de WIDS/WIPS para deteccao automatica de rogue APs
- Monitoramento continuo de espectro wireless nas instalacoes
- Alertas para novos SSIDs ou BSSIDs nao catalogados
- Auditoria periodica de configuracoes de APs e controladores
- Logs centralizados de autenticacao RADIUS para analise

## Integracao com Outros Frameworks
- Correlaciona com: credential-attack-methodology.md (credenciais WiFi)
- Correlaciona com: lateral-movement-methodology.md (acesso via wireless)
- Alimenta: network segmentation assessment e risk register
- Reporta para: compliance frameworks (PCI-DSS wireless requirements)
