# Fail Secure Pattern

Padrao que garante que falhas no sistema resultem em estado seguro, nao permissivo.

## Principio

Quando um componente de seguranca falha, o comportamento padrao deve ser
negar acesso ou manter protecao, nunca falhar para um estado aberto.

## Fail Secure vs Fail Open

| Cenario | Fail Open (inseguro) | Fail Secure (correto) |
|---------|---------------------|----------------------|
| WAF indisponivel | Trafego passa direto | Trafego bloqueado |
| Auth service down | Acesso liberado | Acesso negado |
| MFA timeout | Login sem MFA | Login negado |
| Certificate expired | Conexao aceita | Conexao recusada |
| Rate limiter crash | Sem limite | Requests bloqueados |

## Implementacao

### Authentication
```
# Fail open (ERRADO)
def authenticate(user):
    try:
        return auth_service.verify(user)
    except ServiceUnavailable:
        return True  # PERIGO: bypass de autenticacao

# Fail secure (CORRETO)
def authenticate(user):
    try:
        return auth_service.verify(user)
    except ServiceUnavailable:
        log.critical("Auth service unavailable")
        return False  # Acesso negado por seguranca
```

### Authorization
- Default deny em todas as politicas de acesso
- Whitelist > blacklist para regras de firewall
- Permissoes explicitas, nunca implicitas

### Error Handling
- Nao expor stack traces ou detalhes internos em erros
- Retornar mensagens genericas ao usuario
- Logar detalhes tecnicos internamente para debug

## Excecoes Controladas

Em cenarios onde fail secure causa indisponibilidade critica
(ex: sistema de emergencia), documentar formalmente a decisao
de fail open com controles compensatorios e monitoramento.

## Validacao

Testar regularmente o comportamento de falha de componentes criticos:
- Desligar auth service e verificar que acesso e negado
- Simular falha do WAF e confirmar bloqueio de trafego
- Testar timeout de servicos dependentes
