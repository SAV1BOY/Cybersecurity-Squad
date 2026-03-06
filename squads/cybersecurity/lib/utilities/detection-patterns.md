# Detection Patterns

Padroes reutilizaveis para criacao de regras de deteccao de ameacas.

## Pattern: Threshold-based Detection

Detecta atividade que excede um limiar definido em janela de tempo.
```
Exemplo: Brute force
Logica: count(failed_login) > 10 within 5m group by src_ip
Tuning: Ajustar threshold e janela conforme baseline do ambiente
```

## Pattern: Anomaly-based Detection

Detecta desvios do comportamento normal estabelecido via baseline.
```
Exemplo: Login anomalo
Logica: login_location NOT IN user_baseline_locations
         OR login_time NOT IN user_baseline_hours
Tuning: Periodo de baseline minimo de 30 dias
```

## Pattern: Sequence Detection

Detecta sequencia especifica de eventos em ordem temporal.
```
Exemplo: Credential access seguido de lateral movement
Logica: event_A(lsass_access) followed_by event_B(smb_connection)
        within 30m same_host
Tuning: Janela temporal e correlacao por host/user
```

## Pattern: Absence Detection

Detecta a ausencia de evento esperado (heartbeat, check-in).
```
Exemplo: Agente EDR silencioso
Logica: NOT seen(edr_heartbeat) for host within 24h
Tuning: Excluir hosts em manutencao programada
```

## Pattern: New/First Seen

Detecta primeira ocorrencia de entidade ou comportamento.
```
Exemplo: Novo servico executavel
Logica: service_created WHERE service_path NOT IN known_services
Tuning: Manter lista de servicos aprovados atualizada
```

## Pattern: Known Bad (IOC Match)

Detecta indicadores de comprometimento conhecidos.
```
Exemplo: Conexao a C2 conhecido
Logica: dest_ip IN threat_intel_feed OR dest_domain IN malicious_domains
Tuning: Atualizar feeds diariamente, gerenciar false positives
```

## Pattern: Impossible Travel

Detecta logins de localizacoes geograficamente impossiveis.
```
Exemplo: Login do Brasil e da Russia em 30 minutos
Logica: distance(login_1.geo, login_2.geo) / time_diff > max_travel_speed
Tuning: Considerar VPNs e proxies corporativos
```

## Combinacao de Patterns

Deteccoes mais robustas combinam multiplos patterns. Exemplo:
threshold (multiplos failed logins) + sequence (seguido de successful login)
+ anomaly (de localizacao incomum) = alta confianca de account compromise.
