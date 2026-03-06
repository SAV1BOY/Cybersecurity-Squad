# Wireless Security Quality Gate

Checklist de qualidade para avaliacao de seguranca wireless.

## Reconhecimento Wireless
- [ ] Site survey realizado para mapear redes wireless
- [ ] SSIDs corporativos e guest identificados
- [ ] Rogue access points detectados e catalogados
- [ ] Signal coverage mapeado para identificar bleeding
- [ ] Hidden SSIDs descobertos e documentados
- [ ] Wireless clients enumerados por SSID

## Configuracao de Seguranca
- [ ] Protocolo de autenticacao verificado (WPA3-Enterprise preferido)
- [ ] WPA2-Enterprise com 802.1X validado (se WPA3 indisponivel)
- [ ] WEP e WPA-PSK ausentes em redes corporativas
- [ ] RADIUS server configuration auditada
- [ ] Certificate validation no supplicant verificada
- [ ] EAP method seguro em uso (EAP-TLS, PEAP)
- [ ] PMF (Protected Management Frames) habilitado

## Segmentacao e Isolamento
- [ ] Guest network isolada da rede corporativa
- [ ] VLAN assignment por SSID configurado corretamente
- [ ] Client isolation habilitado em guest networks
- [ ] Wireless management interface restrita a rede de gerencia
- [ ] Firewall rules entre wireless e wired networks revisadas

## Testes de Ataque
- [ ] Deauthentication attack testado
- [ ] Evil twin attack testado contra supplicant configuration
- [ ] PMKID capture tentado para WPA2-PSK (se aplicavel)
- [ ] Credential harvesting via captive portal falso testado
- [ ] KARMA/known-beacons attack testado
- [ ] Bluetooth scanning realizado para dispositivos expostos

## Monitoramento e Deteccao
- [ ] WIDS/WIPS implementado e funcional
- [ ] Alerting para rogue APs configurado
- [ ] Alerting para deauth floods configurado
- [ ] Logging de autenticacao wireless centralizado
- [ ] Periodic scan schedule para rogue detection definido

## Documentacao
- [ ] Mapa de cobertura wireless atualizado
- [ ] Inventario de APs com firmware versions documentado
- [ ] Findings com PoC e impacto documentados
- [ ] Recommendations alinhadas com best practices (NIST, CIS)
- [ ] Report revisado e entregue ao cliente
