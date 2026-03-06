# Manico - SSDLC Gates

Checklist de quality gates para Secure Software Development Lifecycle.

## Requirements Phase Gate
- [ ] Security requirements derivados de threat model
- [ ] Abuse cases documentados junto com use cases
- [ ] Compliance requirements identificados (LGPD, PCI, HIPAA)
- [ ] Data classification realizada para dados manipulados
- [ ] Security acceptance criteria definidos por story/feature
- [ ] Risk assessment realizado para features de alto impacto

## Design Phase Gate
- [ ] Threat model criado ou atualizado para a feature
- [ ] Security design patterns selecionados e documentados
- [ ] Authentication e authorization design revisados
- [ ] Cryptographic choices revisadas por especialista
- [ ] Third-party integration security avaliada
- [ ] Attack surface delta documentado para nova feature
- [ ] Design review de seguranca aprovado

## Implementation Phase Gate
- [ ] Secure coding guidelines seguidas pela equipe
- [ ] Pre-commit hooks para secret scanning habilitados
- [ ] SAST scan executado com zero critical/high findings
- [ ] SCA scan executado sem vulnerabilidades criticas
- [ ] Code review de seguranca realizado por peer
- [ ] Unit tests para security controls implementados
- [ ] Input validation implementada conforme design

## Testing Phase Gate
- [ ] DAST scan executado em ambiente de staging
- [ ] IAST integrado em test suite (se disponivel)
- [ ] Security test cases executados (baseados em abuse cases)
- [ ] Penetration testing realizado (se feature de alto risco)
- [ ] Fuzz testing executado em inputs criticos
- [ ] Authentication e authorization tests automatizados
- [ ] Security regression tests passando

## Release Phase Gate
- [ ] Security sign-off obtido do security champion/team
- [ ] Todas as vulnerabilidades criticas e altas remediadas
- [ ] SBOM gerado e armazenado para a release
- [ ] Container image scanning executado (se aplicavel)
- [ ] Infrastructure as Code scanning executado
- [ ] Security monitoring configurado para nova feature
- [ ] Incident response plan atualizado (se necessario)

## Post-Release
- [ ] Security monitoring ativo para anomalias
- [ ] Bug bounty scope atualizado (se aplicavel)
- [ ] Vulnerability disclosure process funcional
- [ ] Feedback loop de seguranca para proximo sprint
- [ ] Metricas de seguranca do SDLC coletadas e analisadas
- [ ] Security training needs atualizados para o time
