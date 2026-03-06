# Remediation Component

Componente para documentacao padronizada de recomendacoes de remediacao.

## Estrutura

```
## Remediation: [Finding ID]

### Quick Fix (Short-term)
[Acao imediata para mitigar o risco, implementavel em < 48h]

### Permanent Fix (Long-term)
[Solucao definitiva que endereca a root cause]

### Implementation Steps
1. [Passo 1 com detalhes tecnicos]
2. [Passo 2]
3. [Passo N]

### Code Example (when applicable)
[Exemplo de codigo corrigido vs vulneravel]

### Verification
[Como validar que a correcao foi efetiva]

### Effort Estimate
[Low | Medium | High] - [Estimativa em horas/dias]

### Dependencies
[Pre-requisitos ou dependencias para implementacao]
```

## Principios de Remediacao

- **Especifica**: Instrucoes claras, nao genericas
- **Acionavel**: Implementavel pelo time de desenvolvimento
- **Verificavel**: Inclui forma de confirmar a correcao
- **Priorizada**: Quick fix primeiro, solucao definitiva depois

## Exemplos

### SQL Injection
- Quick fix: WAF rule para bloquear payloads comuns
- Permanent fix: Parameterized queries em todo o data access layer
- Verificacao: Retest com mesmos payloads + fuzzing adicional

### Missing Authentication
- Quick fix: Adicionar middleware de autenticacao na rota
- Permanent fix: Implementar authorization framework centralizado
- Verificacao: Tentar acessar endpoint sem token valido

## Anti-Patterns

- Evitar: "Corrigir a vulnerabilidade" (vago)
- Evitar: Recomendacoes que requerem rewrite completo sem alternativa
- Evitar: Ignorar controles compensatorios como opcao intermediaria
