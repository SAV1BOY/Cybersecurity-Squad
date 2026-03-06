# Equifax Breach Analysis (2017)

Analise do breach da Equifax que expôs dados de 147 milhoes de pessoas.

## O Que Aconteceu

Atacantes exploraram uma vulnerabilidade conhecida no Apache Struts (CVE-2017-5638)
em um portal web da Equifax. A vulnerabilidade permitia remote code execution e
ja tinha patch disponivel ha 2 meses quando foi explorada.

## Timeline

| Data | Evento |
|------|--------|
| Mar 7, 2017 | Apache Struts patch publicado para CVE-2017-5638 |
| Mar 8, 2017 | US-CERT emite alerta sobre a vulnerabilidade |
| Mar 9, 2017 | Equifax recebe notificacao interna para patching |
| Mai 13, 2017 | Atacantes iniciam exploracao do portal vulneravel |
| Jul 29, 2017 | Equifax detecta trafego suspeito ao renovar certificado SSL |
| Jul 30, 2017 | Equifax confirma o breach e inicia contencao |
| Set 7, 2017 | Divulgacao publica do incidente |

## Root Cause

1. **Falha no patch management**: Patch disponivel por 2 meses nao aplicado
2. **Certificate expirado**: Certificado SSL usado para inspecao de trafego
   estava expirado ha 19 meses, impedindo deteccao
3. **Segmentacao inexistente**: Atacantes acessaram 48 bancos de dados
   a partir de um unico servidor comprometido
4. **Dados nao criptografados**: Dados sensiveis armazenados em plaintext

## Dados Expostos

- Nomes, SSN, datas de nascimento de 147M pessoas
- Numeros de cartao de credito de 209K consumidores
- Documentos de disputa com PII de 182K consumidores

## Licoes Aprendidas

- Patch management com SLA rigoroso e rastreamento e fundamental
- Certificados de seguranca devem ter monitoramento de expiracao
- Network segmentation limita blast radius
- Encryption at rest protege dados mesmo apos comprometimento
- Asset inventory completo e pre-requisito para vulnerability management

## Como Detectariamos/Preveniríamos

- Vulnerability scanning com SLA enforcement automatizado
- Network segmentation entre camadas e bancos de dados
- Certificate monitoring com alertas de expiracao
- DLP para detectar exfiltracao de dados sensiveis
- Encrypted storage para todos os dados classificados
