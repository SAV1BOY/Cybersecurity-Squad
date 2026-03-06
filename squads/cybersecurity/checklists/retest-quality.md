# Retest Quality Gate

Checklist de qualidade para reteste de vulnerabilidades.

## Preparacao do Retest
- [ ] Lista de findings originais obtida com status de remediacao
- [ ] Ambiente de teste confirmado (mesmo ambiente do assessment original)
- [ ] Acesso e credenciais verificados e funcionais
- [ ] Tools e payloads originais disponíveis para reproducao
- [ ] Scope do retest acordado (apenas remediated items vs full retest)
- [ ] Janela de teste confirmada com o cliente

## Execucao do Retest
- [ ] Cada finding retestado usando o mesmo PoC original
- [ ] Variantes do ataque original testadas para bypass
- [ ] Fix implementation verificada (nao apenas sintoma, mas root cause)
- [ ] Regression testing realizado em funcionalidades adjacentes
- [ ] Novas attack vectors testados que possam ter surgido com o fix
- [ ] Evidence coletada para cada finding (fixed ou still vulnerable)

## Classificacao dos Resultados
- [ ] Cada finding classificado: Fixed, Partially Fixed, Not Fixed, New Issue
- [ ] Partially Fixed items com detalhamento do que falta
- [ ] Not Fixed items com analise se houve tentativa de correcao
- [ ] New findings identificados durante retest documentados separadamente
- [ ] Risk score atualizado para findings parcialmente corrigidos

## Evidencias
- [ ] Screenshot ou request/response para cada finding retestado
- [ ] Comparacao before/after documentada
- [ ] Timestamp de cada teste registrado
- [ ] Tool output salvo como evidencia complementar
- [ ] Command history preservado para reproducibilidade

## Reporting
- [ ] Retest report com status consolidado de cada finding
- [ ] Metricas de remediacao calculadas (% fixed, % open, % new)
- [ ] Executive summary com progresso geral
- [ ] Recommendations para findings ainda abertos
- [ ] Timeline para proximo retest definida (se necessario)
- [ ] Report revisado por peer antes de entrega

## Encerramento
- [ ] Stakeholders notificados sobre resultados do retest
- [ ] Remediation tracker atualizado com novos status
- [ ] Criterios de aceite do engagement verificados
- [ ] Sign-off do cliente obtido para findings fechados
