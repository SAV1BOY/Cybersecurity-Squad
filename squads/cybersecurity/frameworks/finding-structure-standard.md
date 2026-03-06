# Finding Structure Standard — Framework Interno

> Padrao obrigatorio para documentar qualquer finding de seguranca no squad.

## Estrutura do Finding

Todo finding DEVE conter as seguintes secoes:

### 1. Identificacao
```yaml
ID: CYBER-[ANO]-[SEQ]           # Ex: CYBER-2026-0042
Titulo: [Descricao curta e clara]
Severidade: Critical | High | Medium | Low | Informational
CVSS: [Score se aplicavel]
Risk Score: [Modelo interno]
CWE: [CWE-ID se aplicavel]
ATT&CK: [Technique ID se aplicavel]
Status: Open | In Remediation | Retest | Closed | Accepted Risk
```

### 2. Resumo Executivo (2-3 frases)
- O que foi encontrado
- Qual o impacto potencial ao negocio
- O que precisa ser feito

### 3. Descricao Tecnica
- O que e a vulnerabilidade/misconfiguration/fraqueza
- Onde foi encontrada (sistema, endpoint, funcao)
- Por que e um problema (contexto tecnico)

### 4. Prova de Conceito (PoC)
```
Passos para reproducao:
1. [Passo 1]
2. [Passo 2]
3. [Resultado observado]

Evidencia:
- Screenshot: [referencia ao arquivo]
- Request/Response: [captura]
- Comando utilizado: [comando]
- Hash da evidencia: [SHA-256]
```

### 5. Impacto
- **Confidencialidade**: Dados que podem ser acessados
- **Integridade**: Dados que podem ser alterados
- **Disponibilidade**: Servicos que podem ser afetados
- **Impacto ao negocio**: Consequencias praticas (financeiro, reputacional, regulatorio)

### 6. Recomendacao de Correcao
- **Fix primario**: A solucao ideal
- **Mitigacao temporaria**: Se o fix leva tempo
- **Esforco estimado**: Baixo/Medio/Alto
- **Owner sugerido**: Time responsavel

### 7. Referencias
- CVE/CWE links
- OWASP/NIST referencia
- Documentacao do vendor
- Artigos tecnicos relevantes

### 8. Metadata
```yaml
Descoberto por: [Agente/Analista]
Data de descoberta: [YYYY-MM-DD]
Engajamento: [ID do projeto]
Asset: [Sistema/aplicacao]
Ambiente: [Producao/Staging/Dev]
Retestado: [Sim/Nao — data]
```

## Regras

1. **Sem finding sem prova** — PoC obrigatoria ou nao e finding
2. **Sem jargao desnecessario** — Clareza para qualquer leitor tecnico
3. **Impacto em termos de negocio** — Nao apenas "RCE possivel" mas "atacante pode acessar banco de dados de clientes"
4. **Correcao acionavel** — "Adicionar validacao de input no parametro X" nao "melhorar seguranca"
5. **Evidencia com integridade** — Hash SHA-256 de toda evidencia
