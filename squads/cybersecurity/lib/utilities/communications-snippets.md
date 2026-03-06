# Communications Snippets

Templates de comunicacao para diferentes cenarios de seguranca.

## Notificacao de Incidente (Interno)

```
Assunto: [SECURITY INCIDENT] [Severity] - [Titulo Breve]

Equipe,

Um incidente de seguranca foi identificado e esta sendo tratado pelo time de IR.

- Severidade: [Critical/High/Medium/Low]
- Impacto atual: [Descricao breve do impacto]
- Status: [Investigando/Contido/Em remediacao]
- Incident Commander: [Nome]

Acoes imediatas requeridas:
- [Acao 1 se aplicavel]

Proximo update: [Horario do proximo comunicado]
Canal de comunicacao: [Slack channel / bridge call]
```

## Notificacao a Clientes (Breach)

```
Prezado cliente,

Estamos escrevendo para informar sobre um incidente de seguranca que pode
ter afetado seus dados. Levamos a seguranca dos seus dados com extrema
seriedade e queremos ser transparentes sobre o ocorrido.

O que aconteceu: [Descricao factual e concisa]
Quando: [Periodo do incidente]
Dados potencialmente afetados: [Tipos de dados]
O que fizemos: [Acoes de contencao e remediacao]
O que voce pode fazer: [Recomendacoes ao usuario]
Proximo contato: [Quando enviaremos atualizacao]
```

## Escalacao para Lideranca

```
Para: [CISO / CTO / CEO]
Assunto: [ESCALATION] Incidente de seguranca requer atencao

Resumo executivo:
- [O que aconteceu em 1-2 frases]
- [Impacto potencial ao negocio]
- [Decisoes necessarias da lideranca]
- [Recomendacao do time de seguranca]
```

## Report de Vulnerabilidade (para Dev Team)

```
Assunto: [SECURITY FINDING] [Severity] - [Finding ID] - [Titulo]

Time de desenvolvimento,

Identificamos uma vulnerabilidade que requer atencao:

- Finding: [ID e titulo]
- Severidade: [Level] (CVSS: [score])
- Localizacao: [Endpoint/arquivo/componente]
- SLA para correcao: [Data limite]
- Documentacao completa: [Link para finding]
- Contato security: [Nome do analista]
```

## Comunicacao Pos-Incidente (All-Hands)

```
Equipe,

Gostaramos de compartilhar o resultado da investigacao do incidente
[INC-ID]. O postmortem completo esta disponivel em [link].

Principais aprendizados:
1. [Licao 1]
2. [Licao 2]
3. [Licao 3]

Obrigado a todos que contribuiram para a resposta.
```
