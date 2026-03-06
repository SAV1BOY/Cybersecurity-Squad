# CIS Controls v8 — Center for Internet Security Critical Security Controls

## Overview

Os CIS Controls versao 8 sao um conjunto priorizado de 18 controles de seguranca cibernetica desenvolvidos pelo Center for Internet Security com base em dados reais de ataques. Diferente de frameworks abrangentes como NIST 800-53, os CIS Controls focam nas acoes de maior impacto para reducao de risco, organizados em tres Implementation Groups que permitem adocao gradual conforme a maturidade da organizacao. A versao 8 foi redesenhada para ser agnóstica a tecnologia, refletindo ambientes hibridos e cloud-native.

## Core Concepts

### Os 18 Controles

| # | Controle | Descricao |
|---|----------|-----------|
| 1 | Inventory and Control of Enterprise Assets | Inventario ativo de dispositivos fisicos, virtuais e cloud |
| 2 | Inventory and Control of Software Assets | Inventario de software autorizado e nao autorizado |
| 3 | Data Protection | Classificacao e protecao de dados sensiveis |
| 4 | Secure Configuration of Enterprise Assets and Software | Hardening de configuracoes |
| 5 | Account Management | Gestao de contas e credenciais |
| 6 | Access Control Management | Controle de acesso baseado em least privilege |
| 7 | Continuous Vulnerability Management | Identificacao e remediacao continua de vulnerabilidades |
| 8 | Audit Log Management | Coleta, retencao e analise de logs de auditoria |
| 9 | Email and Web Browser Protections | Protecoes contra ameacas via email e navegador |
| 10 | Malware Defenses | Prevencao e deteccao de malware |
| 11 | Data Recovery | Backup e recuperacao de dados |
| 12 | Network Infrastructure Management | Gestao segura de infraestrutura de rede |
| 13 | Network Monitoring and Defense | Monitoramento e defesa de rede |
| 14 | Security Awareness and Skills Training | Treinamento e conscientizacao |
| 15 | Service Provider Management | Gestao de seguranca de fornecedores |
| 16 | Application Software Security | Seguranca no ciclo de vida de aplicacoes |
| 17 | Incident Response Management | Gestao de resposta a incidentes |
| 18 | Penetration Testing | Testes de penetracao periodicos |

### Implementation Groups (IGs)

Os IGs definem subconjuntos progressivos de Safeguards baseados no perfil de risco:

- **IG1 (Essential Cyber Hygiene)** — 56 Safeguards fundamentais para organizacoes com recursos limitados e baixa complexidade de TI. Representa o minimo aceitavel de seguranca cibernetica.
- **IG2 (Intermediate)** — 74 Safeguards adicionais para organizacoes com equipe de TI dedicada que gerenciam dados sensiveis de clientes ou operacoes de negocio.
- **IG3 (Advanced)** — 23 Safeguards adicionais para organizacoes com programas de seguranca maduros que enfrentam adversarios sofisticados e ataques direcionados.

Total: 153 Safeguards distribuidos progressivamente entre os tres grupos.

### Safeguards

Cada controle contem multiplos Safeguards (anteriormente chamados Sub-Controls) que definem acoes especificas e mensuraveis. Cada Safeguard possui:

- Identificador unico (ex: 1.1, 7.4).
- Descricao da acao requerida.
- Asset type ao qual se aplica (Devices, Data, Applications, Users, Network).
- Security function associada (Identify, Protect, Detect, Respond, Recover).
- Implementation Group aplicavel (IG1, IG2 ou IG3).

## Practical Application

### Estrategia de Implementacao

1. Classificar a organizacao no Implementation Group apropriado com base em perfil de risco.
2. Realizar assessment do estado atual contra os Safeguards do IG selecionado.
3. Priorizar implementacao dos Safeguards do IG1 como fundacao de higiene cibernetica.
4. Automatizar verificacao de conformidade utilizando CIS Benchmarks e scanning tools.
5. Evoluir progressivamente para IG2 e IG3 conforme maturidade e recursos permitirem.
6. Medir progresso com porcentagem de Safeguards implementados por IG e por controle.

### Relacao com CIS Benchmarks

Os CIS Benchmarks sao guias de configuracao detalhados para tecnologias especificas que operacionalizam os controles 4 e 12. Estao disponiveis para sistemas operacionais, bancos de dados, containers, cloud platforms e dispositivos de rede.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O discovery-layer implementa os controles 1 e 2 para manter inventario atualizado de ativos e software.
- O defense-layer cobre controles 8, 10 e 13 relacionados a monitoramento, malware e defesa de rede.
- O identity-layer implementa controles 5 e 6 para gestao de contas e acesso.
- O appsec-layer cobre o controle 16 com security testing integrado no ciclo de desenvolvimento.
- O vuln-triage-playbook operacionaliza o controle 7 de Continuous Vulnerability Management.
- O ir-layer implementa o controle 17 de Incident Response Management.
- O offense-layer executa testes conforme controle 18 de Penetration Testing.
- O security-kpi-dashboard exibe cobertura de Safeguards por IG como indicador de maturidade.
- O security-champion-program contribui para o controle 14 de Security Awareness and Skills Training.
