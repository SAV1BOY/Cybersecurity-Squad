# AppSec Layer — Framework Operacional

> Camada de seguranca de aplicacoes: seguranca desde o design ate o deploy.

## Objetivo

A AppSec Layer integra seguranca no ciclo de desenvolvimento de software (SDLC). Nao e sobre bloquear deploys — e sobre ajudar developers a construir software seguro desde o inicio, com gates automatizados e revisoes focadas em risco real.

## Principios

1. **Shift-left, nao shift-blame** — Seguranca mais cedo, sem culpar developers
2. **Parceria > policia** — Security champion model, nao auditoria punitiva
3. **Automacao primeiro** — SAST/DAST/SCA no CI, nao manual
4. **Risco real > compliance checkbox** — Focar em vulnerabilidades exploraveis
5. **Developer experience importa** — Ferramentas que developers querem usar
6. **Threat model antes de codigo** — Entender ameacas antes de escrever controles

## Componentes do SDLC Seguro

### 1. Requirements & Design
- **Threat modeling** (STRIDE, PASTA) — Antes de escrever codigo
- **Security requirements** — Derivados do threat model
- **Architecture review** — Patterns seguros, trust boundaries claros
- **Security user stories** — "Como atacante, eu tentaria..."

### 2. Implementation
- **Secure coding standards** — Por linguagem (Java, Python, JS, Go, etc.)
- **Security champion** — Developer embedded no time que lidera seguranca
- **IDE plugins** — Feedback em tempo real no editor
- **Pre-commit hooks** — Secrets scanning, linting basico

### 3. Verification
- **SAST** (Static Analysis) — No CI, blocking para criticos
- **SCA** (Software Composition Analysis) — Dependencias vulneraveis
- **DAST** (Dynamic Analysis) — Contra ambiente staging
- **Code review** — Revisao manual focada em: auth, crypto, injection, deserializacao
- **API testing** — AuthZ, BOLA, rate limits, schema validation

### 4. Release
- **Security sign-off** — Gate de seguranca antes de producao
- **SBOM** — Software Bill of Materials gerado e armazenado
- **Container scanning** — Imagens verificadas antes do deploy
- **Secrets check** — Nenhum segredo hardcoded no artefato final

### 5. Operations
- **Vulnerability management** — SLA de correcao por severidade
- **Bug bounty** — Canal externo de descoberta
- **Dependency updates** — Patch cadence definida
- **Runtime protection** — WAF, RASP (onde aplicavel)

## Security Gates por Nivel (OWASP ASVS)

| Gate | Nivel ASVS | Quando Aplicar |
|------|------------|----------------|
| L1 — Oportunistico | ASVS Level 1 | Todas as aplicacoes |
| L2 — Padrao | ASVS Level 2 | Aplicacoes com dados sensiveis |
| L3 — Avancado | ASVS Level 3 | Aplicacoes criticas (financeiro, saude) |

## Vulnerabilidades Prioritarias

Ordem de prioridade baseada em impacto real:

1. **Broken Access Control** — BOLA, IDOR, privilege escalation
2. **Injection** — SQL, OS, LDAP, template injection
3. **Authentication failures** — Weak passwords, session fixation, MFA bypass
4. **Cryptographic failures** — Weak algorithms, improper key management
5. **SSRF** — Server-side request forgery
6. **Insecure deserialization** — Remote code execution via deserialization
7. **Security misconfiguration** — Default creds, unnecessary features, verbose errors

## Agentes Envolvidos

| Agente | Papel na AppSec Layer |
|--------|----------------------|
| Jim Manico | Secure coding, OWASP standards, threat modeling, SDLC gates |
| Fuzzer | API/input fuzzing, edge case discovery |
| Command Generator | SAST/DAST automation scripts |
| Cyber Chief | Gate approvals, risk decisions |

## Outputs

- Threat models documentados
- Code review findings
- SDLC security gates configurados
- Security champion program ativo
- Vulnerability backlog priorizado
- SBOM por aplicacao

## Quality Gates

- `code-review-security-quality.md`
- `manico/manico-ssdlc-gates.md`
- `manico/manico-secure-coding-review.md`
- `appsec/appsec-api-security-gate.md`
