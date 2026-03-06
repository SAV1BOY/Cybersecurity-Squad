# MITRE ATLAS — Adversarial Threat Landscape for AI Systems

## Overview

O MITRE ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems) e uma base de conhecimento de taticas e tecnicas adversarias direcionadas a sistemas de inteligencia artificial e machine learning. Modelado na estrutura do ATT&CK, o ATLAS cataloga ameacas reais observadas contra sistemas de ML em producao. Com a adocao acelerada de AI/ML em aplicacoes criticas, o ATLAS fornece o framework necessario para avaliar e mitigar riscos especificos desse dominio emergente.

## Core Concepts

### Taticas do ATLAS

O ATLAS define taticas especificas para o ciclo de vida de ataques contra sistemas ML:

| ID | Tatica | Objetivo |
|----|--------|----------|
| AML.TA0000 | Reconnaissance | Coletar informacoes sobre o sistema ML alvo |
| AML.TA0001 | Resource Development | Preparar recursos para atacar o sistema ML |
| AML.TA0002 | Initial Access | Obter acesso ao sistema ML ou seus componentes |
| AML.TA0003 | ML Model Access | Obter acesso ao modelo para queries ou manipulacao |
| AML.TA0004 | Execution | Executar codigo adversario no contexto do sistema ML |
| AML.TA0005 | Persistence | Manter acesso ao sistema ML apos reinicializacoes |
| AML.TA0006 | Defense Evasion | Evitar deteccao por controles de seguranca do sistema ML |
| AML.TA0007 | Discovery | Mapear o ambiente ML e seus componentes |
| AML.TA0008 | Collection | Coletar dados do sistema ML de interesse do adversario |
| AML.TA0009 | ML Attack Staging | Preparar e executar ataques especificos contra o modelo ML |
| AML.TA0010 | Exfiltration | Extrair dados ou modelos do ambiente ML |
| AML.TA0011 | Impact | Manipular, degradar ou destruir o sistema ML |

### Tecnicas Chave

#### Ataques contra Modelos

- **Adversarial Examples** — Entradas maliciosamente modificadas para causar classificacao incorreta pelo modelo. Perturbacoes imperceptiveis a humanos podem alterar completamente a predicao.
- **Model Poisoning** — Contaminacao dos dados de treinamento para inserir backdoors ou degradar performance do modelo em cenarios especificos.
- **Model Inversion** — Reconstrucao de dados de treinamento sensiveis a partir de acesso ao modelo treinado, violando privacidade.
- **Model Extraction** — Roubo da propriedade intelectual do modelo por meio de queries sistematicas para criar replica funcional.
- **Prompt Injection** — Manipulacao de inputs em LLMs para contornar instrucoes do sistema e executar acoes nao autorizadas.

#### Ataques contra Infraestrutura ML

- **ML Supply Chain Compromise** — Comprometimento de dependencias, modelos pre-treinados ou datasets de terceiros.
- **Notebook Exploitation** — Exploracao de vulnerabilidades em Jupyter Notebooks e plataformas de desenvolvimento ML.
- **Data Pipeline Manipulation** — Alteracao de dados em pipelines de ETL que alimentam modelos em producao.

### Case Studies

O ATLAS inclui case studies documentados de ataques reais incluindo:

- Evasao de sistemas de deteccao de malware usando adversarial examples.
- Extracao de modelos proprietarios de APIs de ML comerciais.
- Envenenamento de datasets publicos utilizados por multiplas organizacoes.
- Prompt injection em assistentes AI para exfiltrar dados de conversas.

## Practical Application

### AI/ML Threat Assessment

1. Inventariar sistemas de AI/ML em producao e classificar por criticidade de negocio.
2. Mapear superficie de ataque de cada sistema (model serving, training pipeline, data stores).
3. Identificar tecnicas ATLAS relevantes para cada superficie de ataque.
4. Avaliar controles existentes contra cada tecnica identificada.
5. Priorizar mitigacoes com base no risco residual e impacto de negocio.
6. Implementar monitoramento especifico para detectar ataques contra modelos ML.

### Controles de Seguranca para ML

| Ameaca | Controle | Implementacao |
|--------|----------|---------------|
| Adversarial Examples | Input validation e adversarial training | Validacao de distribuicao de inputs |
| Model Poisoning | Data provenance e integrity verification | Assinatura de datasets e auditoria |
| Model Extraction | Rate limiting e query monitoring | Deteccao de padroes de query anomalos |
| Prompt Injection | Input sanitization e output filtering | Guardrails e content filtering |
| Supply Chain | Model signing e SBOM para ML | Verificacao de integridade de artefatos |

### Modelo de Maturidade AI Security

- **Nivel 1** — Inventario de sistemas ML e classificacao basica de risco.
- **Nivel 2** — Threat assessment ATLAS e controles basicos implementados.
- **Nivel 3** — Monitoramento continuo, red team ML e resposta a incidentes AI-specific.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer incorpora verificacoes ATLAS no pipeline de review de aplicacoes com componentes ML.
- O offense-layer inclui tecnicas ATLAS em engagements que envolvem sistemas de AI/ML.
- O mitre-att-ck fornece a base metodologica que o ATLAS estende para o dominio de AI/ML.
- O risk-scoring-model inclui fatores de risco especificos para sistemas ML baseados no ATLAS.
- O finding-structure-standard suporta classificacao de vulnerabilidades mapeadas a tecnicas ATLAS.
- O stride-threat-model e pasta-threat-model sao complementados com ameacas AI-specific do ATLAS.
- O defense-layer monitora anomalias em APIs de model serving como indicador de model extraction.
- O security-kpi-dashboard rastreia inventario e postura de seguranca de sistemas ML em producao.
