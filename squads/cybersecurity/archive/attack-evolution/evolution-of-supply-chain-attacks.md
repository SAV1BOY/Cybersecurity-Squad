# Evolution of Supply Chain Attacks

Historia e evolucao dos ataques a supply chain de software e hardware.

## Timeline Evolutiva

### Era 1: Primordios (2000-2012)
- Trojanizacao de software pirata e cracks
- Compromisso de sites de download legítimos
- RSA SecurID breach (2011): tokens comprometidos afetam clientes
- Impacto limitado e pouco sistematico

### Era 2: Ataques Direcionados (2013-2017)
- **Target (2013)**: Via vendor de HVAC
- **CCleaner (2017)**: 2.3M downloads de versao comprometida
- **NotPetya (2017)**: Via atualizacao de software fiscal ucraniano (MeDoc)
- Atacantes percebem que vendors sao multiplicadores de acesso

### Era 3: Build System Compromise (2018-2021)
- **SolarWinds (2020)**: Comprometimento do build pipeline
- **Codecov (2021)**: Script de CI comprometido exfiltrava secrets
- **Kaseya (2021)**: Exploit em plataforma de RMM afeta 1500+ empresas
- Foco em comprometer o processo de build, nao o codigo fonte

### Era 4: Open Source e Dependency Attacks (2021-presente)
- **Log4Shell (2021)**: Vulnerabilidade em biblioteca ubiqua
- **ua-parser-js, colors.js (2022)**: Maintainer compromise/protest
- **xz-utils (2024)**: Infiltracao de longo prazo em projeto open-source
- Typosquatting em registros de pacotes (npm, PyPI)
- Dependency confusion attacks

## Vetores de Ataque

| Vetor | Exemplo | Impacto Tipico |
|-------|---------|---------------|
| Vendor compromise | SolarWinds | Milhares de organizacoes |
| Build pipeline | Codecov | Secrets de clientes |
| Open-source dependency | Log4Shell | Milhoes de apps |
| Typosquatting | ua-parser-js | Desenvolvedores individuais |
| Hardware supply chain | SuperMicro (alegado) | Infraestrutura fisica |

## Defesas

- Software Bill of Materials (SBOM) para visibilidade
- Software Composition Analysis (SCA) continuo
- SLSA framework para integridade de build
- Dependency pinning e lock files
- Vendor risk assessment com auditorias regulares
- Zero trust para software de terceiros
- Monitoring de dependencias para malicious updates

## Tendencia

Supply chain attacks continuam crescendo em sofisticacao. A comunidade
open-source e especialmente vulneravel por depender de voluntarios
com recursos limitados mantendo infraestrutura critica global.
