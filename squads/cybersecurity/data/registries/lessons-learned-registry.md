# Lessons Learned Registry

Registro de licoes aprendidas a partir de incidentes, projetos e exercicios de seguranca.

## Schema do Registro

| Lesson ID | Source | Date | Category | Description | Action Taken | Impact | Owner |
|-----------|--------|------|----------|-------------|-------------|--------|-------|
| LL-2026-001 | INC-2026-001 | 2026-01-12 | Detection | Phishing nao detectado por falta de regra para typosquatting | Criada regra DET-015 para dominios similares | Reducao de 60% em phishing nao detectado | @soc-team |
| LL-2026-002 | Pentest Q1 | 2026-02-01 | AppSec | SSRF via redirect nao coberto por DAST | Adicionado test case customizado ao scanner | Novo finding category coberta | @appsec-team |
| LL-2026-003 | Tabletop Exercise | 2026-02-15 | IR | Falta de playbook para supply chain compromise | Desenvolvido playbook PB-012 | Tempo de resposta estimado reduzido em 50% | @ir-team |

## Categorias

- **Detection**: Gaps ou melhorias na capacidade de deteccao
- **Response**: Melhorias no processo de resposta a incidentes
- **Prevention**: Controles preventivos identificados como necessarios
- **AppSec**: Licoes de application security
- **Process**: Melhorias em processos e workflows
- **Communication**: Melhorias em comunicacao durante crises

## Fontes de Licoes

- Incidentes de seguranca (post-incident review)
- Pentests e red team engagements
- Tabletop exercises e simulacoes
- Auditorias internas e externas
- Analise de breaches publicos relevantes
- Feedback de security champions

## Processo

1. Licao identificada durante review ou retrospectiva
2. Documentacao no registro com acao proposta
3. Atribuicao de owner e prazo para acao
4. Acompanhamento na reuniao mensal de seguranca
5. Validacao de eficacia da acao implementada

## Principio Fundamental

Abordagem blameless: o foco e sempre no processo e nos controles, nunca em
individuos. O objetivo e melhorar continuamente o programa de seguranca.
