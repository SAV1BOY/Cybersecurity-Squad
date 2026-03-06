# Remediation Plans

Exemplos de planos de remediation que traduzem findings em acoes concretas e priorizadas.

## Estrutura de Remediation Plan

1. **Finding Reference** - ID e titulo do finding original
2. **Priority** - Baseada em risk score (impacto x probabilidade)
3. **Owner** - Time ou pessoa responsavel
4. **Action Items** - Steps especificos para correcao
5. **Timeline** - SLA baseado em severidade
6. **Validation Criteria** - Como confirmar que foi corrigido
7. **Dependencies** - Bloqueios ou pre-requisitos

## SLA por Severidade (Exemplo)

| Severidade | SLA Remediation | SLA Retest |
|-----------|----------------|------------|
| Critical  | 72 horas       | 1 semana   |
| High      | 2 semanas      | 3 semanas  |
| Medium    | 30 dias        | 45 dias    |
| Low       | 90 dias        | Proximo ciclo |

## Exemplo: Plano para Patch Management Gap

- **Finding:** 47 servidores com patches criticos pendentes ha 90+ dias
- **Owner:** Time de Infraestrutura
- **Acoes:** (1) Inventario completo, (2) Teste em staging, (3) Deploy em waves
- **Timeline:** 14 dias para critical, 30 dias para high
- **Validacao:** Vulnerability scan pos-patch com zero critical/high

## Dicas de Priorizacao

- Quick wins primeiro (alto impacto, baixo esforco)
- Agrupar findings com mesma root cause
- Considerar compensating controls enquanto fix definitivo nao esta pronto
- Documentar risk acceptance formal para findings nao remediados
