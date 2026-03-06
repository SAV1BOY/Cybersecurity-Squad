# Task: Vulnerability Validation

## Objetivo
Validar vulnerabilidades identificadas durante recon e scanning, confirmando explorabilidade real e descartando falsos positivos com evidencia reproduzivel.

## Agents
- **georgia-weidman** (lead) — Valida exploits e PoCs
- **peter-kim** (support) — Prioriza por attack path e impacto
- **fuzzer** (executor) — Fuzzing para descoberta adicional

## Inputs
- Resultados de recon e enumeracao
- Scan results (vulnerability scanners)
- CVE database e exploit databases relevantes

## Steps
1. Triar vulnerabilidades por severidade e contexto de negocio
2. Descartar falsos positivos com validacao manual
3. Confirmar exploitability com PoC minimo e nao destrutivo
4. Executar fuzzing direcionado em endpoints suspeitos
5. Validar CVEs contra versoes confirmadas de servicos
6. Classificar cada vuln usando Risk Scoring Model interno
7. Mapear vulnerabilidades contra attack paths potenciais
8. Documentar PoC reproduzivel para cada vuln confirmada
9. Capturar evidencias com timestamps e hash SHA-256
10. Registrar findings no `findings-registry`

## Output
- Lista de vulnerabilidades validadas com PoC
- Classificacao de severidade por Risk Scoring Model
- Falsos positivos documentados e descartados
- Evidencias hasheadas (SHA-256) por finding

## Quality Gates
- [ ] Cada vuln confirmada tem PoC reproduzivel
- [ ] Falsos positivos explicitamente descartados com justificativa
- [ ] Severidade classificada pelo Risk Scoring Model
- [ ] Evidencias com timestamp e hash SHA-256
- [ ] Exploits executados de forma nao destrutiva
- [ ] Checklist `weidman-exploitation-validation` atendido
- [ ] Checklist `evidence-chain-quality` validado
