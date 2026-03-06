# Naming Conventions

Convencoes de nomenclatura para arquivos, artefatos e identificadores do Cybersecurity Squad.

## Arquivos e Documentos

### Regras Gerais
- Usar kebab-case (palavras separadas por hifen): `pentest-engagement-workflow.md`
- Apenas letras minusculas, numeros e hifens
- Extensao adequada ao formato (.md, .json, .yaml, .py)
- Nomes descritivos que indiquem o conteudo

### Relatorios
- Formato: `[tipo]-[cliente-ou-sistema]-[data].pdf`
- Exemplo: `pentest-portal-cliente-2026-03-06.pdf`
- Data no formato ISO 8601 (YYYY-MM-DD)

### Evidencias
- Formato: `[finding-id]-[descricao-curta]-[sequencia].[ext]`
- Exemplo: `FIND-001-sqli-login-page-01.png`
- Sequencia numerica com zero-padding de 2 digitos

## Identificadores

### Findings
- Formato: `FIND-[NNN]`
- Numeracao sequencial por engagement
- Exemplo: `FIND-001`, `FIND-042`

### Incidentes
- Formato: `INC-[YYYY]-[NNNN]`
- Numeracao sequencial por ano
- Exemplo: `INC-2026-0001`

### Engagements
- Formato: `ENG-[YYYY]-[NNN]`
- Exemplo: `ENG-2026-015`

### Risk Acceptances
- Formato: `RA-[YYYY]-[NNN]`
- Exemplo: `RA-2026-003`

### Detection Rules
- Formato: `DET-[tactic]-[NNN]`
- Tactic abreviada do ATT&CK
- Exemplo: `DET-EXEC-001`, `DET-LATMOV-015`

## Branches e Commits

### Branches
- Formato: `[tipo]/[descricao-curta]`
- Tipos: `feature/`, `fix/`, `docs/`, `update/`
- Exemplo: `feature/new-detection-rule-ransomware`

### Commits
- Mensagem em ingles, imperativo, maximo 72 caracteres na primeira linha
- Exemplo: `Add detection rule for Kerberoasting technique`

## Tags e Labels

### Severidade
- Usar exatamente: `critical`, `high`, `medium`, `low`, `informational`
- Nunca usar variacoes como "crit", "med", "info"

### Status
- Usar exatamente: `open`, `in-progress`, `pending-validation`, `closed`, `risk-accepted`
- Nunca usar variacoes nao padronizadas

### Categorias de Finding
- Usar categorias padronizadas: `injection`, `authentication`, `authorization`, `cryptography`, `configuration`, `information-disclosure`

## Pastas de Engagement

- Formato: `[ENG-ID]-[nome-cliente-ou-sistema]/`
- Subpastas padrao: `evidence/`, `reports/`, `notes/`, `tools/`
- Exemplo: `ENG-2026-015-portal-cliente/evidence/`
