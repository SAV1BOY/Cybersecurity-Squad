# NIST SSDF — Secure Software Development Framework

## Overview

O NIST Secure Software Development Framework (SP 800-218) define um conjunto de praticas de desenvolvimento seguro de software que visam reduzir vulnerabilidades em aplicacoes antes da entrega. O SSDF nao prescreve ferramentas ou tecnologias especificas, mas estabelece outcomes desejados que podem ser alcancados por diferentes abordagens. Tornou-se requisito de facto para fornecedores de software do governo americano apos a Executive Order 14028, e serve como referencia global para programas de AppSec.

## Core Concepts

### Grupos de Praticas

O SSDF organiza suas praticas em quatro grupos fundamentais:

#### 1. Prepare the Organization (PO)

Praticas que garantem que pessoas, processos e tecnologia estejam prontos para desenvolvimento seguro:

- **PO.1** — Definir requisitos de seguranca para o processo de desenvolvimento de software.
- **PO.2** — Implementar papeis e responsabilidades de seguranca no ciclo de desenvolvimento.
- **PO.3** — Implementar toolchains de suporte que cubram analise estatica, composicao e testes dinamicos.
- **PO.4** — Definir criterios para verificacao de seguranca de software e gate reviews.
- **PO.5** — Criar e manter ambientes de desenvolvimento seguros e isolados.

#### 2. Protect the Software (PS)

Praticas focadas em proteger componentes de software contra adulteracao e acesso nao autorizado:

- **PS.1** — Proteger todo o codigo fonte contra acesso nao autorizado e alteracoes indevidas.
- **PS.2** — Fornecer mecanismo para verificar integridade de releases (signing, checksums, SBOM).
- **PS.3** — Arquivar e proteger cada release de software para facilitar investigacoes futuras.

#### 3. Produce Well-Secured Software (PW)

Praticas que asseguram que o software e desenvolvido com seguranca integrada:

- **PW.1** — Projetar software para satisfazer requisitos de seguranca e mitigar riscos identificados.
- **PW.2** — Revisar design de software para verificar conformidade com requisitos de seguranca.
- **PW.4** — Reutilizar software existente e bem mantido quando possivel em vez de construir do zero.
- **PW.5** — Criar codigo fonte aderente a praticas de codificacao segura e padroes do projeto.
- **PW.6** — Configurar build processes para melhorar a seguranca dos executaveis gerados.
- **PW.7** — Revisar e testar o codigo para identificar vulnerabilidades e verificar conformidade.
- **PW.8** — Configurar o software para ter configuracoes default seguras.
- **PW.9** — Testar o software executavel para identificar vulnerabilidades e verificar conformidade.

#### 4. Respond to Vulnerabilities (RV)

Praticas para identificar e responder a vulnerabilidades apos o release:

- **RV.1** — Identificar e confirmar vulnerabilidades de forma continua em cada release.
- **RV.2** — Avaliar, priorizar e remediar vulnerabilidades identificadas.
- **RV.3** — Analisar vulnerabilidades para identificar root causes e prevenir recorrencias.

## Practical Application

### Implementacao Gradual

1. Realizar gap assessment mapeando praticas atuais contra os outcomes do SSDF.
2. Priorizar praticas do grupo PO como fundacao do programa.
3. Integrar ferramentas de SAST, SCA e DAST no CI/CD pipeline (PW.7, PW.9).
4. Implementar code signing e SBOM generation para cada release (PS.2).
5. Estabelecer processo de vulnerability disclosure e response (RV.1, RV.2).
6. Medir cobertura de praticas trimestralmente e ajustar o roadmap.

### Ferramentas por Pratica

| Pratica | Categoria de Ferramenta | Exemplos |
|---------|------------------------|----------|
| PW.5 | SAST (Static Analysis) | Semgrep, SonarQube, CodeQL |
| PW.4 | SCA (Software Composition) | Snyk, Dependabot, Trivy |
| PW.9 | DAST (Dynamic Analysis) | OWASP ZAP, Burp Suite, Nuclei |
| PS.2 | Supply Chain Security | Sigstore, in-toto, SLSA |
| RV.1 | Vulnerability Management | DefectDojo, Nucleus |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer implementa diretamente as praticas PW do SSDF no pipeline de desenvolvimento.
- O security-champion-program capacita desenvolvedores nas praticas PO e PW para shift-left efetivo.
- O finding-structure-standard segue o fluxo RV.2 para priorizacao e rastreamento de vulnerabilidades.
- SBOMs gerados conforme PS.2 alimentam o processo de SCA e vulnerability management do squad.
- O retest-method valida a eficacia das remediacoes conforme pratica RV.3 de root cause analysis.
- Metricas de adocao do SSDF sao exibidas no security-kpi-dashboard por equipe e produto.
- O owasp-samm complementa o SSDF oferecendo modelo de maturidade para medir evolucao das praticas.
