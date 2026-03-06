# Detection Coverage Matrix — Framework Interno

> Mapear MITRE ATT&CK -> fontes de log -> regras de deteccao -> gaps.

## Objetivo

A Detection Coverage Matrix e o dashboard principal do Blue Team. Mostra para cada tecnica ATT&CK relevante: se temos fonte de log, se temos regra de deteccao, se a regra foi testada, e qual a taxa de falsos positivos. Gaps nesta matriz sao blind spots.

## Estrutura da Matriz

```
| ATT&CK Technique | Tactic | Log Source | Rule Exists | Rule Tested | FP Rate | Status |
|-------------------|--------|------------|-------------|-------------|---------|--------|
| T1566.001 Phishing | Initial Access | Email Gateway | Yes | Yes | Low | Active |
| T1059.001 PowerShell | Execution | EDR + Sysmon | Yes | Yes | Medium | Tuning |
| T1053.005 Sched Task | Persistence | Sysmon | No | - | - | GAP |
```

## Como Construir

### 1. Selecionar Tecnicas Relevantes
- Nao mapear TODAS as tecnicas (500+) — focar nas relevantes ao ambiente
- Usar threat intelligence para priorizar
- Considerar industria e threat landscape
- Top priorities: Initial Access, Execution, Persistence, Lateral Movement, Exfiltration

### 2. Mapear Log Sources
Para cada tecnica, identificar:
- Qual log mostraria esta atividade?
- O log esta sendo coletado?
- Qual a retencao?
- Qual a completude (todos os hosts, ou parcial)?

### 3. Mapear Regras de Deteccao
Para cada tecnica com log source:
- Existe regra de deteccao?
- A regra foi testada (simulacao)?
- Qual a taxa de FP?
- Quando foi revisada pela ultima vez?

### 4. Identificar Gaps
Gaps sao priorizados por:
1. **Tecnicas usadas por threat actors relevantes** (intel-driven)
2. **Tecnicas sem nenhuma visibilidade** (blind spots)
3. **Tecnicas com regra nao-testada** (deteccao teorica)
4. **Tecnicas com alto FP** (regra inutil)

## Metricas Derivadas

- **Coverage %**: Tecnicas com regra ativa / Total de tecnicas relevantes
- **Tested %**: Regras testadas com simulacao / Total de regras
- **Gap count por tatica**: Quantos gaps por cada fase da kill chain
- **FP rate medio**: Media de FP rate das regras ativas
- **Time since last test**: Quanto tempo desde ultima validacao

## Cadencia de Atualizacao

| Atividade | Frequencia |
|-----------|-----------|
| Review de coverage | Mensal |
| Adicionar novas regras | Semanal (sprint) |
| Testar regras existentes | Quinzenal (purple team mini) |
| Update de threat intel | Semanal |
| Full coverage report | Trimestral |

## Agentes Envolvidos

- **Chris Sanders**: Design de regras, analise de gaps, hunting
- **Omar Santos**: Log source coverage, SOC readiness
- **Shannon Runner**: Pattern analysis, anomaly-based detection
- **Rogue**: Adversary simulation para testar regras

## Output

- `trackers/detection-coverage-tracker.md` — Dashboard atualizado
- `data/registries/detection-rules-registry.md` — Catalogo de regras
- Gap report com priorizacao
- Sprint backlog de novas deteccoes
