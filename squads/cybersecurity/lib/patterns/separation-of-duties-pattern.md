# Separation of Duties Pattern

Padrao que distribui responsabilidades criticas entre multiplas pessoas ou sistemas.

## Principio

Nenhuma pessoa deve ter controle completo sobre um processo critico.
Dividir responsabilidades previne fraude, erros e abuso de privilegios.

## Aplicacoes em Seguranca

### Change Management
- Quem escreve o codigo nao aprova o merge
- Quem aprova o merge nao faz o deploy
- Quem faz deploy nao tem acesso direto a producao

### Access Management
- Quem solicita acesso nao aprova a solicitacao
- Quem aprova nao implementa a concessao
- Reviews periodicos por terceiro independente

### Financial Controls
- Quem inicia transacao nao autoriza pagamento
- Limites de aprovacao por nivel hierarquico
- Reconciliacao por equipe independente

### Security Operations
- Quem cria regras de deteccao nao as desabilita sozinho
- Quem investiga incidentes nao fecha sem peer review
- Quem concede excecoes nao e o beneficiario

## Implementacao Tecnica

### Git Workflow
```
Branch protection rules:
- Require pull request reviews: 1+ approver
- Require code owner review
- Dismiss stale reviews on new commits
- Restrict who can push to main
```

### CI/CD Pipeline
- Build, test e deploy executados por service accounts distintas
- Secrets gerenciados por equipe diferente de quem faz deploy
- Audit log imutavel de todas as acoes no pipeline

### Cloud IAM
- Separate admin accounts por funcao
- Aprovacao dual para operacoes destrutivas
- Break-glass com notificacao automatica

## Desafios em Times Pequenos

Em equipes reduzidas, separation of duties pura pode ser impraticavel.
Controles compensatorios incluem: logging detalhado, alertas em tempo real
para acoes sensiveis e revisoes retrospectivas regulares.
