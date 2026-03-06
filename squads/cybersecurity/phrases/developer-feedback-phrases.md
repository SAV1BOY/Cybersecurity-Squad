# Developer Feedback Phrases

Frases padronizadas para fornecer feedback de seguranca a desenvolvedores de forma construtiva.

## Feedback Positivo

- "O tratamento de input validation neste modulo esta bem implementado e segue as melhores praticas de secure coding."
- "Excelente uso de prepared statements para prevenir SQL injection. Este e o padrao que queremos ver em todo o codebase."
- "A implementacao de rate limiting na API demonstra atencao a protecao contra abuse, parabens pela iniciativa."
- "O code review mostrou uma evolucao significativa na adocao de praticas seguras em comparacao com releases anteriores."

## Feedback Corretivo - Tom Colaborativo

- "Identificamos uma oportunidade de melhoria no tratamento de autenticacao neste endpoint. Podemos agendar um papo rapido para discutir?"
- "O pattern utilizado para gerenciamento de secrets pode expor credenciais em logs. Sugerimos utilizar a abordagem documentada em [link]."
- "Notamos que a validacao de input nao cobre todos os campos do formulario. Complementar essa validacao preveniria ataques de injection."
- "A dependencia [nome] possui uma vulnerabilidade conhecida. Atualizar para a versao [numero] resolve o problema sem breaking changes."

## Explicacao de Riscos para Desenvolvedores

- "Sem essa correcao, um atacante poderia manipular os parametros da request para acessar dados de outros usuarios."
- "O risco aqui e que dados sensiveis ficam expostos em texto claro nos logs, o que facilita acesso nao autorizado."
- "Essa vulnerabilidade de Cross-Site Scripting (XSS) permitiria a execucao de JavaScript malicioso no browser de outros usuarios."
- "A ausencia de CSRF tokens neste formulario possibilita que um atacante induza acoes em nome de usuarios autenticados."

## Orientacoes Praticas

- "Para corrigir este finding, recomendamos substituir [codigo inseguro] por [codigo seguro]. Exemplo disponivel em [link]."
- "Nosso secure coding guide cobre este cenario no capitulo [N]. Vale a leitura para entender o contexto completo."
- "O OWASP Cheat Sheet para [topico] tem exemplos praticos que podem ajudar na implementacao segura."
- "Se tiver duvidas sobre como implementar esta correcao, o security champion do seu time pode auxiliar."

## Solicitacao de Mudancas

- "Pedimos que esta correcao seja aplicada antes do merge, pois o finding e de severidade alta e afeta dados de clientes."
- "Este item pode ser corrigido no proximo sprint, mas recomendamos nao deixar para alem disso dado o risco associado."
- "Entendemos que a correcao ideal requer refactoring significativo. Como alternativa imediata, sugerimos [mitigacao]."

## Agradecimento e Encerramento

- "Agradecemos a receptividade ao feedback. Seguranca e um esforco coletivo e sua contribuicao faz diferenca."
- "Estamos disponiveis para pair programming se precisar de apoio na implementacao das correcoes sugeridas."
- "Ótimo trabalho no geral. Os pontos levantados sao ajustes que elevam ainda mais a qualidade do codigo."
