# Evolution of Detection

Historia e evolucao das tecnologias e abordagens de deteccao de ameacas.

## Timeline Evolutiva

### Era 1: Signature-Based Detection (1990-2005)
- Antivirus com assinaturas de malware conhecidos
- IDS baseado em regras Snort
- Pattern matching simples contra ameacas conhecidas
- Limitacao: zero-days e variantes nao detectados
- Atualizacao diaria de assinaturas como defesa primaria

### Era 2: Heuristic e Behavioral (2006-2012)
- Heuristica para detectar variantes de malware
- Sandboxing para analise dinamica de arquivos suspeitos
- Behavioral rules no SIEM (threshold, sequence)
- Network behavior analysis (NBA/NTA)
- Melhora na deteccao de ameacas desconhecidas

### Era 3: Indicator-Based (2013-2017)
- Threat intelligence feeds com IOCs (IPs, hashes, domains)
- Integracao de intel no SIEM e ferramentas de seguranca
- Pyramid of Pain: foco em TTPs alem de IOCs atomicos
- YARA rules para deteccao flexivel de malware
- STIX/TAXII para compartilhamento padronizado de intel

### Era 4: Behavior Analytics e ML (2018-2022)
- UEBA (User and Entity Behavior Analytics)
- Machine learning para deteccao de anomalias
- EDR/XDR com behavioral detection
- Detection as code com CI/CD pipeline
- MITRE ATT&CK como framework de cobertura

### Era 5: AI-Powered Detection (2023-presente)
- Large Language Models para analise de logs
- Automated threat hunting com AI
- Graph-based detection para attack paths
- Generative AI para criacao de regras de deteccao
- Real-time correlation com contexto enriquecido

## Pyramid of Pain (David Bianco)

| Nivel | Tipo | Dificuldade para Atacante |
|-------|------|--------------------------|
| 1 | Hash Values | Trivial mudar |
| 2 | IP Addresses | Facil mudar |
| 3 | Domain Names | Simples mudar |
| 4 | Network/Host Artifacts | Incomodo |
| 5 | Tools | Desafiador |
| 6 | TTPs | Muito dificil |

## Principio Atual

Detectar em niveis mais altos da Pyramid of Pain (TTPs) e mais eficaz
e duravel do que depender de IOCs atomicos que atacantes mudam facilmente.
