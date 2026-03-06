# Zero Trust Architecture

## Overview

Zero Trust Architecture (ZTA) e um paradigma de seguranca que elimina a confianca implicita em qualquer elemento, no ou servico, exigindo verificacao continua de cada request independentemente da origem. O principio fundamental "never trust, always verify" substitui o modelo tradicional de perimetro de rede onde tudo dentro do firewall era considerado confiavel. Formalizado pelo NIST SP 800-207, o modelo ZTA responde a realidade de ambientes hibridos, trabalho remoto e ameacas internas que tornaram o perimetro tradicional insuficiente.

## Core Concepts

### Principios Fundamentais

#### Never Trust, Always Verify

Toda requisicao de acesso deve ser autenticada, autorizada e criptografada independentemente da localizacao de rede do solicitante. Nenhuma conexao herda confianca de conexoes anteriores ou posicao na rede.

#### Least Privilege Access

Acesso concedido com o minimo de privilegios necessarios para a tarefa, com escopo limitado em tempo e abrangencia. Just-in-Time (JIT) e Just-Enough-Access (JEA) sao padroes implementados.

#### Assume Breach

O design do sistema assume que comprometimento ja ocorreu ou e iminente. Controles sao projetados para limitar blast radius, prevenir movimentacao lateral e detectar comportamento anomalo continuamente.

### Componentes Arquiteturais (NIST SP 800-207)

#### Policy Engine (PE)

Componente que toma decisoes de acesso baseado em politicas organizacionais:

- Avalia identidade, contexto, postura do dispositivo e risk score.
- Consulta fontes externas de threat intelligence e compliance.
- Emite decisoes de permitir, negar ou requerer autenticacao adicional.

#### Policy Administrator (PA)

Componente que executa as decisoes do Policy Engine:

- Estabelece ou encerra sessoes de comunicacao entre sujeito e recurso.
- Configura dinamicamente data plane components (proxies, gateways, firewalls).
- Gera tokens de sessao e credenciais temporarias.

#### Policy Enforcement Point (PEP)

Componente que aplica controles no caminho de comunicacao:

- Intercepta todas as requisicoes entre sujeitos e recursos.
- Valida tokens e credenciais emitidos pelo Policy Administrator.
- Encerra sessoes quando politicas sao violadas ou expiram.

### Pilares de Zero Trust

| Pilar | Descricao | Tecnologias |
|-------|-----------|-------------|
| Identity | Verificacao forte de identidade para todos os usuarios e servicos | MFA, SSO, Identity Governance, PAM |
| Device | Validacao de postura e saude de dispositivos | EDR, MDM, Device Trust, Compliance Checks |
| Network | Microsegmentacao e criptografia de comunicacoes | Software-Defined Perimeter, mTLS, ZTNA |
| Application | Acesso granular a aplicacoes sem VPN | ZTNA, Application Proxy, API Gateway |
| Data | Protecao centrada nos dados em todo o ciclo de vida | Classification, DLP, Encryption, RBAC |
| Visibility | Monitoramento continuo e analytics de seguranca | SIEM, UEBA, XDR, Continuous Monitoring |

## Practical Application

### Jornada de Implementacao

1. **Identificar ativos e fluxos criticos** — Mapear dados, aplicacoes e servicos protegidos.
2. **Mapear fluxos de transacao** — Documentar como sujeitos acessam recursos e dependencias.
3. **Arquitetar rede Zero Trust** — Implementar microsegmentacao e eliminar confianca implicita.
4. **Criar politicas de acesso** — Definir regras granulares baseadas em identidade, contexto e risco.
5. **Monitorar e manter** — Implementar visibilidade continua e ajustar politicas baseado em analytics.

### Modelo de Maturidade ZTA

| Nivel | Estagio | Caracteristicas |
|-------|---------|-----------------|
| 1 | Traditional | Perimetro de rede, VPN, confianca implicita na LAN |
| 2 | Advanced | MFA implementado, segmentacao parcial, logging centralizado |
| 3 | Optimal | Microsegmentacao completa, ZTNA, continuous verification |
| 4 | Strategic | Risk-based adaptive access, AI-driven analytics, full automation |

### Quick Wins para Inicio

- Implementar MFA para todos os usuarios e acessos administrativos.
- Eliminar VPN para acesso a aplicacoes SaaS e migrar para ZTNA.
- Implementar device compliance checks antes de conceder acesso.
- Criptografar todo trafego interno com mTLS entre servicos.
- Centralizar logs de autenticacao e acesso para analytics.

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O identity-layer implementa os pilares Identity e Device do modelo Zero Trust.
- O defense-layer cobre os pilares Network e Visibility com microsegmentacao e monitoramento.
- O cloudsec-layer aplica principios ZTA em ambientes multi-cloud com ZTNA e identity federation.
- O governance-layer define politicas de acesso que alimentam o Policy Engine.
- O risk-scoring-model fornece risk scores dinamicos que influenciam decisoes do Policy Engine.
- O detection-coverage-matrix monitora tentativas de movimentacao lateral como validacao do assume breach.
- O security-kpi-dashboard rastreia indicadores de maturidade ZTA por pilar.
- O nist-800-53-controls mapeia controles especificos que operacionalizam cada componente ZTA.
- O purple-team-method valida eficacia da microsegmentacao com simulacoes de lateral movement.
