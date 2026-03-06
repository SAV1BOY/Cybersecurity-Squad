# LGPD Impact on Security

Analise do impacto da Lei Geral de Protecao de Dados no cenario de seguranca brasileiro.

## Contexto

A LGPD (Lei 13.709/2018) entrou em vigor em setembro de 2020 no Brasil,
com sancoes aplicaveis a partir de agosto de 2021. Inspirada no GDPR europeu,
estabelece regras para coleta, armazenamento e tratamento de dados pessoais.

## Principios Relevantes para Seguranca (Art. 6)

| Principio | Impacto em Seguranca |
|-----------|---------------------|
| Finalidade | Limitar coleta e armazenamento ao necessario |
| Necessidade | Data minimization reduz superficie de ataque |
| Seguranca | Medidas tecnicas e administrativas obrigatorias |
| Prevencao | Investimento proativo em controles de seguranca |
| Responsabilizacao | Demonstrar conformidade com evidencias |

## Requisitos Tecnicos

### Protecao de Dados Pessoais
- Encryption at rest e in transit para dados pessoais
- Access control granular baseado em necessidade de acesso
- Pseudonymization e anonymization quando aplicavel
- Logging de acesso a dados pessoais

### Incidentes de Seguranca (Art. 48)
- Comunicacao a ANPD em prazo razoavel
- Notificacao ao titular quando risco relevante
- Descricao da natureza dos dados afetados
- Medidas de mitigacao adotadas

### Direitos dos Titulares
- Acesso, correcao e exclusao de dados (impacta arquitetura)
- Portabilidade de dados (requer APIs padronizadas)
- Revogacao de consentimento (controle granular necessario)

## ANPD - Autoridade Nacional de Protecao de Dados

Sancoes previstas:
- Advertencia com indicacao de prazo para medidas corretivas
- Multa simples de ate 2% do faturamento (limitada a R$50M por infracao)
- Publicizacao da infracao
- Bloqueio ou eliminacao dos dados pessoais

## Impacto Pratico no Brasil

- Crescimento do mercado de seguranca da informacao
- Demanda por DPOs e profissionais de privacy
- Investimento em ferramentas de data discovery e classification
- Programas de security awareness incluem protecao de dados
- Contratos com terceiros incluem clausulas de LGPD

## Desafios

- Muitas organizacoes brasileiras ainda em estagio inicial de conformidade
- PMEs com recursos limitados para implementacao completa
- Interpretacoes divergentes sobre requisitos tecnicos especificos
- ANPD em fase de maturacao de fiscalizacao e enforcement
