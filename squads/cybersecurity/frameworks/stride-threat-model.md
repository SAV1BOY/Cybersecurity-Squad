# STRIDE — Threat Modeling Methodology

## Overview

O STRIDE e uma metodologia de modelagem de ameacas desenvolvida pela Microsoft em 1999 que categoriza ameacas de seguranca em seis tipos distintos. Cada categoria corresponde a uma violacao de uma propriedade de seguranca desejada. O modelo e amplamente utilizado por sua simplicidade e eficacia em workshops de threat modeling, sendo particularmente adequado para equipes de desenvolvimento que precisam identificar ameacas de forma sistematica durante o design de sistemas.

## Core Concepts

### As Seis Categorias de Ameacas

#### Spoofing (Falsificacao de Identidade)

Viola a propriedade de **Authentication**. O adversario assume a identidade de outra entidade (usuario, servico ou sistema) para obter acesso nao autorizado.

- Exemplos: credential theft, token forgery, IP spoofing, DNS spoofing.
- Contramedidas: MFA, mutual authentication, certificate pinning, strong password policies.

#### Tampering (Adulteracao)

Viola a propriedade de **Integrity**. O adversario modifica dados em transito ou em repouso sem autorizacao.

- Exemplos: man-in-the-middle, SQL injection, parameter tampering, binary patching.
- Contramedidas: input validation, digital signatures, HMAC, integrity monitoring.

#### Repudiation (Repudio)

Viola a propriedade de **Non-repudiation**. O adversario nega ter realizado uma acao sem que a organizacao consiga provar o contrario.

- Exemplos: exclusao de logs, ausencia de audit trail, acoes anonimas em sistemas criticos.
- Contramedidas: audit logging, digital signatures, timestamps confiaveis, log forwarding.

#### Information Disclosure (Divulgacao de Informacao)

Viola a propriedade de **Confidentiality**. Dados sensiveis sao expostos a entidades nao autorizadas.

- Exemplos: data breach, directory listing, verbose error messages, side-channel attacks.
- Contramedidas: encryption at rest/in transit, access controls, data classification, DLP.

#### Denial of Service (Negacao de Servico)

Viola a propriedade de **Availability**. O adversario torna um servico ou recurso indisponivel para usuarios legitimos.

- Exemplos: DDoS, resource exhaustion, algorithmic complexity attacks, lock-out attacks.
- Contramedidas: rate limiting, auto-scaling, CDN, circuit breakers, input validation.

#### Elevation of Privilege (Escalacao de Privilegio)

Viola a propriedade de **Authorization**. O adversario obtem permissoes superiores as concedidas originalmente.

- Exemplos: privilege escalation, IDOR, JWT manipulation, role bypass, container escape.
- Contramedidas: least privilege, RBAC/ABAC, input validation, sandboxing, capability drops.

### STRIDE-per-Element

Variacao que aplica categorias STRIDE especificas a cada tipo de elemento no Data Flow Diagram:

| Elemento DFD | Ameacas Aplicaveis |
|-------------|-------------------|
| External Entity | Spoofing, Repudiation |
| Data Flow | Tampering, Information Disclosure, Denial of Service |
| Data Store | Tampering, Information Disclosure, Repudiation, Denial of Service |
| Process | Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege |
| Trust Boundary | Todas as categorias na fronteira |

## Practical Application

### Processo de Threat Modeling com STRIDE

1. **Decomposicao do Sistema** — Criar Data Flow Diagram (DFD) identificando processos, data stores, data flows, external entities e trust boundaries.
2. **Identificacao de Ameacas** — Para cada elemento do DFD, aplicar as categorias STRIDE relevantes e listar ameacas concretas.
3. **Avaliacao de Risco** — Classificar cada ameaca por probabilidade e impacto utilizando DREAD ou outro modelo de scoring.
4. **Definicao de Mitigacoes** — Para cada ameaca relevante, definir controles que reduzam o risco a nivel aceitavel.
5. **Validacao** — Verificar que mitigacoes foram implementadas e testar eficacia com security testing.

### Template de Documentacao de Ameaca

```
Ameaca: [Nome descritivo]
Categoria STRIDE: [S/T/R/I/D/E]
Elemento DFD: [Processo/Data Store/Data Flow afetado]
Descricao: [Como o ataque ocorre]
Impacto: [Consequencia para o negocio]
Probabilidade: [Alta/Media/Baixa]
Mitigacao: [Controle proposto]
Status: [Identificada/Mitigada/Aceita]
```

### Workshop de Threat Modeling

- Duracao recomendada: 60 a 90 minutos por componente.
- Participantes: arquiteto, desenvolvedor senior, security champion, product owner.
- Preparacao: DFD atualizado do componente a ser analisado.
- Output: lista priorizada de ameacas com mitigacoes no backlog.
- Frequencia: a cada nova feature de alto risco ou mudanca arquitetural significativa.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer conduz sessoes de STRIDE threat modeling como parte do secure design review.
- O security-champion-program treina champions para facilitar workshops de STRIDE em suas equipes.
- O finding-structure-standard categoriza findings com referencia a categoria STRIDE correspondente.
- O pasta-threat-model oferece metodologia alternativa mais abrangente para cenarios complexos.
- O linddun-privacy-threat-model complementa o STRIDE com foco especifico em ameacas de privacidade.
- Ameacas identificadas via STRIDE sao registradas no risk-scoring-model para priorizacao.
- O offense-layer valida mitigacoes de ameacas STRIDE durante engagements de pentest.
- Templates de DFD e documentacao de ameacas sao mantidos no repositorio do squad.
