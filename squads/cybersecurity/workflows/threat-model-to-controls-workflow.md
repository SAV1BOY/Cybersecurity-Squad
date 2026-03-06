# Threat Model to Controls Workflow

Processo que transforma um threat model em controles de seguranca implementaveis e rastreaveis.

## Objetivo

Converter ameacas identificadas durante o threat modeling em controles tecnicos e organizacionais concretos, garantindo que cada ameaca mapeada tenha pelo menos um controle associado.

## Inputs

- Diagrama de arquitetura do sistema-alvo
- Data flow diagrams (DFDs) atualizados
- Lista de atores de ameaca relevantes
- Framework de referencia (STRIDE, PASTA, LINDDUN)

## Stages

### 1. Scope Definition

- Responsavel: **Threat Model Lead Agent**
- Definir boundaries do sistema a ser modelado
- Identificar trust boundaries e entry points
- Validar DFDs com a equipe de engenharia

### 2. Threat Identification

- Responsavel: **Threat Analyst Agent**
- Aplicar framework selecionado (ex: STRIDE por elemento)
- Listar ameacas por componente e data flow
- Classificar cada ameaca por likelihood e impact

### 3. Threat Prioritization

- Responsavel: **Risk Analyst Agent**
- Calcular risk score combinando likelihood e impact
- Ponto de decisao: **Risco acima do threshold aceitavel?**
  - Sim -> definir controle obrigatorio
  - Nao -> documentar como risco aceito com justificativa

### 4. Control Selection

- Responsavel: **Controls Architect Agent**
- Mapear cada ameaca priorizada a um ou mais controles
- Referenciar controles em frameworks conhecidos (NIST 800-53, CIS Controls, ISO 27001)
- Classificar controles como preventive, detective ou corrective

### 5. Control Design

- Responsavel: **Security Engineer Agent**
- Detalhar implementacao tecnica de cada controle
- Definir requisitos de configuracao, tooling e monitoramento
- Validar viabilidade com equipe de engenharia

### 6. Implementation Tracking

- Responsavel: **Project Tracker Agent**
- Criar tickets para cada controle a ser implementado
- Associar controles ao threat model de origem
- Monitorar progresso e reportar blockers

### 7. Validation

- Responsavel: **Validation Agent**
- Testar eficacia de cada controle implementado
- Ponto de decisao: **Controle mitiga a ameaca?**
  - Sim -> marcar como implemented e effective
  - Nao -> retornar ao design para ajustes

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Ameaca sem controle viavel | Nenhum controle tecnico disponivel | Propor controle compensatorio ou aceitar risco |
| Controle muito custoso | Custo > valor do asset protegido | Reavaliar com risk committee |
| Mudanca de arquitetura | DFD alterado durante o processo | Reiniciar threat identification para componentes afetados |

## Outputs

- Threat model documentado e versionado
- Matriz de ameacas vs controles (traceability matrix)
- Tickets de implementacao criados
- Relatorio de validacao de controles
