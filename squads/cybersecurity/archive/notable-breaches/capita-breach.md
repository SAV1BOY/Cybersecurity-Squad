# Capita Breach Analysis (2023)

Analise do breach da Capita, uma das maiores empresas de outsourcing do Reino Unido.

## O Que Aconteceu

O grupo de ransomware Black Basta comprometeu a Capita, uma empresa de outsourcing
que gerencia dados e sistemas para centenas de organizacoes incluindo o NHS,
autoridades locais e fundos de pensao. O ataque afetou multiplos clientes
e expos dados sensiveis de milhoes de pessoas.

## Timeline

| Data | Evento |
|------|--------|
| Mar 22, 2023 | Primeiros sinais de acesso nao autorizado |
| Mar 31, 2023 | Capita reporta "incidente de TI" afetando servicos |
| Abr 3, 2023 | Capita confirma ataque cibernetico |
| Abr 20, 2023 | Capita confirma exfiltracao de dados |
| Mai 2023 | Descoberta de S3 buckets publicos com dados sensiveis |
| Jun 2023 | USS (fundo de pensao) confirma dados de membros expostos |

## Root Cause

1. **Acesso inicial nao detectado**: 9 dias entre acesso e deteccao
2. **Controles insuficientes**: Falta de segmentacao e monitoramento
3. **Shadow IT**: S3 buckets publicos descobertos durante investigacao
4. **Amplitude de acesso**: Como outsourcer, Capita tinha acesso a dados de centenas de clientes

## Impacto

- Mais de 90 organizacoes notificadas sobre dados comprometidos
- Dados de fundos de pensao de milhares de membros expostos
- Custo estimado de 25 milhoes de libras para Capita
- Multas regulatorias pendentes do ICO

## Licoes Aprendidas

- Outsourcers sao alvos de alto valor por agregarem dados de muitos clientes
- Cloud security posture management (CSPM) e essencial
- Shadow IT com dados sensiveis e um risco frequentemente subestimado
- Third-party risk management deve incluir auditorias regulares
- Comunicacao transparente e rapida minimiza dano reputacional
- Segmentacao de dados por cliente em ambientes multi-tenant

## Como Detectariamos/Preveniríamos

- CSPM para identificar S3 buckets publicos automaticamente
- Monitoramento de data exfiltration com DLP
- Segmentacao rigorosa entre dados de diferentes clientes
- EDR com deteccao de ransomware behavior patterns
- Threat hunting proativo para deteccao de acesso nao autorizado
