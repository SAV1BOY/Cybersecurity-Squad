# Task: SDLC Security Gates Setup

## Objetivo
Implementar security gates no ciclo de desenvolvimento de software (SDLC), garantindo que requisitos de seguranca sejam verificados em cada fase do pipeline.

## Agents
- **jim-manico** (lead) — Define security gates e criterios
- **cyber-chief** (support) — Alinha com governanca e compliance

## Inputs
- Pipeline de CI/CD existente
- OWASP SAMM e NIST SSDF como referencia
- Requisitos de compliance aplicaveis
- Threat models existentes

## Steps
1. Mapear o pipeline de CI/CD atual e identificar pontos de integracao
2. Definir security gates por fase: design, code, build, test, deploy
3. Configurar SAST no pipeline de build
4. Configurar DAST em ambiente de staging
5. Implementar SCA (Software Composition Analysis) para dependencias
6. Definir criterios de bloqueio por severidade (ex: block on Critical)
7. Criar workflow de excecao para bypass autorizado
8. Documentar security gates em politica de Secure SDLC
9. Treinar equipe de desenvolvimento nos novos gates
10. Registrar decisoes no `decisions-log`

## Output
- Security gates implementados no pipeline de CI/CD
- Politica de Secure SDLC documentada
- Criterios de bloqueio e excecao definidos
- Material de treinamento para desenvolvedores

## Quality Gates
- [ ] SAST integrado e funcional no pipeline
- [ ] DAST configurado para ambiente de staging
- [ ] SCA implementado para dependency scanning
- [ ] Criterios de bloqueio definidos por severidade
- [ ] Workflow de excecao documentado e controlado
- [ ] Desenvolvedores treinados nos novos gates
- [ ] Checklist `manico-ssdlc-gates` 100% atendido

## Routing & Escalation
- **frameworks**: owasp-samm, nist-ssdf, appsec-layer
- **checklists**: manico/manico-ssdlc-gates
- **templates**: policies/secure-sdlc-policy
- **registry**: data/registries/decisions-log
- **receives_from**: cyber-chief directive
- **delivers_to**: dev squad integration
