# Application Security Tooling

## Visao Geral
Ferramentas utilizadas pelo squad para atividades de Application Security,
incluindo analise estatica, dinamica, composicao de software e testes manuais.

## Static Application Security Testing (SAST)

### Semgrep
- **Tipo**: SAST open-source baseado em patterns
- **Linguagens**: Python, JavaScript, Go, Java, Ruby, C, e mais
- **Uso**: code review automatizado, custom rules
- **Diferencial**: regras customizaveis em YAML, facil de adotar
- **Integracao**: CI/CD pipelines, pre-commit hooks

### SonarQube
- **Tipo**: plataforma de quality e security analysis
- **Uso**: analise continua de qualidade e seguranca de codigo
- **Metricas**: security hotspots, code smells, coverage
- **Integracao**: Jenkins, GitHub Actions, GitLab CI

### CodeQL
- **Tipo**: semantic code analysis engine (GitHub)
- **Uso**: queries semanticas para encontrar vulnerabilidades
- **Diferencial**: analise baseada em data flow e taint tracking
- **Integracao**: GitHub Advanced Security

## Dynamic Application Security Testing (DAST)

### OWASP ZAP
- **Tipo**: DAST open-source
- **Uso**: scanning automatizado e testes manuais de web apps
- **Modos**: passive scan, active scan, fuzzing
- **Integracao**: CI/CD via API ou CLI

### Nuclei
- **Tipo**: vulnerability scanner baseado em templates
- **Uso**: scanning rapido com templates customizaveis
- **Templates**: comunidade mantém milhares de templates
- **Diferencial**: velocidade e facilidade de criar checks custom

## Software Composition Analysis (SCA)

### Dependabot / Renovate
- **Tipo**: dependency update automation
- **Uso**: manter dependencias atualizadas automaticamente

### Snyk
- **Tipo**: SCA comercial com SAST e container scanning
- **Uso**: analise de vulnerabilidades em dependencias
- **Integracao**: IDE, CLI, CI/CD, container registries

### OWASP Dependency-Check
- **Tipo**: SCA open-source
- **Uso**: identificar componentes com CVEs conhecidas
- **Formatos**: Java, .NET, Python, Node.js

## Secret Detection

### TruffleHog
- **Tipo**: secret scanner
- **Uso**: detectar secrets em repositorios git
- **Cobertura**: API keys, passwords, tokens, certificates

### GitLeaks
- **Tipo**: secret detection para git repos
- **Uso**: pre-commit hooks e CI/CD scanning

## Pipeline de AppSec do Squad
1. Pre-commit: secret scanning (GitLeaks)
2. PR/MR: SAST (Semgrep), SCA (Dependency-Check)
3. Build: DAST (ZAP em modo headless)
4. Release: full scan com Nuclei + ZAP
5. Production: continuous monitoring

## Notas do Squad
Balancear automacao com revisao manual. Ferramentas automatizadas encontram
fruit de baixo nivel; vulnerabilidades logicas requerem analise humana.
