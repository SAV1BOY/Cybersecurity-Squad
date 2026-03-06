# Threat Modeling - Ficha de Referencia

## Metadados
- **Titulo**: Threat Modeling: Designing for Security
- **Autor**: Adam Shostack
- **Categoria**: Application Security / Security Design

## Descricao Geral
Referencia definitiva sobre threat modeling, escrita por um dos criadores do
processo na Microsoft. Cobre metodologias como STRIDE, attack trees e
processos praticos para integrar threat modeling no ciclo de desenvolvimento.

## Conceitos-Chave
- STRIDE methodology (Spoofing, Tampering, Repudiation, Information Disclosure, DoS, EoP)
- Data Flow Diagrams (DFD) para modelagem de ameacas
- Attack trees e attack libraries
- Threat modeling em agile e DevOps
- Risk rating e prioritization frameworks
- Mitigations mapping e validation
- Threat modeling workshops facilitation
- Automation de threat modeling
- Threat modeling para cloud e microservices
- Integration com SDLC e security gates

## Por Que Importa para o Squad
Threat modeling e a atividade de seguranca com melhor custo-beneficio. Encontrar
vulnerabilidades em fase de design e ordens de magnitude mais barato que
encontra-las em producao.

## Como o Squad Utiliza
- **Design Reviews**: metodologia para revisoes de arquitetura
- **AppSec Program**: processo formal de threat modeling
- **Training**: workshops para times de desenvolvimento
- **Risk Assessment**: entrada para avaliacoes de risco
- **Security Champions**: habilidade core para champions

## Complementa
- manico-iron-clad-java.md (implementacao de mitigacoes)
- stuttard-web-application-hackers.md (validacao ofensiva)
- mcgraw-software-security.md (security lifecycle)

## Nivel de Profundidade
Intermediario - requer entendimento de arquitetura de software.

## Notas do Squad
Implementar sessoes regulares de threat modeling para novos projetos e mudancas
significativas. Manter uma biblioteca de threat models como referencia.
