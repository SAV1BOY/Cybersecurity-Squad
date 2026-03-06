# Task: Report Findings

## Objetivo
Consolidar todos os findings do Red Team em relatorio tecnico e executivo, com attack paths narrativos, evidencia reproduzivel e recomendacoes acionaveis.

## Agents
- **peter-kim** (lead) — Redige relatorio tecnico e executivo
- **cyber-chief** (reviewer) — Revisa qualidade e alinhamento estrategico

## Inputs
- Todos os findings registrados no `findings-registry`
- Evidencias coletadas durante o engagement
- Risk Scoring Model para classificacao de severidade
- Templates de report (technical e executive summary)

## Steps
1. Consolidar todos os findings por categoria e severidade
2. Construir attack path narrativos (nao apenas vulns isoladas)
3. Classificar cada finding usando Risk Scoring Model
4. Redigir descricao tecnica com PoC reproduzivel para cada finding
5. Descrever impacto em termos de negocio (nao apenas tecnico)
6. Elaborar recomendacoes acionaveis e especificas por finding
7. Escrever executive summary em 1 pagina para C-level
8. Incluir metricas agregadas do engagement
9. Validar que nenhum dado sensivel real aparece no relatorio
10. Submeter para review usando checklist de qualidade

## Output
- Relatorio tecnico completo com findings e attack paths
- Executive summary de 1 pagina
- Evidencias organizadas e referenciadas no relatorio
- Registro final no `findings-registry`

## Quality Gates
- [ ] Todos os findings tem PoC reproduzivel
- [ ] Attack paths narrativos documentados (nao apenas vulns isoladas)
- [ ] Impacto descrito em termos de negocio
- [ ] Recomendacoes acionaveis e especificas
- [ ] Executive summary compreensivel para nao-tecnicos
- [ ] Nenhum dado sensivel real no relatorio
- [ ] Evidencias hasheadas (SHA-256) e referenciadas
- [ ] Checklist `security-report-quality` 100% atendido
- [ ] Checklist `kim-proof-and-reporting` validado
