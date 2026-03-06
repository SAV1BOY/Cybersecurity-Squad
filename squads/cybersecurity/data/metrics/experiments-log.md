# Experiments Log

Registro de experimentos e iniciativas piloto do programa de seguranca.

## Schema do Registro

| Experiment ID | Title | Hypothesis | Start Date | Duration | Status | Result |
|--------------|-------|------------|------------|----------|--------|--------|
| EXP-001 | UEBA para deteccao de insider threat | ML-based UEBA reduzira false positives em 40% | 2026-01-15 | 90 days | In Progress | Pendente |
| EXP-002 | Shift-left SAST no pre-commit | SAST no pre-commit reduzira vulns em producao em 30% | 2025-11-01 | 60 days | Completed | Reducao de 25%, adotado |
| EXP-003 | Purple team automation com Atomic Red Team | Testes automatizados validarao 80% das deteccoes | 2026-02-01 | 45 days | In Progress | Pendente |
| EXP-004 | Bug bounty programa piloto | Programa externo encontrara vulns nao cobertas | 2026-01-01 | 90 days | Completed | 12 vulns unicas, programa expandido |
| EXP-005 | ChatOps para incident response | Integracao Slack reducira tempo de coordenacao em 50% | 2026-02-15 | 30 days | In Progress | Pendente |

## Status Validos

- **Proposed**: Experimento desenhado, aguardando aprovacao
- **In Progress**: Experimento em execucao
- **Completed**: Finalizado com resultados documentados
- **Abandoned**: Cancelado com justificativa

## Template de Experimento

1. **Hipotese**: O que esperamos provar ou refutar
2. **Metricas de Sucesso**: Como mediremos o resultado
3. **Escopo**: Limites e restricoes do experimento
4. **Riscos**: Potenciais impactos negativos
5. **Duracao**: Periodo definido para o teste
6. **Resultado**: Conclusao com dados de suporte
7. **Decisao**: Adotar, iterar ou abandonar

## Principios

- Definir hipotese clara e mensuravel antes de iniciar
- Limitar escopo para permitir avaliacao rapida
- Documentar resultados independente do outcome
- Compartilhar aprendizados com o time mesmo em falhas
