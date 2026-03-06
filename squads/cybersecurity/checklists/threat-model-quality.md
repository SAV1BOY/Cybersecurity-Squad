# Threat Model Quality Gate

Checklist de qualidade para modelagem de ameacas.

## Escopo e Contexto
- [ ] Sistema/aplicacao alvo claramente definido
- [ ] Business context e criticidade documentados
- [ ] Stakeholders identificados e envolvidos no processo
- [ ] Metodologia escolhida (STRIDE, PASTA, LINDDUN, Attack Trees)
- [ ] Iteracao anterior do threat model revisada (se existente)

## Decomposicao do Sistema
- [ ] Data Flow Diagram (DFD) criado com todos os componentes
- [ ] Trust boundaries claramente marcados no diagrama
- [ ] Entry points e exit points identificados
- [ ] Data stores e data flows classificados por sensibilidade
- [ ] External dependencies e third-party services mapeados
- [ ] Actors e roles documentados com niveis de confianca

## Identificacao de Ameacas
- [ ] STRIDE analysis aplicada a cada componente/fluxo
- [ ] Spoofing threats identificados para cada entry point
- [ ] Tampering threats para data stores e data flows
- [ ] Repudiation risks avaliados para acoes criticas
- [ ] Information Disclosure risks para dados sensiveis
- [ ] Denial of Service threats para componentes criticos
- [ ] Elevation of Privilege paths documentados
- [ ] Threat library consultada para ameacas conhecidas do dominio

## Avaliacao de Risco
- [ ] Likelihood estimada para cada ameaca (Low, Medium, High)
- [ ] Impact classificado para cada ameaca
- [ ] Risk score calculado (likelihood x impact)
- [ ] Ameacas priorizadas por risk score
- [ ] Existing mitigations mapeadas para cada ameaca
- [ ] Residual risk documentado apos mitigations

## Mitigacoes e Controles
- [ ] Countermeasures propostas para cada ameaca nao mitigada
- [ ] Mitigacoes mapeadas a controles tecnicos especificos
- [ ] Accepted risks documentados com justificativa e owner
- [ ] Security requirements derivados do threat model

## Documentacao e Manutencao
- [ ] Threat model documentado em formato reproduzivel (tool/template)
- [ ] Versionamento do threat model alinhado com releases
- [ ] Review triggers definidos (mudanca de arquitetura, novo feature)
- [ ] Findings integrados no backlog de desenvolvimento
- [ ] Apresentacao do modelo realizada para equipe tecnica
