# Risk Register

Registro centralizado de riscos de seguranca identificados, avaliados e monitorados.

## Schema do Registro

| Risk ID | Description | Category | Likelihood | Impact | Risk Score | Owner | Treatment | Status | Review Date |
|---------|-------------|----------|------------|--------|------------|-------|-----------|--------|-------------|
| RISK-001 | Credential stuffing em apps expostas | Application Security | High | High | 20 | @appsec-lead | Mitigate | Active | 2026-03-01 |
| RISK-002 | Supply chain compromise via dependencies | Supply Chain | Medium | Critical | 20 | @devsecops | Mitigate | Active | 2026-03-01 |
| RISK-003 | Insider threat - privileged users | Insider Threat | Low | Critical | 15 | @iam-team | Accept | Monitoring | 2026-04-01 |
| RISK-004 | DDoS em servicos publicos | Infrastructure | Medium | High | 16 | @infra-team | Transfer | Active | 2026-03-15 |

## Matriz de Risco (Likelihood x Impact)

|              | Negligible(1) | Low(2) | Medium(3) | High(4) | Critical(5) |
|--------------|:---:|:---:|:---:|:---:|:---:|
| Almost Certain(5) | 5 | 10 | 15 | 20 | 25 |
| Likely(4)    | 4 | 8 | 12 | 16 | 20 |
| Possible(3)  | 3 | 6 | 9 | 12 | 15 |
| Unlikely(2)  | 2 | 4 | 6 | 8 | 10 |
| Rare(1)      | 1 | 2 | 3 | 4 | 5 |

## Tratamento de Risco

- **Mitigate**: Implementar controles para reduzir likelihood ou impact
- **Accept**: Aceitar formalmente com aprovacao da lideranca
- **Transfer**: Transferir via seguro ou terceirizacao
- **Avoid**: Eliminar a atividade que gera o risco

## Processo de Revisao

Riscos com score >= 15 sao revisados mensalmente. Demais riscos sao revisados
trimestralmente. Novos riscos podem ser adicionados a qualquer momento e devem
ser avaliados dentro de 5 dias uteis.
