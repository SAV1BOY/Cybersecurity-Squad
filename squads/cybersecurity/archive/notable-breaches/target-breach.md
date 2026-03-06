# Target Breach Analysis (2013)

Analise do breach da Target que comprometeu dados de 110 milhoes de clientes.

## O Que Aconteceu

Atacantes comprometeram a Target atraves de um fornecedor de HVAC (Fazio Mechanical),
usando credenciais roubadas para acessar a rede corporativa. A partir dai,
moveram-se lateralmente ate os sistemas de point-of-sale (POS), instalando
malware para captura de dados de cartao de credito.

## Timeline

| Data | Evento |
|------|--------|
| Set 2013 | Phishing ao fornecedor Fazio Mechanical |
| Nov 15, 2013 | Atacantes acessam rede da Target via vendor portal |
| Nov 27, 2013 | Malware instalado em POS terminals (Black Friday) |
| Dez 2, 2013 | FireEye alerta gerados mas nao investigados |
| Dez 12, 2013 | DOJ notifica Target sobre o breach |
| Dez 15, 2013 | Target confirma e inicia contencao |
| Dez 19, 2013 | Divulgacao publica |

## Root Cause

1. **Third-party access**: Vendor com acesso excessivo a rede interna
2. **Segmentacao ausente**: Rede de vendors conectada a rede de POS
3. **Alertas ignorados**: FireEye gerou alertas que nao foram investigados
4. **Falta de least privilege**: Vendor de HVAC com acesso a rede de pagamentos

## Dados Expostos

- 40 milhoes de numeros de cartao de credito
- 70 milhoes de registros com PII (nome, endereco, telefone, email)
- Custo total estimado: $292 milhoes

## Licoes Aprendidas

- Terceiros devem ter acesso minimo e segmentado
- Alertas de seguranca devem ter processo de triagem obrigatorio
- Network segmentation entre ambientes e essencial (PCI-DSS)
- Supply chain risk management deve incluir todos os vendors
- Monitoramento de POS e sistemas de pagamento requer atencao especial
- Incident response deve ser capaz de agir rapidamente apos alertas

## Como Detectariamos/Preveniríamos

- Vendor risk assessment e monitoramento continuo
- Micro-segmentation entre rede de vendors e sistemas criticos
- SOC com processo de triagem obrigatorio para alertas de alta severidade
- POS monitoring com behavioral analysis
- MFA para todo acesso de terceiros
- Regular penetration testing focado em lateral movement
