# Best Disclosure Practices

Exemplos de boas praticas em divulgacao de vulnerabilidades e incidentes.

## Responsible Disclosure - Exemplos Positivos

### Google Project Zero
- 90 dias de disclosure deadline com extensao de 14 dias para patches complexos
- Transparencia total: publica detalhes apos deadline independente de fix
- Motivou toda a industria a melhorar tempos de patching
- Documentacao detalhada de cada vulnerabilidade encontrada

### HackerOne / Bugcrowd Programs
- Plataformas que profissionalizaram bug bounty
- Safe harbor legal para pesquisadores de boa-fe
- Coordenacao entre pesquisador, vendor e plataforma
- Exemplos: programas de Google, Microsoft, Apple

## Breach Disclosure - Exemplos Positivos

### Cloudflare (Multiple Incidents)
- Blog posts detalhados publicados em horas/dias
- Descricao tecnica completa do incidente
- Timeline transparente incluindo erros cometidos
- Acoes concretas tomadas e planejadas

### Twilio (2022)
- Notificacao proativa a clientes afetados
- Atualizacoes frequentes durante investigacao
- Detalhes tecnicos compartilhados para protecao da comunidade
- Post-mortem abrangente publicado

## Anti-Patterns em Disclosure

| Pratica Ruim | Exemplo | Consequencia |
|-------------|---------|-------------|
| Minimizar impacto | Equifax: "app vulnerability" | Perda de confianca |
| Demora na divulgacao | Uber (2016): escondeu breach por 1 ano | Multas e processos |
| Linguagem vaga | "Unauthorized access to systems" | Especulacao publica |
| Culpar pesquisador | Processar quem reportou a vuln | Comunidade hostil |

## Framework para Boa Disclosure

1. **Notificacao rapida**: Assim que fatos basicos sao confirmados
2. **Transparencia**: Compartilhar o que se sabe e o que ainda esta sendo investigado
3. **Atualizacoes regulares**: Comunicar progresso mesmo sem novidades
4. **Detalhes tecnicos**: Publicar quando nao comprometer investigacao
5. **Acoes concretas**: O que foi feito e o que sera feito
6. **Responsabilidade**: Assumir sem desviar culpa

## Regulamentacoes de Disclosure

- **GDPR**: 72 horas para notificar autoridade de protecao de dados
- **LGPD**: Prazo razoavel para notificar ANPD e titulares
- **SEC**: 4 dias uteis para disclosure material de cyber incidents
