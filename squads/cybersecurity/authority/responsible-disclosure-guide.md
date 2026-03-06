# Responsible Disclosure Guide

Guia para conducao de responsible disclosure de vulnerabilidades.

## Processo como Descobridor

### 1. Documentacao Inicial
- Documentar a vulnerabilidade com detalhes tecnicos
- Capturar evidencias (screenshots, requests, logs)
- Avaliar severidade e impacto potencial
- NAO explorar alem do necessario para confirmacao

### 2. Contato com o Vendor
- Buscar canal oficial: security.txt, security@, bug bounty program
- Enviar report inicial com detalhes tecnicos
- Usar criptografia (PGP) quando possivel
- Definir expectativa de timeline (90 dias e padrao da industria)

### 3. Coordenacao
- Trabalhar com o vendor no entendimento da vulnerabilidade
- Fornecer informacoes adicionais quando solicitado
- Concordar em timeline de disclosure mutuamente aceitavel
- Testar e validar o fix quando solicitado

### 4. Publicacao
- Publicar apos fix disponivel e timeline acordada
- Incluir credito adequado e timeline de coordenacao
- Fornecer detalhes tecnicos uteis para a comunidade
- Respeitar embargo se acordado

## Processo como Receptor de Reports

### Estrutura do Programa
- Pagina security.txt no dominio principal
- Email security@ monitorado ativamente
- Politica de safe harbor publica
- SLA de resposta definido e comunicado

### SLAs de Resposta

| Acao | SLA |
|------|-----|
| Acknowledge do report | 24 horas |
| Triagem e avaliacao inicial | 72 horas |
| Feedback sobre validade | 5 dias uteis |
| Fix para Critical | 30 dias |
| Fix para High | 60 dias |
| Fix para Medium/Low | 90 dias |

### Template de Resposta
```
Agradecemos seu report de seguranca.

Confirmamos o recebimento e iniciaremos a analise em ate 72h.
Sua referencia: [REPORT-ID]
Contato: [security-team-email]

Operamos sob politica de responsible disclosure com safe harbor
para pesquisadores de boa-fe agindo dentro do escopo definido.
```

## Safe Harbor

Pesquisadores que atuam de boa-fe, dentro do escopo definido e
sem causar dano intencional nao serao processados. Esta politica
deve ser publicada claramente e aprovada pelo departamento legal.

## Recompensas

Definir se o programa oferece recompensa monetaria (bug bounty),
reconhecimento publico (hall of fame), ou ambos.
