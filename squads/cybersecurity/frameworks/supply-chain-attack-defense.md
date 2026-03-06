# Supply Chain Attack & Defense

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para avaliacao de riscos na cadeia de suprimentos de software. Cobre
analise de dependencias, ataques de confusion, seguranca de CI/CD pipelines,
code signing e SBOM. Foco em prevencao e deteccao de comprometimento supply chain.

## Requisitos de Autorizacao
- Acesso autorizado a repositorios de codigo e pipelines de CI/CD
- Permissao para analise de dependencias e configuracoes de build
- Coordenacao com equipes de desenvolvimento e DevOps
- Ambiente de teste isolado para simulacao de ataques supply chain
- Acordo de confidencialidade para informacoes de infraestrutura

## Etapas da Metodologia

### 1. SBOM (Software Bill of Materials) Analysis
- Geracao de SBOM completo para todas as aplicacoes criticas
- Identificacao de dependencias diretas e transitivas
- Correlacao com vulnerability databases (NVD, OSV, GitHub Advisory)
- Verificacao de licencas e compliance de componentes open source
- Mapeamento de dependencias abandonadas ou sem manutencao

### 2. Dependency Confusion Testing
- Identificacao de pacotes internos/privados e seus namespaces
- Verificacao de protecao contra dependency confusion attacks
- Teste de configuracao de registries privados (scoped packages)
- Avaliacao de namespace reservation em registries publicos
- Verificacao de priority resolution entre registries interno e externo

### 3. Typosquatting Assessment
- Analise de dependencias para identificar potenciais typosquats
- Verificacao de pacotes com nomes similares a dependencias legitimas
- Avaliacao de lockfile integrity (package-lock.json, yarn.lock, Pipfile.lock)
- Teste de alertas para novas dependencias adicionadas sem revisao

### 4. CI/CD Pipeline Security
- Auditoria de permissoes em runners e build agents
- Verificacao de secrets exposure em logs de build
- Analise de third-party GitHub Actions e plugins utilizados
- Teste de poisoned pipeline execution via PR manipulation
- Avaliacao de branch protection rules e code review requirements
- Verificacao de artifact integrity entre stages do pipeline

### 5. Code Signing e Verification
- Avaliacao de commit signing (GPG/SSH) enforcement
- Verificacao de artifact signing em container images e binarios
- Analise de certificate management e key rotation practices
- Teste de verificacao de signatures em deployment pipeline
- Avaliacao de Sigstore/cosign adoption para supply chain attestation

### 6. Build Reproducibility e Integrity
- Teste de reproducible builds para validacao de integridade
- Verificacao de build environment isolation e hermeticidade
- Analise de provenance attestation (SLSA framework compliance)
- Avaliacao de proteção contra build-time injection attacks

## Ferramentas de Referencia
- Syft, Grype (SBOM e vulnerability scanning), Trivy, Snyk
- Scorecard (OpenSSF), Dependabot, Renovate, Socket.dev
- cosign/Sigstore, in-toto, SLSA verifier

## Contrapartida de Deteccao (Blue Team)
- Monitoramento automatico de novas dependencias em pull requests
- Alertas para dependency version changes inesperadas
- Scanning continuo de SBOM contra vulnerability feeds atualizados
- Auditoria de CI/CD pipeline modifications e permission changes
- Verificacao periodica de integridade de lockfiles e checksums
- Deteccao de data exfiltration durante build process

## Integracao com Outros Frameworks
- Correlaciona com: container-security-methodology.md (image supply chain)
- Correlaciona com: api-security-testing-methodology.md (API dependencies)
- Alimenta: programa de DevSecOps e secure development lifecycle
- Reporta para: risk register e compliance framework (SLSA, SSDF)
