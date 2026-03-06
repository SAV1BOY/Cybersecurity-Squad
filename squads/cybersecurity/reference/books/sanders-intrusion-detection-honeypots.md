# Intrusion Detection Honeypots - Ficha de Referencia

## Metadados
- **Titulo**: Intrusion Detection Honeypots: Detection through Deception
- **Autor**: Chris Sanders
- **Categoria**: Defensive Security / Deception Technology

## Descricao Geral
Abordagem pratica para implementacao de honeypots como mecanismo de deteccao de
intrusao. O livro cobre desde conceitos fundamentais de deception technology ate
implementacoes avancadas em ambientes corporativos.

## Conceitos-Chave
- Deception technology fundamentals e taxonomia
- Honeypot types: low-interaction vs high-interaction
- Honeytoken design e deployment strategies
- Network-based honeypots e honey services
- Credential honeypots e canary tokens
- Integration com SIEM e alerting pipelines
- Deception em cloud environments
- Metricas de eficacia de honeypots
- Legal considerations e ethical boundaries
- Operational security para deception ops

## Por Que Importa para o Squad
Honeypots sao uma das formas mais eficazes de deteccao com baixo false positive
rate. Permitem ao squad detectar atacantes que ja ultrapassaram o perimetro e
estao em fase de lateral movement.

## Como o Squad Utiliza
- **Detection Strategy**: planejamento de deception layers na infraestrutura
- **Early Warning**: alertas de alta fidelidade para intrusoes ativas
- **Red Team Awareness**: entender deception para evita-la em engagements
- **Threat Intel**: coletar TTPs de atacantes reais via honeypots expostos
- **Training**: exercicios de deploy e monitoramento de honeypots

## Ferramentas Mencionadas
- OpenCanary, Cowrie, Dionaea
- Canary Tokens (Thinkst)
- Artillery (honeypot tool)
- HoneyDB, T-Pot platform
- Custom honeypot frameworks

## Complementa
- sanders-applied-nsm.md (deteccao em rede)
- sanders-practical-packet-analysis.md (analise de trafego)
- bejtlich-practice-nsm.md (NSM abrangente)

## Nivel de Profundidade
Intermediario - requer conhecimento de redes e conceitos defensivos.

## Notas do Squad
Priorizar implementacao de honeytokens em ambientes de producao como quick win.
Canary tokens sao simples de implementar e oferecem deteccao de alta confianca
para lateral movement e data exfiltration.
