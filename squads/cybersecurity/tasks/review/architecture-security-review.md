# Task: Architecture Security Review

## Objetivo
Revisar a arquitetura de sistemas e infraestrutura sob perspectiva de seguranca, identificando riscos estruturais e recomendando controles de design.

## Agents
- **cyber-chief** (lead) — Coordena review de arquitetura
- **jim-manico** (reviewer) — Avalia aspectos de AppSec e design
- **omar-santos** (reviewer) — Avalia aspectos de cloud e infraestrutura

## Inputs
- Diagramas de arquitetura dos sistemas
- Threat models existentes
- Data flow diagrams
- Requisitos de seguranca e compliance

## Steps
1. Revisar arquitetura geral quanto a principios de security by design
2. Avaliar separacao de responsabilidades e defense in depth
3. Verificar implementacao de zero trust principles
4. Analisar pontos de autenticacao e autorizacao na arquitetura
5. Revisar criptografia em transito e at rest
6. Avaliar resiliencia e redundancia contra ataques
7. Verificar segmentacao de rede e isolamento de workloads
8. Identificar single points of failure de seguranca
9. Documentar findings com recomendacoes de design
10. Registrar no `risk-register`

## Output
- Relatorio de architecture security review
- Lista de riscos estruturais com recomendacoes de design
- Mapeamento de gaps contra zero trust principles
- Registro no `risk-register`

## Quality Gates
- [ ] Principios de security by design avaliados
- [ ] Defense in depth verificado em todas as camadas
- [ ] Zero trust principles avaliados
- [ ] Criptografia em transito e at rest validada
- [ ] Single points of failure identificados
- [ ] Checklist `threat-model-quality` atendido
- [ ] Checklist `cloud-security-assessment-quality` validado
