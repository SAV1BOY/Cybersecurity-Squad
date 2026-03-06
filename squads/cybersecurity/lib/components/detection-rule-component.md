# Detection Rule Component

Componente padronizado para documentacao de regras de deteccao.

## Estrutura

```
## Detection Rule: [DET-ID]

### Metadata
- **Name**: [Nome descritivo da regra]
- **MITRE ATT&CK**: [Technique ID e nome]
- **Severity**: [Critical | High | Medium | Low]
- **Platform**: [SIEM | EDR | Cloud | Custom]
- **Author**: [Criador da regra]
- **Created**: [Data de criacao]
- **Last Updated**: [Data da ultima atualizacao]

### Description
[O que esta regra detecta e por que e importante]

### Detection Logic
[Query, regra ou pseudocodigo da deteccao]

### Data Sources Required
[Logs e fontes de dados necessarios]

### False Positive Scenarios
[Cenarios conhecidos que geram false positives]

### Tuning Notes
[Thresholds ajustaveis e criterios de exclusao]

### Triage Runbook
[Passos para o analista seguir ao receber o alerta]

### Test Cases
[Como validar que a regra funciona corretamente]
```

## Exemplo Completo

### DET-042: Brute Force SSH Detection
- **MITRE**: T1110.001 - Brute Force: Password Guessing
- **Severity**: High
- **Logic**: `auth.type=ssh AND event=failed_login | stats count by src_ip | where count > 10 in 5min`
- **False Positives**: Scanning de vulnerabilidade autorizado, sistemas de monitoramento
- **Tuning**: Excluir IPs de scanners autorizados via whitelist
- **Test**: Executar 15 tentativas SSH com senha incorreta em 5 minutos

## Lifecycle da Regra

1. Draft: Hipotese de deteccao documentada
2. Review: Revisao por peer do time de detection engineering
3. Testing: Validacao em ambiente de teste
4. Tuning: Ajuste baseado em dados reais de producao
5. Production: Regra ativa gerando alertas
6. Periodic Review: Revisao trimestral de eficacia
