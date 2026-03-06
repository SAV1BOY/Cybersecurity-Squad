# Cybersecurity Squad — MMOS

> Red Team + Blue Team + AppSec + CloudSec + Incident Response
> O sistema operacional de ciberseguranca mais completo e pragmatico do MMOS.

## Visao Geral

O Cybersecurity Squad e um sistema de 15 agentes especializados que cobrem todo o ciclo de seguranca ofensiva e defensiva: desde o scoping e autorizacao ate a analise pos-incidente e metricas de maturidade. Cada agente opera com prompts HRM (Hierarchical Role Modeling) e e roteado pelo `config.yaml` para executar tasks, seguir frameworks, cumprir checklists e gerar outputs padronizados.

## Principios Operacionais

1. **authorized-only** — Nada sem autorizacao explicita e documentada
2. **evidence-first** — Tudo com prova, rastreabilidade e integridade
3. **minimize-impact** — Minimo dano, minima alteracao, minima disrupcao
4. **reproducible-results** — Resultados reproduziveis e verificaveis
5. **fix-over-fear** — Foco em consertar, nao em assustar

## Arquitetura do Squad

```
intake -> discovery -> execution -> report -> remediation -> retest -> metrics -> improvement
```

### Camadas Operacionais

| Camada | Funcao | Agentes Primarios |
|--------|--------|-------------------|
| Discovery | Ativos, fluxos, trust boundaries | Cartographer, Busterer, Dirber |
| Offense | Red Team, validacao, simulacao | Peter Kim, Georgia Weidman, Rogue, Ripper |
| Defense | Deteccao, resposta, hunting | Chris Sanders, Omar Santos, Shannon Runner |
| AppSec | SDLC, code review, APIs | Jim Manico, Fuzzer |
| CloudSec | IAM, logs, storage, network | Omar Santos |
| IR | Triage, contencao, forense | Chris Sanders, Omar Santos |
| Governance | Risco, compliance, metricas | Cyber Chief, Marcus Carey |

## Como Usar

### 1. Identifique a Task
Navegue ate `tasks/` e encontre a tarefa desejada (ex: `tasks/red-team/recon-and-enumeration.md`).

### 2. Consulte o Routing
O `config.yaml` define para cada task: quais agentes chamar, quais frameworks seguir, quais checklists aplicar e quais templates usar.

### 3. Execute com o Agente
Ative o agente usando seu prompt de ativacao (em `agents/`). O agente segue o framework, executa a task e gera output no template correto.

### 4. Aplique o Quality Gate
Passe o output pelas checklists obrigatorias (definidas em `config.yaml > quality_gates`).

### 5. Registre
Salve resultados nos registries (`data/registries/`).

## Estrutura de Diretorios

```
squads/cybersecurity/
├── agents/              # 15 agentes com prompts HRM
├── archive/             # Historico: breaches, evolucao, respostas
├── authority/           # Credibilidade e thought leadership
├── checklists/          # Quality gates por entregavel, autor e dominio
├── data/                # Pesquisa, registros e metricas
├── docs/                # Documentacao do squad
├── frameworks/          # Metodologias, padroes e frameworks internos
├── lib/                 # Componentes, padroes e utilidades reutilizaveis
├── phrases/             # Biblioteca de frases e blocos
├── projects/            # Templates de projeto
├── reference/           # Livros, standards, tools, labs, psicologia
├── scripts/             # Automacao e consistencia
├── swipe/               # Swipe files curados
├── swipe-sources/       # Fontes de swipe
├── tasks/               # Tarefas executaveis por dominio
├── templates/           # Templates de deliverables
├── voice/               # Tom, comunicacao e linguagem
├── workflows/           # Fluxos ponta-a-ponta repetiveis
├── ARCHITECTURE.md      # Mapa de interconexao
├── config.yaml          # Cerebro de roteamento
├── README.md            # Este arquivo
└── swipe.config         # Config de curadoria
```

## Agentes (15)

### Nucleo (Pessoas/Referencias)
| Agente | Especialidade |
|--------|---------------|
| Peter Kim | Red Team pragmatico; pentest com ROI |
| Georgia Weidman | Pentest hands-on; exploracao validada |
| Jim Manico | AppSec/OWASP; secure coding; SDLC seguro |
| Chris Sanders | NSM/DFIR; analise de pacotes; IR baseado em evidencia |
| Omar Santos | Blue Team; SOC/CyberOps; hardening; deteccao |
| Marcus Carey | Cultura; operacao; playbooks do mundo real |

### Especiais (Funcoes)
| Agente | Funcao |
|--------|--------|
| Cyber Chief | Orquestrador: escopo, prioridades, governanca |
| Command Generator | Gera comandos/scripts com seguranca |
| Cartographer | Mapeia superficie de ataque/defesa |
| Busterer | Descoberta/enumeracao rapida |
| Dirber | Enumeracao de conteudo web |
| Fuzzer | Fuzzing de input/protocolos/APIs |
| Ripper | Auditoria de credenciais/hashes |
| Rogue | Adversary em simulacao (red/purple) |
| Shannon Runner | Entropy & anomaly runner |

## KPIs do Squad

- **MTTD** — Mean Time to Detect
- **MTTR** — Mean Time to Respond
- **Vuln SLA Compliance** — % corrigidas dentro do SLA
- **Detection Coverage** — % tecnicas ATT&CK com deteccao
- **False Positive Rate** — Taxa de falsos positivos
- **Security Maturity Score** — Score de maturidade

## Cross-Squad Integration

- **Dev Squad**: findings -> backlog; secure coding guidelines; SDLC gates
- **Infra Squad**: hardening baselines; detection rules; cloud guardrails
- **Compliance Squad**: evidence packages; control mappings; risk register

## OPSEC

Este repositorio NAO contem:
- Segredos, credenciais ou API keys
- Exploits ativos ou payloads funcionais
- Dados sensíveis reais de clientes ou sistemas
- Wordlists ofensivas nao-sanitizadas

Tudo e sanitizado, contextualizado e orientado a referencia.

## Custo Estimado

R$ 420K/mes para operacao completa do squad de 15 agentes.

---

*Cybersecurity Squad v1.0.0 — MMOS*
