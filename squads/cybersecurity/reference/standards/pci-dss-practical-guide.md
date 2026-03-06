# PCI DSS - Guia Pratico

## Visao Geral
Payment Card Industry Data Security Standard (PCI DSS) e o padrao de seguranca
para organizacoes que processam, armazenam ou transmitem dados de cartao de
pagamento. Versao atual: PCI DSS v4.0.

## Os 12 Requisitos (v4.0)

### Build and Maintain a Secure Network
1. Install and maintain network security controls
2. Apply secure configurations to all system components

### Protect Account Data
3. Protect stored account data
4. Protect cardholder data with strong cryptography during transmission

### Maintain a Vulnerability Management Program
5. Protect all systems and networks from malicious software
6. Develop and maintain secure systems and software

### Implement Strong Access Control Measures
7. Restrict access to system components by business need to know
8. Identify users and authenticate access to system components
9. Restrict physical access to cardholder data

### Regularly Monitor and Test Networks
10. Log and monitor all access to system components and cardholder data
11. Test security of systems and networks regularly

### Maintain an Information Security Policy
12. Support information security with organizational policies and programs

## Mudancas Importantes no v4.0
- Customized approach como alternativa ao defined approach
- Targeted risk analysis para flexibilidade
- Enhanced authentication requirements (MFA expandido)
- E-commerce e phishing protections
- Automated mechanisms para log reviews
- Future-dated requirements com deadlines especificos

## Como o Squad Aplica
- **PCI Assessments**: avaliacao de conformidade para clientes
- **Scope Reduction**: estrategias para reduzir escopo PCI
- **Segmentation Testing**: validacao de segmentacao de rede
- **Penetration Testing**: pentests requeridos pelo requisito 11
- **Log Monitoring**: design de monitoramento para requisito 10

## Contexto Brasil
- Mercado financeiro brasileiro e altamente regulado
- Bandeiras de cartao locais (Elo, Hipercard) tambem exigem PCI
- PIX nao substitui PCI para operacoes com cartao
- Integracao com requisitos do Banco Central

## Ferramentas Uteis
- PCI SSC document library
- ASV scanning tools (Qualys, Tenable)
- Network segmentation testing tools
- File integrity monitoring (OSSEC, Tripwire)

## Notas do Squad
PCI DSS v4.0 introduziu o conceito de customized approach, que permite mais
flexibilidade mas exige maior maturidade. Avaliar caso a caso qual approach
e mais adequado para cada cliente.
