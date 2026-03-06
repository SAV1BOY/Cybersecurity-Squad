# False Positive Reduction Cases

Casos praticos de reducao de false positives para melhorar signal-to-noise ratio.

## Metricas de FP Rate

- **Aceitavel:** < 10% de FP em regras critical/high
- **Necessita tuning:** 10-30% FP rate
- **Desabilitar e reescrever:** > 30% FP rate

## Caso 1: Brute Force Alert com Service Accounts

**Problema:** Regra de failed logins gerando 200+ alertas/dia por service accounts.
**Root Cause:** Service accounts com password rotation geravam burst de failed auth.
**Solucao:** Exclusion list de service accounts + regra separada para monitorar SAs.
**Resultado:** Reducao de 85% nos alertas, zero impacto em deteccao real.

## Caso 2: Suspicious PowerShell Execution

**Problema:** Alerta em encoded PowerShell disparando para scripts legitimos de IT.
**Root Cause:** Time de automacao usava encoded commands em scripts de deploy.
**Solucao:** Allowlist por parent process + path de execucao do tooling de IT.
**Resultado:** FP rate caiu de 60% para 5%.

## Caso 3: Data Exfiltration por Volume

**Problema:** Alertas de upload volumetrico para cloud storage.
**Root Cause:** Backups e sincronizacao de ferramentas corporativas (OneDrive, GDrive).
**Solucao:** Baseline por usuario + exclusao de destinos corporativos aprovados.
**Resultado:** Alertas reduziram de 50/dia para 3/dia com melhor fidelidade.

## Framework de Reducao de FP

1. Coletar FP samples por 2 semanas
2. Categorizar por root cause
3. Implementar suppressions granulares (nunca genericas)
4. Validar que true positives nao foram suprimidos
5. Documentar cada suppression com justificativa
6. Revisar suppressions trimestralmente
