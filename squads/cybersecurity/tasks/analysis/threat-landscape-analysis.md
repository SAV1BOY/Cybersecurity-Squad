# Task: Threat Landscape Analysis

## Objetivo
Analisar o cenario de ameacas relevante ao setor e organizacao, identificando threat actors, TTPs emergentes e tendencias que devem informar a estrategia de seguranca.

## Agents
- **cyber-chief** (lead) — Direciona analise estrategica
- **rogue** (support) — Fornece perspectiva adversaria e TTPs

## Inputs
- Threat intelligence feeds e reports
- MITRE ATT&CK e MITRE ATLAS
- Informacoes do setor e vertical de negocio
- Incidentes publicos relevantes ao setor

## Steps
1. Coletar threat intelligence de fontes multiplas (OSINT, feeds, ISACs)
2. Identificar threat actors relevantes ao setor (APTs, cybercrime, hacktivism)
3. Mapear TTPs mais utilizados por threat actors relevantes
4. Analisar tendencias emergentes (ransomware, supply chain, AI-based attacks)
5. Avaliar aplicabilidade de novas tecnicas ao ambiente da organizacao
6. Mapear gaps de deteccao contra TTPs mais provaveis
7. Identificar oportunidades de proactive defense
8. Priorizar recomendacoes por probabilidade e impacto
9. Gerar threat landscape brief para stakeholders
10. Registrar no `security-kpis`

## Output
- Threat landscape brief com threat actors e TTPs relevantes
- Mapeamento de TTPs contra deteccao existente
- Tendencias emergentes com avaliacao de impacto
- Recomendacoes de defesa proativa

## Quality Gates
- [ ] Threat intelligence de fontes multiplas e confiáveis
- [ ] Threat actors relevantes ao setor identificados
- [ ] TTPs mapeados contra MITRE ATT&CK
- [ ] Tendencias emergentes avaliadas quanto a impacto
- [ ] Recomendacoes de defesa proativa priorizadas
- [ ] Checklist `threat-hunt-quality` validado
