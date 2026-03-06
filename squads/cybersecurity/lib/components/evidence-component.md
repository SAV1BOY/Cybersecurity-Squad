# Evidence Component

Componente para coleta e documentacao padronizada de evidencias de seguranca.

## Tipos de Evidencia

### HTTP Request/Response
```
Request:
POST /api/v2/users/search HTTP/1.1
Host: target.example.com
Content-Type: application/json
Authorization: Bearer [REDACTED]

{"query": "test' UNION SELECT username,password FROM users--"}

Response:
HTTP/1.1 200 OK
Content-Type: application/json

{"results": [{"username":"admin","password":"$2b$12..."}]}
```

### Screenshot
- Captura de tela com timestamp visivel
- Highlight na area relevante
- Resolucao legivel sem zoom

### Log Entry
- Timestamp, source, mensagem completa
- Contexto (linhas anteriores e posteriores)
- Correlacao com outros eventos quando relevante

### Code Snippet
- Trecho de codigo vulneravel com linha e arquivo
- Versao corrigida para comparacao quando possivel

## Requisitos de Evidencia

| Criterio | Descricao |
|----------|-----------|
| Autenticidade | Evidencia nao alterada, com metadata preservada |
| Timestamp | Data e hora da coleta claramente registrados |
| Reprodutibilidade | Passos para reproduzir o finding documentados |
| Redacao | Dados sensiveis reais redactados (tokens, senhas) |
| Cadeia de Custodia | Quem coletou, quando e como armazenado |

## Ferramentas de Coleta

- **Burp Suite**: Proxy logs, request/response pairs
- **Screenshots**: Flameshot, ShareX com timestamp overlay
- **Logs**: Exportacao direta do SIEM ou ferramenta de origem
- **Network**: Wireshark pcap files para evidencia de rede

## Armazenamento

Evidencias armazenadas em repositorio seguro com controle de acesso.
Retencao minima de 1 ano apos encerramento do engagement.
Nomeacao: `[FINDING-ID]_[TYPE]_[TIMESTAMP].[EXT]`
