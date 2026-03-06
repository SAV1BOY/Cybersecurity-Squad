# AppSec - Supply Chain

Checklist para seguranca da cadeia de suprimentos de software.

## Software Bill of Materials (SBOM)
- [ ] SBOM gerado para cada aplicacao (CycloneDX ou SPDX)
- [ ] SBOM inclui dependencias diretas e transitivas
- [ ] SBOM atualizado a cada build
- [ ] SBOM armazenado e acessivel para consulta
- [ ] SBOM inclui versoes exatas de cada componente
- [ ] SBOM inclui licencas de cada componente
- [ ] SBOM comparado entre releases para detectar changes

## Vulnerability Management
- [ ] SCA (Software Composition Analysis) integrado ao CI/CD
- [ ] Known vulnerabilities em dependencies identificadas
- [ ] Critical/High CVEs bloqueiam o pipeline (break the build)
- [ ] Vulnerability database atualizada automaticamente
- [ ] Remediation SLA definido por severity
- [ ] Dependency update automation configurada (Dependabot, Renovate)
- [ ] Monitoring continuo de novas CVEs em dependencies em producao

## Package Integrity
- [ ] Package lock files commitados e respeitados
- [ ] Package checksums verificados durante install
- [ ] Package signing verificado (se disponivel)
- [ ] Private registry utilizado para packages internos
- [ ] Typosquatting protection implementada
- [ ] Namespace confusion/dependency confusion prevenida
- [ ] Mirroring de packages criticos configurado

## Build Pipeline Security
- [ ] Build environment isolado e hardened
- [ ] Build reproducibility verificada
- [ ] Build artifacts assinados digitalmente
- [ ] SLSA framework adotado (level definido)
- [ ] Build logs retidos para auditoria
- [ ] Build dependencies pinadas por hash
- [ ] Container base images de trusted sources apenas

## Third-Party Code Review
- [ ] Criteria para adocao de novas dependencies definido
- [ ] Security assessment de dependencies criticas realizado
- [ ] Maintenance status de dependencies verificado (abandoned?)
- [ ] Community health de open-source projects avaliado
- [ ] Forking strategy para dependencies abandonadas definida

## Governance e Compliance
- [ ] License compliance verificada (compatibilidade de licencas)
- [ ] Approved dependency list mantida (se aplicavel)
- [ ] Prohibited dependencies listadas e enforced
- [ ] Supply chain risk register mantido
- [ ] Supply chain incident response plan definido
- [ ] Regular audit de supply chain security realizado
- [ ] Metricas reportadas (CVE count, mean time to patch deps)
