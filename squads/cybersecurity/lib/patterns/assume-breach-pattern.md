# Assume Breach Pattern

Padrao que opera sob a premissa de que o ambiente ja esta ou sera comprometido.

## Principio

Projetar defesas assumindo que um atacante ja tem acesso ao ambiente interno.
Isso muda o foco de prevencao pura para deteccao, contencao e resiliencia.

## Mudanca de Mindset

| Abordagem Tradicional | Assume Breach |
|----------------------|---------------|
| "Vamos impedir todo acesso" | "Vamos detectar e limitar o impacto" |
| Foco no perimetro | Foco em deteccao interna |
| Confianca na rede interna | Zero trust interno |
| Prevencao como unica estrategia | Deteccao + resposta como prioridade |

## Praticas Fundamentais

### Deteccao Interna
- Monitoramento de lateral movement
- Deteccao de privilege escalation
- Analise de comportamento anomalo (UEBA)
- Honey tokens e honeypots internos

### Limitacao de Blast Radius
- Network segmentation rigorosa
- Privileged access workstations (PAW)
- Tiered administration model
- Break-glass procedures documentados

### Preparacao para Resposta
- Incident response plan testado regularmente
- Forensic readiness (logs, retention, chain of custody)
- Communication templates pre-aprovados
- Relacionamento pre-estabelecido com DFIR externo

### Resiliencia
- Backups offline e imutaveis testados
- Disaster recovery plan para cenarios de ransomware
- Business continuity procedures
- Redundancia em sistemas criticos

## Exercicios de Validacao

- **Red Team**: Simular adversario real com objetivos definidos
- **Tabletop**: Exercicios de simulacao com lideranca
- **Purple Team**: Colaboracao entre ataque e defesa
- **Chaos Engineering**: Testar resiliencia a falhas

## Indicadores de Maturidade

- Dwell time medio abaixo de 7 dias
- Deteccao interna (vs. notificacao externa) > 80%
- Tempo de contencao < 2 horas
- Recovery point e recovery time objectives atendidos
