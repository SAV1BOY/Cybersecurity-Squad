# Threat Model Project

Template de projeto para conducao de threat modeling.

## Visao Geral

| Campo | Valor |
|-------|-------|
| Sistema | [Nome do sistema/feature] |
| Metodologia | STRIDE + DREAD |
| Facilitador | [AppSec engineer] |
| Participantes | [Dev lead, architect, product] |
| Duracao | [1-2 sessoes de 2h] |

## Preparacao (Pre-sessao)

- [ ] Obter documentacao de arquitetura existente
- [ ] Identificar participantes (dev, product, infra)
- [ ] Preparar template de Data Flow Diagram (DFD)
- [ ] Revisar threat models anteriores do sistema
- [ ] Agendar sessao de 2h com todos os participantes

## Sessao 1: Modelagem (2h)

### Decomposicao do Sistema (45 min)
- [ ] Desenhar Data Flow Diagram com o time
- [ ] Identificar componentes: processos, data stores, external entities
- [ ] Mapear fluxos de dados entre componentes
- [ ] Definir trust boundaries

### Identificacao de Ameacas (45 min)
- [ ] Aplicar STRIDE para cada componente e fluxo
- [ ] Brainstorm de cenarios de ataque relevantes
- [ ] Documentar cada ameaca identificada
- [ ] Priorizar por likelihood e impact

### Mitigacoes (30 min)
- [ ] Identificar controles existentes para cada ameaca
- [ ] Propor controles adicionais necessarios
- [ ] Definir owners para implementacao

## Sessao 2: Revisao (1h)

- [ ] Revisar ameacas e mitigacoes documentadas
- [ ] Validar priorizacao com o time
- [ ] Criar action items para controles faltantes
- [ ] Definir criterios para re-avaliacao

## Deliverables

- Documento de threat model completo
- Data Flow Diagram atualizado
- Lista de ameacas com rating e mitigacoes
- Action items com owners e prazos
- Criterios de trigger para revisao

## Quando Revisar

- Mudanca arquitetural significativa
- Nova integracao com terceiros
- Novo tipo de dado processado
- Apos incidente de seguranca relacionado
- Revisao anual programada
