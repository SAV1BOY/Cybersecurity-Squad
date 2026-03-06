# FAIR — Factor Analysis of Information Risk

## Overview

O FAIR (Factor Analysis of Information Risk) e o unico modelo quantitativo de analise de risco de informacao internacionalmente padronizado (OpenFAIR, publicado pela Open Group). Diferente de abordagens qualitativas que classificam risco como alto/medio/baixo, o FAIR produz estimativas financeiras de risco expressas em termos monetarios, permitindo comparacao direta com outras categorias de risco empresarial. O modelo decompoe risco em fatores mensuraveis que podem ser estimados individualmente e combinados via simulacao Monte Carlo.

## Core Concepts

### Taxonomia FAIR

O FAIR decompoe risco em uma arvore hierarquica de fatores:

#### Risk (Risco)

Frequencia provavel de perda e magnitude provavel de perda associadas a um cenario de ameaca especifico.

#### Loss Event Frequency (LEF)

Frequencia esperada de eventos de perda em um periodo:

- **Threat Event Frequency (TEF)** — Quantas vezes um threat agent atua contra um ativo por periodo.
  - **Contact Frequency** — Frequencia de contato entre threat agent e ativo.
  - **Probability of Action** — Probabilidade de o threat agent agir ao ter contato.
- **Vulnerability (Vuln)** — Probabilidade de o ativo ser comprometido dado um ataque.
  - **Threat Capability (TCap)** — Capacidade tecnica do threat agent.
  - **Resistance Strength (RS)** — Forca dos controles defensivos do ativo.

#### Loss Magnitude (LM)

Magnitude financeira da perda quando um evento ocorre:

- **Primary Loss** — Perdas diretamente causadas pelo evento.
  - Productivity loss, Response cost, Replacement cost.
- **Secondary Loss** — Perdas indiretas resultantes da reacao de stakeholders.
  - Competitive advantage loss, Fines and judgments, Reputation damage.
- **Secondary Loss Event Frequency** — Probabilidade de perdas secundarias ocorrerem.

### Formas de Perda

O FAIR define seis formas de perda para quantificacao:

| Forma | Descricao | Exemplo |
|-------|-----------|---------|
| Productivity | Perda de produtividade operacional | Downtime de sistemas criticos |
| Response | Custo de resposta ao incidente | Forense, comunicacao, juridico |
| Replacement | Custo de substituicao de ativos | Reconstrucao de infraestrutura |
| Fines/Judgments | Multas regulatorias e decisoes judiciais | Sancoes LGPD/GDPR |
| Competitive Advantage | Perda de vantagem competitiva | Exfiltracao de propriedade intelectual |
| Reputation | Dano reputacional | Perda de clientes apos breach |

### Simulacao Monte Carlo

O FAIR utiliza simulacao Monte Carlo para combinar as distribuicoes de probabilidade de cada fator:

- Cada fator e estimado como um range (minimo, mais provavel, maximo) em vez de ponto unico.
- A simulacao executa milhares de iteracoes combinando os fatores aleatoriamente.
- O resultado e uma distribuicao de probabilidade de perda anualizada (ALE).
- Permite afirmacoes como "ha 90 por cento de probabilidade de que a perda anual esteja entre X e Y".

## Practical Application

### Processo de Analise FAIR

1. **Identificar o cenario de risco** — Definir o ativo, threat agent, efeito da ameaca e forma de perda.
2. **Estimar Loss Event Frequency** — Decompor em TEF e Vulnerability com ranges calibrados.
3. **Estimar Loss Magnitude** — Decompor em Primary e Secondary Loss por forma de perda.
4. **Executar simulacao** — Rodar Monte Carlo para gerar distribuicao de ALE.
5. **Interpretar resultados** — Analisar percentis (P10, P50, P90) para comunicacao de risco.
6. **Comparar cenarios** — Avaliar reducao de risco de diferentes opcoes de mitigacao.
7. **Comunicar resultados** — Apresentar em termos financeiros para decisores de negocio.

### Calibracao de Estimativas

Tecnicas para melhorar a qualidade das estimativas:

- **Expert Elicitation** — Entrevistas estruturadas com especialistas do dominio.
- **Historical Data** — Dados de incidentes passados da organizacao e do setor.
- **Industry Reports** — Relatorios como Verizon DBIR e IBM Cost of a Data Breach.
- **Decomposition** — Quebrar estimativas complexas em sub-componentes mais faceis de estimar.
- **Calibration Training** — Treinamento de estimadores para reduzir overconfidence bias.

### Exemplo de Cenario

```
Cenario: Ransomware em infraestrutura critica
Ativo: Ambiente de producao principal
Threat Agent: Grupos criminosos organizados
Efeito: Indisponibilidade e exfiltracao de dados

TEF: 1-3 vezes por ano (tentativas)
Vulnerability: 10-30% (probabilidade de sucesso)
LEF resultante: 0.1-0.9 eventos por ano

Primary Loss: R$ 500K - R$ 2M (response + productivity)
Secondary Loss: R$ 1M - R$ 5M (fines + reputation)
Prob. Secondary: 40-70%

ALE P50: R$ 800K
ALE P90: R$ 3.2M
```

### Ferramentas FAIR

| Ferramenta | Tipo | Descricao |
|------------|------|-----------|
| RiskLens | Comercial | Plataforma enterprise de analise FAIR |
| FAIR-U | Open Source | Ferramenta web simplificada para analise FAIR |
| PyFAIR | Open Source | Biblioteca Python para simulacao FAIR |
| Excel Templates | Template | Planilhas com simulacao Monte Carlo basica |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O risk-scoring-model utiliza FAIR como fundacao para quantificacao financeira de riscos.
- O governance-layer apresenta resultados FAIR ao board para suportar decisoes de investimento.
- O vuln-triage-playbook incorpora Loss Magnitude do FAIR na priorizacao de vulnerabilidades.
- O security-kpi-dashboard exibe ALE por cenario de risco para comunicacao executiva.
- O ir-layer alimenta dados de custo de resposta que calibram estimativas de Primary Loss.
- O nist-csf utiliza resultados FAIR para priorizar gaps entre Current e Target Profile.
- O stride-threat-model e pasta-threat-model identificam cenarios que sao quantificados via FAIR.
- Analises FAIR sao conduzidas para os top 10 cenarios de risco semestralmente.
- O bug-bounty-framework utiliza Loss Magnitude para calibrar recompensas por vulnerabilidade.
- Decisoes de aceitar, mitigar ou transferir risco sao fundamentadas em analises FAIR documentadas.
