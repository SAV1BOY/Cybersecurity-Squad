# Task: Evidence Collection

## Objetivo
Coletar, preservar e documentar evidencias digitais do incidente com cadeia de custodia integra, garantindo admissibilidade e reprodutibilidade.

## Agents
- **chris-sanders** (lead) — Coleta e preserva evidencias
- **shannon-runner** (executor) — Analisa entropia e artefatos

## Inputs
- Ativos afetados identificados na triagem
- Playbooks de coleta forense
- Ferramentas de coleta aprovadas
- Evidence standard do squad

## Steps
1. Identificar fontes de evidencia (memoria, disco, logs, rede, cloud)
2. Priorizar coleta por volatilidade (ordem de volatilidade RFC 3227)
3. Capturar memory dump de sistemas afetados (se aplicavel)
4. Coletar disk images ou triage packages
5. Exportar logs relevantes de SIEM, EDR e cloud providers
6. Capturar network traffic se captura ativa estiver disponivel
7. Calcular hash SHA-256 de cada peca de evidencia
8. Documentar cadeia de custodia para cada item
9. Armazenar evidencias em repositorio seguro e imutavel
10. Registrar no `incident-registry`

## Output
- Colecao de evidencias com hash SHA-256
- Cadeia de custodia documentada por item
- Timeline de eventos baseada em evidencias
- Registro no `incident-registry`

## Quality Gates
- [ ] Ordem de volatilidade respeitada na coleta
- [ ] Hash SHA-256 calculado para cada peca de evidencia
- [ ] Cadeia de custodia documentada sem gaps
- [ ] Evidencias armazenadas em repositorio seguro e imutavel
- [ ] Memory dumps coletados antes de shutdown (quando possivel)
- [ ] Checklist `forensics-collection-quality` atendido
- [ ] Checklist `sanders-evidence-integrity` validado
