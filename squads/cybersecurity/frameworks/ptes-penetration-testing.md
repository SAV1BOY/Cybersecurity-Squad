# PTES — Penetration Testing Execution Standard

## Overview

O Penetration Testing Execution Standard (PTES) e um framework que define as sete secoes de um teste de penetracao completo, desde o planejamento ate o relatorio final. Diferente de guias de alto nivel, o PTES fornece detalhamento tecnico significativo em cada fase, incluindo orientacoes especificas sobre ferramentas, tecnicas e entregaveis. E amplamente utilizado como referencia para estruturar engagements de pentest e garantir consistencia e qualidade nos resultados entregues.

## Core Concepts

### As 7 Secoes do PTES

#### 1. Pre-engagement Interactions

Atividades realizadas antes do inicio tecnico do teste:

- Definicao de escopo detalhado incluindo alvos in-scope e out-of-scope.
- Assinatura de autorizacao formal (Authorization Letter ou Statement of Work).
- Estabelecimento de Rules of Engagement (RoE) com restricoes e limites.
- Definicao de janelas de teste, pontos de contato e canais de comunicacao de emergencia.
- Acordo sobre formato e prazo de entrega do relatorio.
- Definicao de tratamento de vulnerabilidades criticas encontradas durante o teste.

#### 2. Intelligence Gathering

Coleta de informacoes sobre o alvo utilizando tecnicas passivas e ativas:

- **OSINT** — Coleta de informacoes publicas sobre a organizacao, funcionarios e infraestrutura.
- **Footprinting** — Mapeamento de dominios, subdomínios, ranges de IP e tecnologias expostas.
- **Fingerprinting** — Identificacao de sistemas operacionais, servicos e versoes de software.
- **Social Engineering Reconnaissance** — Identificacao de alvos humanos e vetores de engenharia social.
- Ferramentas: Amass, Subfinder, Shodan, theHarvester, LinkedIn, SpiderFoot.

#### 3. Threat Modeling

Analise de ameacas especifica para o alvo baseada nas informacoes coletadas:

- Identificacao de ativos de alto valor e dados sensiveis no escopo.
- Mapeamento de vetores de ataque mais provaveis baseado na superficie exposta.
- Priorizacao de alvos por valor de negocio e probabilidade de sucesso.
- Definicao de cenarios de ataque alinhados aos objetivos do engagement.

#### 4. Vulnerability Analysis

Identificacao e validacao de vulnerabilidades nos sistemas alvo:

- **Automated Scanning** — Scanning com ferramentas como Nessus, Nuclei e OpenVAS.
- **Manual Testing** — Verificacao manual de vulnerabilidades de logica e configuracao.
- **Correlation** — Cruzamento de resultados de multiplas ferramentas para reducir falsos positivos.
- **Research** — Pesquisa de exploits e tecnicas para vulnerabilidades identificadas.
- Classificacao de vulnerabilidades por criticidade e explorabilidade.

#### 5. Exploitation

Exploracao controlada de vulnerabilidades para demonstrar impacto real:

- Execucao de exploits validados em ambiente controlado quando possivel.
- Bypass de controles de seguranca (AV evasion, WAF bypass, EDR evasion).
- Obtencao de acesso inicial e estabelecimento de presenca no ambiente.
- Documentacao de cada passo com evidencias (screenshots, logs, payloads).
- Respeito estrito as Rules of Engagement durante toda a fase.

#### 6. Post-Exploitation

Atividades realizadas apos acesso inicial para demonstrar impacto maximo:

- **Privilege Escalation** — Elevacao de privilegios para acesso administrativo.
- **Lateral Movement** — Movimentacao entre sistemas para ampliar o comprometimento.
- **Data Exfiltration** — Demonstracao de acesso a dados sensiveis (sem exfiltrar dados reais).
- **Persistence** — Demonstracao de mecanismos de persistencia (em ambiente de teste).
- **Pivoting** — Uso de sistemas comprometidos para acessar redes segmentadas.
- Avaliacao do impacto real ao negocio com base no acesso obtido.

#### 7. Reporting

Documentacao completa dos resultados em formato acionavel:

- **Executive Summary** — Visao de alto nivel do risco para stakeholders de negocio.
- **Technical Report** — Detalhamento tecnico de cada vulnerabilidade com evidencias.
- **Finding Details** — Descricao, severidade, evidencia, impacto e recomendacao de remediacao.
- **Attack Narrative** — Descricao da cadeia de ataque do inicio ao objetivo final.
- **Remediation Roadmap** — Priorizacao de acoes de remediacao por impacto e esforco.

## Practical Application

### Classificacao de Engagements

| Tipo | Conhecimento | Objetivo |
|------|-------------|----------|
| Black Box | Sem informacao previa | Simular atacante externo |
| Grey Box | Credenciais e documentacao parcial | Simular insider ou pos-phishing |
| White Box | Acesso completo ao codigo e arquitetura | Maximizar cobertura de vulnerabilidades |

### Checklist de Qualidade por Secao

- Pre-engagement: RoE assinadas, escopo documentado, contatos de emergencia definidos.
- Intelligence Gathering: OSINT report entregue, superficie de ataque mapeada.
- Threat Modeling: Attack scenarios definidos, alvos priorizados.
- Vulnerability Analysis: Scans executados, falsos positivos filtrados, findings validados.
- Exploitation: Evidencias capturadas, chain of compromise documentada.
- Post-Exploitation: Impacto de negocio demonstrado, dados sensiveis identificados.
- Reporting: Executive summary, technical findings, remediation roadmap entregues.

### Ferramentas por Secao

| Secao | Ferramentas |
|-------|-------------|
| Intelligence | Amass, Subfinder, Shodan, Nmap |
| Vulnerability | Nessus, Nuclei, Burp Suite, Nikto |
| Exploitation | Metasploit, Cobalt Strike, Sliver, custom scripts |
| Post-Exploitation | BloodHound, Mimikatz, Impacket, CrackMapExec |
| Reporting | Ghostwriter, PlexTrac, SysReptor |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O offense-layer estrutura todos os pentests seguindo as sete secoes do PTES.
- O finding-structure-standard define o formato de findings alinhado a secao Reporting.
- O evidence-standard especifica requisitos de evidencia para cada fase do engagement.
- O nist-800-115-technical-testing complementa o PTES com orientacoes adicionais de testing.
- O osstmm oferece metodologia alternativa com foco em metricas de seguranca operacional.
- O retest-method valida remediacoes de findings identificados em engagements PTES.
- O red-team-maturity-model avalia a qualidade de execucao de cada secao PTES pela equipe.
- O bug-bounty-framework referencia secoes do PTES para orientar pesquisadores externos.
- Relatorios de pentest sao armazenados no repositorio do squad e metricas rastreadas no dashboard.
