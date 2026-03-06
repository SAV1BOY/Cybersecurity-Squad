# Okta / Lapsus$ Breach Analysis (2022)

Analise do comprometimento da Okta pelo grupo Lapsus$ via contractor terceirizado.

## O Que Aconteceu

O grupo Lapsus$ comprometeu a conta de um engenheiro de suporte da Sitel
(contractor da Okta), obtendo acesso ao sistema de suporte interno da Okta.
Atraves dessa posicao, o grupo potencialmente acessou dados de ate 366
clientes da Okta (aproximadamente 2.5% da base).

## Timeline

| Data | Evento |
|------|--------|
| Jan 16, 2022 | Lapsus$ compromete laptop de engenheiro Sitel |
| Jan 20, 2022 | Okta Security detecta tentativa de MFA reset |
| Jan 21, 2022 | Okta investiga e reseta conta do engenheiro |
| Jan-Mar 2022 | Okta aguarda relatorio forense da Sitel |
| Mar 22, 2022 | Lapsus$ publica screenshots do acesso interno |
| Mar 22, 2022 | Okta confirma incidente publicamente |

## Root Cause

1. **Third-party access**: Contractor com acesso privilegiado a sistemas internos
2. **Resposta lenta**: 2 meses entre deteccao e comunicacao publica
3. **Subestimacao do impacto**: Avaliacao inicial minimizou o escopo
4. **Falta de visibilidade**: Controle limitado sobre endpoints de terceiros
5. **Comunicacao inadequada**: Resposta publica inicial foi considerada dismissiva

## Impacto

- Ate 366 clientes da Okta potencialmente afetados
- Dano reputacional significativo para um provider de identidade
- Queda de 9% nas acoes da Okta apos divulgacao
- Questionamentos sobre seguranca de identity providers

## Licoes Aprendidas

- Identity providers sao alvos de altissimo valor (supply chain)
- Third-party access deve ter controles equivalentes a funcionarios
- Comunicacao proativa e transparente e essencial
- Nao subestimar incidentes - overreact e melhor que underreact
- Session recording e monitoring para acessos privilegiados de terceiros
- Zero trust deve se aplicar tambem a contractors e fornecedores

## Como Detectariamos/Preveniríamos

- Privileged Access Management (PAM) para todo acesso de terceiros
- Session recording e behavioral monitoring
- Zero-trust endpoint compliance para dispositivos de contractors
- Comunicacao imediata aos clientes ao confirmar comprometimento
- Reducao do escopo de acesso de suporte ao minimo necessario
- Alertas para acoes administrativas anomalas em horarios incomuns
