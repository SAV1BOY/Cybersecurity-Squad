# Evolution of Identity Attacks

Historia e evolucao dos ataques direcionados a identidade e autenticacao.

## Timeline Evolutiva

### Era 1: Password Attacks (2000-2010)
- Brute force e dictionary attacks contra login pages
- Password spraying em ambientes corporativos
- Keyloggers para captura de credenciais
- Rainbow tables para cracking de hashes
- Defesa: password complexity policies

### Era 2: Credential Stuffing (2011-2016)
- Mega-breaches (LinkedIn, Adobe, Yahoo) geram bilhoes de credenciais
- Reutilizacao de senhas permite acesso automatizado em massa
- Ferramentas como Sentry MBA automatizam credential stuffing
- Dark web marketplaces vendem credenciais em bulk
- Defesa: MFA, breach credential monitoring

### Era 3: MFA Bypass (2017-2021)
- SIM swapping para interceptar SMS OTP
- Real-time phishing proxies (Evilginx, Modlishka)
- MFA fatigue/prompt bombing
- Social engineering de help desk para MFA reset
- Defesa: phishing-resistant MFA (FIDO2/WebAuthn)

### Era 4: Identity Provider Targeting (2022-2024)
- **Okta/Lapsus$ (2022)**: Comprometimento via contractor
- **Microsoft Storm-0558 (2023)**: Forged authentication tokens
- Token theft e session hijacking pos-autenticacao
- OAuth consent phishing (illicit consent grant)
- Defesa: token binding, continuous access evaluation

### Era 5: AI-Enhanced Identity Attacks (2024-presente)
- Deepfake voice para bypassa verificacao de voz
- AI-generated pretexting para social engineering
- Automated reconnaissance para personalizacao
- Attack path analysis automatizada para privilege escalation
- Defesa: behavioral biometrics, continuous verification

## Tipos de Ataque Atuais

| Tecnica | Dificuldade | Impacto | Prevalencia |
|---------|-------------|---------|-------------|
| Credential Stuffing | Baixa | Medio | Muito alta |
| Phishing (AitM) | Media | Alto | Alta |
| MFA Fatigue | Baixa | Alto | Media |
| Token Theft | Media | Critico | Crescente |
| SIM Swapping | Media | Alto | Media |
| Deepfake Social Engineering | Alta | Critico | Emergente |

## Defesas Modernas

- Passwordless authentication (FIDO2, passkeys)
- Continuous Access Evaluation Protocol (CAEP)
- Identity Threat Detection and Response (ITDR)
- Conditional access policies baseadas em risco
- Session management robusto com token binding
- Behavioral analytics para deteccao de account takeover

## Tendencia

Identidade e o novo perimetro. Com adocao de cloud e trabalho remoto,
comprometer uma identidade frequentemente equivale a comprometer a organizacao.
