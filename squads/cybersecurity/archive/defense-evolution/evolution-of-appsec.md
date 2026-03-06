# Evolution of AppSec

Historia e evolucao da seguranca de aplicacoes.

## Timeline Evolutiva

### Era 1: Perimeter Defense (2000-2006)
- Seguranca focada em firewalls e WAFs
- Aplicacoes consideradas "protegidas" pelo perimetro
- Pentests anuais como unica avaliacao
- OWASP Top 10 primeira versao (2003)
- Desenvolvimento sem consideracao de seguranca

### Era 2: SDL e Testing (2007-2013)
- Microsoft SDL (Security Development Lifecycle) como referencia
- SAST e DAST como ferramentas especializadas
- Pentests manuais como pratica regular
- Code review focado em seguranca
- Seguranca como gate no final do ciclo (waterfall)

### Era 3: DevSecOps e Shift-Left (2014-2019)
- Integracao de testes de seguranca no CI/CD pipeline
- SAST, DAST e SCA automatizados em cada build
- Security champions em equipes de desenvolvimento
- Threat modeling como pratica de design
- Infrastructure as Code (IaC) scanning

### Era 4: Supply Chain e API Security (2020-2023)
- Foco em dependencias e supply chain (SCA maturo)
- SBOM (Software Bill of Materials) como requisito
- API security como disciplina especifica (OWASP API Top 10)
- Container e Kubernetes security
- ASPM (Application Security Posture Management)

### Era 5: AI-Assisted AppSec (2024-presente)
- AI-powered code review e vulnerability detection
- Automated fix suggestions com LLMs
- AI-generated test cases para security testing
- Runtime protection inteligente (RASP)
- Secure-by-default frameworks e guardrails

## Evolucao de Ferramentas

| Era | Ferramentas Tipicas |
|-----|-------------------|
| Perimeter | WAF, firewalls |
| SDL | Fortify, WebInspect, Burp Suite |
| DevSecOps | SonarQube, Snyk, Checkmarx, OWASP ZAP |
| Supply Chain | Dependabot, Trivy, Grype, Syft |
| AI-Assisted | GitHub Copilot Security, Semgrep AI |

## OWASP Top 10 - Evolucao

Categorias como Injection caíram em ranking conforme frameworks modernos
mitigam por default. Novas categorias como Insecure Design e SSRF
refletem mudancas no threat landscape.

## Tendencia

AppSec evolui de "encontrar bugs" para "prevenir classes de bugs".
Guardrails, secure defaults e paved roads sao mais eficazes que
scanning retroativo. Developer experience e chave para adocao.
