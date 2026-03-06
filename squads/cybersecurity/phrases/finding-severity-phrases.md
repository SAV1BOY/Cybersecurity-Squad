# Finding Severity Phrases

Frases padronizadas para descrever a severidade de findings de seguranca em relatorios.

## Critical Severity

- "Esta vulnerabilidade permite execucao remota de codigo sem autenticacao, representando risco imediato de comprometimento total do sistema."
- "O finding classificado como critical indica que um adversario pode explorar esta falha para obter controle completo do ambiente afetado."
- "A exploracao desta vulnerabilidade resulta em acesso irrestrito a dados sensiveis sem necessidade de credenciais validas."
- "Dada a facilidade de exploracao e o impacto potencial, este finding exige remediacao imediata dentro do SLA de emergencia."

## High Severity

- "Esta vulnerabilidade permite escalacao de privilegios, possibilitando que um usuario com acesso limitado obtenha permissoes administrativas."
- "O finding de alta severidade indica exposicao de dados confidenciais que pode resultar em impacto regulatorio significativo."
- "A exploracao requer autenticacao previa, porem o impacto pos-exploracao justifica classificacao como high severity."
- "Recomendamos remediacao prioritaria deste finding dentro do SLA de 15 dias uteis para vulnerabilidades de alta severidade."

## Medium Severity

- "Esta vulnerabilidade requer condicoes especificas para exploracao, limitando a probabilidade de abuso em cenario real."
- "O finding de severidade media indica uma fraqueza que, combinada com outros fatores, pode elevar o risco ao ambiente."
- "Embora o impacto direto seja contido, a presenca desta vulnerabilidade amplia a attack surface do sistema."
- "Recomendamos correcao dentro do SLA padrao de 30 dias uteis para findings de media severidade."

## Low Severity

- "Este finding representa uma fraqueza de seguranca com impacto limitado e baixa probabilidade de exploracao."
- "A vulnerabilidade identificada e de natureza informativa e nao representa risco iminente ao ambiente."
- "Recomendamos correcao como parte do ciclo regular de manutencao, dentro do SLA de 90 dias uteis."
- "Embora de baixo risco individual, a acumulacao de findings similares pode indicar uma fragilidade sistematica."

## Informational

- "Este item e registrado para fins de visibilidade e nao representa uma vulnerabilidade exploravel no contexto atual."
- "O finding informativo documenta uma configuracao que, embora nao ideal, nao apresenta risco direto ao ambiente."
- "Recomendamos considerar a correcao como melhoria de postura, sem prazo obrigatorio definido."
