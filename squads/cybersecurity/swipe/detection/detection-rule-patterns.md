# Detection Rule Patterns

Padroes reutilizaveis para criacao de regras de deteccao eficazes.

## Categorias de Detection Patterns

### Threshold-Based
Detecta quando uma metrica excede um limite definido.
```yaml
rule: failed_login_threshold
condition: count(failed_auth) > 20 within 5m per source_ip
severity: medium
```

### Sequence-Based
Detecta uma sequencia especifica de eventos em ordem.
```yaml
rule: privilege_escalation_chain
sequence:
  - event: new_user_created
  - event: added_to_admin_group (within 10m)
  - event: sensitive_data_access (within 30m)
severity: critical
```

### Anomaly-Based
Detecta desvios do baseline comportamental.
```yaml
rule: unusual_data_transfer
condition: outbound_bytes > 3x baseline per user per hour
severity: high
```

### Negation-Based
Detecta ausencia de eventos esperados.
```yaml
rule: missing_heartbeat
condition: NOT received(edr_heartbeat) within 24h per endpoint
severity: medium
```

## Boas Praticas de Engineering

- Sempre definir false positive rate aceitavel antes de deploy
- Incluir suppression rules para cenarios conhecidos de FP
- Documentar MITRE ATT&CK mapping para cada regra
- Testar regras com dados historicos antes de ativar
- Implementar tuning period de 2 semanas para novas regras
- Manter runbook vinculado a cada regra de deteccao
