# Least Privilege Pattern

Padrao que garante que cada entidade tenha apenas as permissoes minimas necessarias.

## Principio

Conceder o minimo de privilegios necessarios para executar uma funcao,
pelo menor tempo possivel, no escopo mais restrito aplicavel.

## Aplicacao por Contexto

### IAM Users e Roles
- Permissoes baseadas em funcao (RBAC), nao em individuo
- Revisao trimestral de acessos (access review)
- Remocao imediata ao mudar de funcao ou sair
- Segregacao entre ambientes (dev/staging/prod)

### Service Accounts
- Permissoes scoped ao recurso especifico
- Sem permissoes wildcard (`*`)
- Rotacao automatica de credenciais
- Monitoramento de uso anomalo

### Database Access
- Usuarios de aplicacao com SELECT/INSERT apenas nas tabelas necessarias
- Sem acesso direto a producao para desenvolvedores
- Queries privilegiadas via stored procedures com audit log
- Break-glass accounts para emergencias com aprovacao

### Cloud Resources
```
# Anti-pattern (permissivo demais)
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*"
}

# Pattern correto (least privilege)
{
  "Effect": "Allow",
  "Action": ["s3:GetObject", "s3:PutObject"],
  "Resource": "arn:aws:s3:::my-bucket/app-data/*"
}
```

### Container Security
- Rodar como non-root user
- Read-only filesystem
- Drop all capabilities, add apenas necessarias
- Sem privilege escalation

## Implementacao Gradual

1. Auditar permissoes atuais de todos os usuarios e servicos
2. Mapear permissoes necessarias vs. concedidas
3. Criar politicas restritivas baseadas em uso real
4. Implementar com periodo de monitoramento (dry-run)
5. Enforcar e monitorar violacoes

## Metricas

- Percentual de contas com permissoes excessivas
- Numero de contas com acesso admin/root
- Tempo medio para revogar acesso apos offboarding
