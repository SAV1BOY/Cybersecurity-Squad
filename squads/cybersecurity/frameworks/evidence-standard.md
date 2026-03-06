# Evidence Standard — Framework Interno

> Como capturar, armazenar e manter integridade de evidencias sem vazar segredos.

## Principios

1. **Integridade acima de tudo** — Toda evidencia e hasheada (SHA-256)
2. **Cadeia de custodia** — Quem coletou, quando, como, onde armazenou
3. **Minimizacao** — Capturar apenas o necessario para provar o finding
4. **Sanitizacao** — Remover dados sensiveis reais antes de incluir em relatorios
5. **Nao-repudio** — Evidencia deve ser verificavel por terceiros

## Tipos de Evidencia

### Screenshots
- Incluir timestamp visivel (relogio do sistema)
- Capturar contexto suficiente (URL, headers, response)
- Marcar (highlight) o ponto relevante
- Sanitizar dados pessoais/sensiveis com blur/redact
- Formato: PNG (sem compressao lossy)

### Request/Response Captures
- Incluir headers completos
- Redactar tokens/cookies com `[REDACTED]`
- Manter parametros relevantes intactos
- Formato: texto plano ou HAR file

### Command Output
```
Formato padrao:
[TIMESTAMP] $ [COMANDO]
[OUTPUT]
[HASH: SHA256 do output]
```

### Log Excerpts
- Incluir timestamps
- Manter contexto (linhas antes e depois)
- Marcar a linha relevante
- Fonte do log identificada

### Memory/Disk Dumps (IR)
- Hash SHA-256 antes e depois da coleta
- Chain of custody form preenchido
- Armazenamento cifrado
- Acesso restrito

## Chain of Custody

Para cada evidencia:
```yaml
evidence_id: EVD-[ANO]-[SEQ]
finding_id: CYBER-[ANO]-[SEQ]
collected_by: [Nome/Agente]
collection_date: [YYYY-MM-DD HH:MM UTC]
collection_method: [Ferramenta/processo]
original_hash: [SHA-256]
storage_location: [Referencia]
access_log:
  - [YYYY-MM-DD]: [Quem acessou] — [Motivo]
```

## Sanitizacao

### O que SEMPRE sanitizar:
- Nomes reais de usuarios/funcionarios
- Emails pessoais
- IPs internos de producao (substituir por 192.0.2.0/24 — RFC 5737)
- Tokens, API keys, passwords (substituir por `[REDACTED]`)
- Dados de clientes (PII, financeiro, saude)

### O que MANTER:
- Estrutura do request/response
- Error messages e stack traces (sanitizados)
- Versoes de software
- Configuracoes relevantes (sem secrets)
- Timestamps e sequencia de eventos

## Armazenamento

- Evidencias NUNCA ficam no repositorio git publico
- Armazenamento cifrado (AES-256) com acesso controlado
- Retencao minima: 1 ano apos fechamento do finding
- Retencao para IR/forense: conforme regulatorio (geralmente 5 anos)
- Backup da evidencia em local separado
