# NIST 800-115 — Technical Guide to Information Security Testing and Assessment

## Overview

O NIST Special Publication 800-115 fornece diretrizes tecnicas para planejar e conduzir testes e avaliacoes de seguranca da informacao. O documento abrange desde revisoes de documentacao ate testes de penetracao completos, oferecendo uma abordagem metodica para identificar vulnerabilidades em sistemas e redes. Publicado em 2008, continua sendo referencia fundamental para estruturar programas de security testing em organizacoes de todos os portes.

## Core Concepts

### Categorias de Tecnicas de Avaliacao

O framework organiza as tecnicas em tres categorias principais:

#### 1. Review Techniques

Tecnicas de revisao que examinam documentacao, configuracoes e politicas:

- **Documentation Review** — Analise de politicas, procedimentos, arquiteturas e diagramas de rede.
- **Log Review** — Exame de registros de auditoria para identificar anomalias e eventos de seguranca.
- **Ruleset Review** — Avaliacao de regras de firewall, ACLs e politicas de filtragem.
- **System Configuration Review** — Verificacao de hardening e conformidade com baselines de seguranca.
- **File Integrity Checking** — Validacao de integridade de arquivos criticos contra hashes conhecidos.

#### 2. Target Identification and Analysis

Tecnicas para descoberta e analise de alvos no ambiente:

- **Network Discovery** — Mapeamento de hosts ativos, topologia e servicos disponiveis via scanning.
- **Network Port and Service Identification** — Enumeracao de portas abertas e versoes de servicos.
- **Vulnerability Scanning** — Identificacao automatizada de vulnerabilidades conhecidas em sistemas e aplicacoes.
- **Wireless Scanning** — Deteccao de access points, analise de protocolos e identificacao de rogue devices.

#### 3. Target Vulnerability Validation

Tecnicas que validam a explorabilidade real das vulnerabilidades identificadas:

- **Password Cracking** — Teste de robustez de credenciais via ataques de dicionario, brute force e rainbow tables.
- **Penetration Testing** — Simulacao controlada de ataques para validar cadeias de exploracao completas.
- **Social Engineering** — Testes de phishing, pretexting e physical security para avaliar o fator humano.

### Fases do Processo de Testing

| Fase | Atividade | Entregavel |
|------|-----------|------------|
| Planning | Definicao de escopo, regras de engajamento e autorizacao | Test Plan e RoE assinados |
| Discovery | Coleta de informacoes e identificacao de alvos | Asset inventory e scan results |
| Attack | Exploracao controlada de vulnerabilidades | Exploitation evidence |
| Reporting | Documentacao de findings com recomendacoes | Assessment Report |

## Practical Application

### Planejamento de Assessment

1. Definir objetivos claros alinhados aos riscos de negocio prioritarios.
2. Obter autorizacao formal por escrito do proprietario do sistema.
3. Estabelecer Rules of Engagement detalhando limites, horarios e pontos de contato.
4. Configurar ambiente de teste com ferramentas validadas e canais de comunicacao seguros.
5. Definir procedimentos de escalacao para situacoes imprevistas durante o teste.
6. Acordar formato do relatorio e cronograma de entrega dos resultados.

### Selecao de Tecnicas por Objetivo

- **Compliance Validation** — Priorizar review techniques e vulnerability scanning automatizado.
- **Risk Reduction** — Combinar vulnerability scanning com penetration testing direcionado.
- **Red Team Assessment** — Utilizar todas as categorias incluindo social engineering e physical testing.
- **Continuous Monitoring** — Automatizar scans periodicos com baseline comparison.

### Consideracoes de Seguranca durante Testes

- Manter backup dos dados de teste e evidencias em storage criptografado.
- Evitar testes destrutivos em ambientes de producao sem aprovacao explicita.
- Documentar cada acao executada para garantir reprodutibilidade e accountability.
- Comunicar imediatamente vulnerabilidades criticas descobertas durante o assessment.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O offense-layer utiliza as tres categorias de tecnicas como base para estruturar engagements de pentest.
- Rules of Engagement padronizadas estao documentadas e versionadas no repositorio do squad.
- O finding-structure-standard define o formato de documentacao de vulnerabilidades alinhado ao Reporting phase.
- O evidence-standard segue as diretrizes de preservacao de evidencias do NIST 800-115.
- Vulnerability scanning continuo alimenta o vuln-triage-playbook com dados atualizados.
- O retest-method implementa o ciclo de validacao pos-remediacao descrito no framework.
- Resultados de assessments sao rastreados no security-kpi-dashboard por tipo de teste e severidade.
- O ptes-penetration-testing complementa este framework com detalhamento especifico para pentests.
