# LINDDUN — Privacy Threat Modeling Framework

## Overview

O LINDDUN e um framework de modelagem de ameacas focado especificamente em privacidade, desenvolvido pela KU Leuven. Enquanto o STRIDE aborda propriedades classicas de seguranca, o LINDDUN complementa essa analise identificando ameacas que afetam a privacidade de dados pessoais. Com a crescente importancia de regulamentacoes como LGPD e GDPR, o framework fornece uma abordagem sistematica para identificar e mitigar riscos de privacidade no design de sistemas que processam dados pessoais.

## Core Concepts

### As Sete Categorias de Ameacas de Privacidade

#### Linking

Associacao de dados ou acoes a um individuo combinando informacoes de multiplas fontes:

- Correlacao de datasets anonimizados com dados publicos para reidentificacao.
- Cruzamento de logs de acesso com informacoes de RH para identificar comportamentos.
- Contramedidas: data minimization, pseudonymization, k-anonymity, differential privacy.

#### Identifying

Aprendizado da identidade de um individuo a partir de dados supostamente anonimos:

- Reidentificacao por quasi-identifiers (data de nascimento, CEP, genero).
- Fingerprinting de dispositivos ou navegadores para rastreamento de usuarios.
- Contramedidas: anonymization robusta, privacy-preserving analytics, data aggregation.

#### Non-repudiation (Involuntaria)

Incapacidade do individuo de negar ter realizado uma acao devido a coleta excessiva de evidencias:

- Registro detalhado de todas as acoes do usuario sem necessidade de negocio.
- Audit trails granulares demais que permitem reconstrucao completa de comportamento.
- Contramedidas: logging proporcional, data retention policies, right to erasure.

#### Detecting

Deteccao de que um individuo esta envolvido em uma atividade sem conhecer os detalhes:

- Observacao de padroes de acesso que revelam interesses ou comportamentos sensiveis.
- Metadata de comunicacoes que revela relacionamentos mesmo sem conteudo.
- Contramedidas: traffic padding, onion routing, plausible deniability.

#### Data Disclosure

Exposicao excessiva de dados pessoais a partes nao autorizadas ou alem do necessario:

- Compartilhamento de dados com terceiros sem consentimento adequado.
- APIs que retornam mais dados pessoais do que o necessario para a funcionalidade.
- Contramedidas: purpose limitation, data minimization, access controls granulares.

#### Unawareness

Processamento de dados pessoais sem o conhecimento ou consentimento informado do individuo:

- Coleta de dados sem transparencia sobre finalidade e uso.
- Mudanca de finalidade de processamento sem notificacao ao titular.
- Contramedidas: privacy notices, consent management, privacy dashboards.

#### Non-compliance

Desvio de politicas, legislacao ou melhores praticas de privacidade:

- Processamento de dados pessoais em desacordo com a base legal definida.
- Transferencia internacional de dados sem salvaguardas adequadas.
- Contramedidas: Privacy Impact Assessment, DPO, compliance monitoring, auditorias.

### LINDDUN GO

Versao simplificada do framework projetada para sessoes de threat modeling mais ageis:

- Utiliza cards com cenarios de ameacas de privacidade predefinidos.
- Cada card descreve uma ameaca, exemplo concreto e possivel mitigacao.
- Sessoes de 60-90 minutos com equipes multidisciplinares.
- Ideal como primeiro passo para equipes sem experiencia em privacy by design.

## Practical Application

### Processo de Privacy Threat Modeling

1. Criar Data Flow Diagram do sistema focando em fluxos de dados pessoais.
2. Identificar categorias de dados pessoais processados e respectivas bases legais.
3. Para cada elemento do DFD, aplicar as sete categorias LINDDUN sistematicamente.
4. Avaliar cada ameaca identificada por severidade de impacto a privacidade.
5. Mapear mitigacoes utilizando Privacy Enhancing Technologies (PETs) e controles organizacionais.
6. Documentar decisoes em Privacy Impact Assessment (PIA) ou DPIA conforme regulamentacao.
7. Validar implementacao das mitigacoes com testes de privacidade especificos.

### Mapeamento LINDDUN para LGPD/GDPR

| Ameaca LINDDUN | Principio LGPD/GDPR Violado | Artigo Referencia |
|----------------|-----------------------------|--------------------|
| Linking | Limitacao de Finalidade | Art. 6 LGPD / Art. 5(1)(b) GDPR |
| Identifying | Minimizacao de Dados | Art. 6 III LGPD / Art. 5(1)(c) GDPR |
| Data Disclosure | Seguranca e Confidencialidade | Art. 46 LGPD / Art. 32 GDPR |
| Unawareness | Transparencia | Art. 6 VI LGPD / Art. 5(1)(a) GDPR |
| Non-compliance | Responsabilizacao | Art. 50 LGPD / Art. 5(2) GDPR |

### Privacy Enhancing Technologies (PETs)

| Tecnica | Ameaca Mitigada | Aplicacao |
|---------|-----------------|-----------|
| Differential Privacy | Linking, Identifying | Analytics preservando privacidade |
| Homomorphic Encryption | Data Disclosure | Processamento de dados criptografados |
| Federated Learning | Data Disclosure, Linking | ML sem centralizar dados pessoais |
| Zero-Knowledge Proofs | Identifying, Detecting | Verificacao sem revelar dados |
| Synthetic Data | Linking, Identifying | Ambientes de teste sem dados reais |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer conduz sessoes LINDDUN GO para sistemas que processam dados pessoais.
- O stride-threat-model e utilizado em conjunto com LINDDUN para cobertura completa de seguranca e privacidade.
- O governance-layer mantem politicas de privacidade alinhadas as mitigacoes identificadas via LINDDUN.
- O finding-structure-standard suporta classificacao de findings com impacto a privacidade.
- O risk-scoring-model incorpora fatores de risco de privacidade derivados de analises LINDDUN.
- O cloudsec-layer avalia controles de privacidade de cloud providers usando categorias LINDDUN.
- O security-champion-program inclui modulo de privacy by design baseado no LINDDUN.
- DPIAs conduzidas pelo squad utilizam LINDDUN como framework estruturante para analise de ameacas.
