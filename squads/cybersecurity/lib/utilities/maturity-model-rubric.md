# Maturity Model Rubric

Rubrica para avaliacao de maturidade do programa de seguranca por dominio.

## Escala de Maturidade (1-5)

### Level 1 - Initial
- Processos ad-hoc e reativos
- Sem documentacao formal
- Depende de conhecimento individual
- Sem metricas ou medicoes

### Level 2 - Developing
- Processos basicos definidos mas inconsistentes
- Documentacao parcial existe
- Ferramentas basicas implementadas
- Metricas manuais e esporadicas

### Level 3 - Defined
- Processos padronizados e documentados
- Roles e responsabilidades claros
- Ferramentas integradas e operacionais
- Metricas coletadas regularmente

### Level 4 - Managed
- Processos medidos com KPIs definidos
- Melhoria baseada em dados e metricas
- Automacao de tarefas repetitivas
- Revisao e otimizacao regular

### Level 5 - Optimizing
- Melhoria continua proativa
- Inovacao e adaptacao ao threat landscape
- Automacao extensiva com orquestracao
- Benchmark contra industria e peers

## Rubrica por Dominio

### Vulnerability Management
| Level | Criterios |
|-------|-----------|
| 1 | Scans ad-hoc, sem processo de remediacao |
| 2 | Scans mensais, remediacao sem SLA |
| 3 | Scans semanais, SLAs definidos, tracking de findings |
| 4 | Scans continuos, MTTR medido, cobertura > 90% |
| 5 | Risk-based prioritization, auto-remediation, SLA compliance > 95% |

### Detection & Response
| Level | Criterios |
|-------|-----------|
| 1 | Sem monitoramento centralizado |
| 2 | SIEM basico, alertas manuais |
| 3 | SIEM com regras customizadas, playbooks documentados |
| 4 | Detection as code, SOAR parcial, MTTD < 4h |
| 5 | ML/UEBA, SOAR completo, purple team regular, MTTD < 1h |

### Application Security
| Level | Criterios |
|-------|-----------|
| 1 | Sem testes de seguranca em aplicacoes |
| 2 | Pentests anuais em apps criticas |
| 3 | SAST/DAST no CI/CD, threat modeling para novos projetos |
| 4 | Security champions, SCA, container scanning, metricas de cobertura |
| 5 | DevSecOps maduro, shift-left completo, bug bounty ativo |

## Processo de Avaliacao

Avaliacao trimestral com evidencias documentadas para cada nivel.
Consenso entre security leadership e stakeholders tecnicos.
Resultados registrados no maturity-score-history.
