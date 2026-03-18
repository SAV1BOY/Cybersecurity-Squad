# Identity Layer — Framework Operacional

> Camada de identidade: IdP, AD, federation, MFA, privilegios e zero trust.

## Objetivo

A Identity Layer trata identidade como o perimetro principal de seguranca. Em ambientes modernos (cloud, hybrid, remote work), identidade e o controle que define quem pode acessar o que. Comprometer identidade = comprometer tudo.

## Principios

1. **Identity is the new firewall** — Controle de acesso baseado em identidade, nao em rede
2. **Least privilege always** — Minimo necessario, pelo menor tempo necessario
3. **MFA everywhere** — Sem excecoes para acessos interativos
4. **Zero standing privilege** — JIT/JEA para operacoes privilegiadas
5. **Federation over passwords** — SSO e federacao reduzem superficie
6. **Monitor identity events** — Login anomalo e o sinal mais valioso

## Componentes

### 1. Identity Providers (IdP)
- Configuracao segura do IdP (Azure AD, Okta, Google Workspace)
- Password policies: comprimento minimo 14 chars, sem rotacao forcada, breach check
- MFA: FIDO2/WebAuthn preferido, TOTP aceitavel, SMS como ultimo recurso
- Conditional access: contexto (device, location, risk) determina requisitos

### 2. Active Directory
- Tiering model: Tier 0 (domain controllers), Tier 1 (servers), Tier 2 (workstations)
- Privileged access: PAW, bastion hosts, AdminSDHolder monitoring
- Delegacoes: Audit de delegacoes nao-padrao, constrained delegation
- Trusts: Audit de forest/domain trusts, SID filtering
- Kerberos: Monitorar Kerberoasting, ASREP roasting, Golden/Silver tickets

### 3. Cloud IAM
- Roles: Custom roles com menor privilegio, audit regular
- Service accounts: Keys rotacionadas, sem permissoes de usuario
- Cross-account: Trust policies com conditions explicitas
- Federation: SAML/OIDC para acesso humano, roles para acesso programatico

### 4. Privileged Access Management (PAM)
- JIT (Just-In-Time): Acesso privilegiado por tempo limitado
- JEA (Just Enough Administration): Apenas os comandos necessarios
- Session recording: Gravacao de sessoes privilegiadas
- Approval workflow: Aprovacao para operacoes de alto risco

### 5. Service Identity
- Machine-to-machine: mTLS, service mesh identity
- API keys: Rotacao automatica, scoped por servico
- Secrets management: Vault centralizado, zero hardcoded secrets
- Workload identity: Cloud-native identity (IRSA, Workload Identity)

## Attack Vectors de Identidade

| Vetor | Deteccao | Prevencao |
|-------|----------|-----------|
| Password spraying | Lockout anomaly, failed auth spike | MFA, smart lockout, breach passwords block |
| Credential stuffing | Multiple accounts, single IP | MFA, rate limiting, breach detection |
| Kerberoasting | SPN requests anomalos | Managed service accounts, AES encryption |
| ASREP roasting | Pre-auth disabled accounts | Enforce pre-authentication |
| Golden ticket | Anomalous TGT lifetime | KRBTGT rotation, PAC validation |
| Pass-the-Hash | Lateral movement patterns | Credential Guard, network segmentation |
| OAuth token theft | Unusual app consent | App consent policies, conditional access |

## Agentes Envolvidos

| Agente | Papel |
|--------|-------|
| Omar Santos | IAM hardening, PAM setup, baselines |
| Cartographer | Identity mapping, privilege paths |
| Peter Kim | Identity attack testing (autorizado) |
| Rogue | Adversary simulation contra identidade |
| Chris Sanders | Identity event analysis, anomaly detection |

## Outputs

- Identity architecture assessment
- Privilege escalation paths mapped
- IAM policy recommendations
- PAM implementation plan
- Identity monitoring rules

## Quality Gates

- `identity-and-ad-assessment-quality.md`
- `cloud/cloud-iam-least-privilege.md`

## Used By

### Tasks (config.yaml routing)
- identity-and-privilege-mapping

### Agents
- cartographer
- omar-santos

### Related Checklists
- identity-and-ad-assessment-quality
- cloud/cloud-iam-least-privilege

### Cross-References
- Config routing: `config.yaml`
- Quality gate system: `docs/quality-gate-system.md`
