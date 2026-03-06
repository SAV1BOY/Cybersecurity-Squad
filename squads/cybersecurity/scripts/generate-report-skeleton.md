# Generate Report Skeleton

Script para gerar a estrutura base de um relatorio de seguranca.

## Descricao

Cria automaticamente a estrutura de pastas e o documento base para um novo relatorio, preenchendo metadados e secoes obrigatorias conforme o template padrao.

## Inputs

- `report_type` - Tipo de relatorio (pentest, incident, review, compliance)
- `engagement_id` - Identificador do engagement (ex: ENG-2026-015)
- `target_name` - Nome do sistema ou cliente alvo
- `author` - Nome do autor principal
- `date` - Data de inicio (formato YYYY-MM-DD)

## Logica

1. Validar que o `engagement_id` segue o formato padrao (ENG-YYYY-NNN)
2. Criar pasta do engagement conforme naming convention: `[engagement_id]-[target_name]/`
3. Criar subpastas: `evidence/`, `reports/`, `notes/`, `tools/`
4. Selecionar template base conforme `report_type`
5. Preencher metadados no template: engagement_id, target_name, author, date
6. Gerar secoes obrigatorias conforme tipo de relatorio
7. Incluir classificacao de confidencialidade padrao no cabecalho
8. Salvar documento base em `reports/`

## Templates por Tipo

| Tipo | Secoes Geradas |
|------|----------------|
| pentest | Executive Summary, Scope, Methodology, Findings, Recommendations, Appendix |
| incident | Executive Summary, Timeline, Impact, Root Cause, Actions Taken, Lessons Learned |
| review | Executive Summary, System Description, Assessment, Findings, Decision |
| compliance | Executive Summary, Scope, Framework, Control Assessment, Gaps, Evidence |

## Output

- Pasta de engagement criada com subpastas
- Documento base do relatorio com metadados preenchidos
- Log de criacao com timestamp e parametros utilizados

## Uso

```
generate-report-skeleton --type pentest --id ENG-2026-015 --target portal-cliente --author "Analyst Name" --date 2026-03-06
```

## Validacoes

- Rejeitar se engagement_id ja existir (evitar sobrescrita)
- Rejeitar se tipo de relatorio nao for reconhecido
- Alertar se a data informada for no futuro
