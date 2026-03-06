# Colonial Pipeline Ransomware (2021)

Analise do ataque de ransomware que paralisou o maior oleoduto dos EUA.

## O Que Aconteceu

O grupo DarkSide comprometeu a Colonial Pipeline atraves de uma senha
comprometida de uma conta VPN legada que nao usava MFA. O ransomware
encriptou sistemas de TI, levando a empresa a desligar o oleoduto
por precaucao, causando escassez de combustivel na costa leste dos EUA.

## Timeline

| Data | Evento |
|------|--------|
| Abr 29, 2021 | Acesso inicial via VPN com credencial comprometida |
| Mai 6, 2021 | DarkSide implanta ransomware na rede corporativa |
| Mai 7, 2021 | Colonial Pipeline detecta o ataque e desliga oleoduto |
| Mai 8, 2021 | Declaracao de emergencia federal |
| Mai 10, 2021 | Colonial paga resgate de ~$4.4 milhoes em Bitcoin |
| Mai 12, 2021 | Oleoduto volta a operar parcialmente |
| Jun 7, 2021 | FBI recupera $2.3 milhoes do resgate |

## Root Cause

1. **Credencial comprometida**: Senha reutilizada encontrada em vazamento
2. **Ausencia de MFA**: Conta VPN sem multi-factor authentication
3. **Conta legada ativa**: Conta nao usada ativamente mas ainda habilitada
4. **Segmentacao IT/OT insuficiente**: Receio de propagacao para OT motivou shutdown

## Impacto

- 5.500 milhas de oleoduto desligado por 6 dias
- Escassez de gasolina em varios estados americanos
- Preco de gasolina no maior nivel em 7 anos
- Resgate de $4.4M (parcialmente recuperado)

## Licoes Aprendidas

- MFA e obrigatorio em todos os acessos remotos, sem excecao
- Contas legadas devem ser desativadas em processo de offboarding
- Credenciais devem ser verificadas contra breach databases
- Segmentacao IT/OT rigorosa e critica em infraestrutura essencial
- Planos de resposta a ransomware devem ser testados regularmente
- Backup offline e imutavel e essencial para recuperacao

## Como Detectariamos/Preveniríamos

- MFA enforcement em todos os acessos VPN
- Monitoramento de credenciais em breach databases (Have I Been Pwned)
- Access review trimestral para identificar contas orfas
- Deteccao de lateral movement pos-VPN access
- Segmentacao rigorosa entre redes IT e OT
