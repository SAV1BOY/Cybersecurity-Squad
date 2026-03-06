# Offense Layer — Framework Operacional

> Camada ofensiva: validar vulnerabilidades, simular ataques reais e provar impacto — sempre dentro de limites autorizados.

## Objetivo

A Offense Layer valida se as defesas funcionam testando-as como um adversario real faria. Diferente de vulnerability scanning (automatizado e superficial), esta camada envolve pensamento adversarial, encadeamento de tecnicas e validacao manual de impacto. Todo achado deve ter prova reproduzivel.

## Principios

1. **ROE e sagrado** — Rules of Engagement definem limites absolutos
2. **Stop rules existem por uma razao** — Parar imediatamente quando atingir limites
3. **Impacto minimo** — Testar sem causar dano, sem persistencia nao-autorizada
4. **Prova > suposicao** — Se nao tem evidencia, nao e finding
5. **Hipotese antes de exploit** — Formular hipotese, validar com menor esforco possivel
6. **Reproduzibilidade** — Outro operador deve conseguir repetir o teste
7. **Report e tao importante quanto o teste** — Finding sem relatorio claro nao gera fix

## Metodologia de Ataque

### Fase 1: Reconnaissance (Discovery Layer)
- Receber mapa de superficie do Cartographer
- Identificar alvos de maior impacto potencial
- Priorizar: internet-facing > interno, critico > low-impact

### Fase 2: Vulnerability Identification
- Scanning automatizado (complementar, nao substituto)
- Analise manual de servicos, configs, codigo
- Correlacao: CVE + contexto + exposicao = risco real
- **Pergunta-chave**: "Isso e exploravel no contexto deste ambiente?"

### Fase 3: Exploitation Validation
- Formular hipotese de ataque
- Validar com PoC minimo (sem escalar alem do necessario)
- Capturar evidencia: screenshots, logs, comandos, outputs
- Documentar cada passo (reproduzibilidade)
- **Stop rule**: Parar se atingir dados sensíveis reais ou sair do escopo

### Fase 4: Post-Exploitation Assessment
- Avaliar impacto real (o que um atacante conseguiria a partir daqui?)
- Mapear caminhos de lateral movement (sem executar, apenas mapear)
- Identificar dados acessiveis e privilegios obtidos
- **Cleanup obrigatorio**: Reverter qualquer alteracao feita

### Fase 5: Attack Path Analysis
- Encadear achados em attack paths completos
- Classificar por: impacto de negocio x probabilidade x esforco
- Identificar "choke points" onde um fix bloqueia multiplos caminhos
- Priorizar recomendacoes por ROI de remediacao

## Frameworks de Referencia

| Framework | Uso na Offense Layer |
|-----------|---------------------|
| MITRE ATT&CK | Mapeamento de tecnicas usadas e cobertura |
| Kill Chain | Estruturar fases do ataque simulado |
| PTES | Metodologia ponta-a-ponta de pentest |
| OSSTMM | Metricas e rigor cientifico |

## Risk Scoring

Cada finding usa o modelo: `Impacto x Probabilidade x Detectabilidade x Esforco`

- **Impacto**: Dano potencial ao negocio (Critical/High/Medium/Low)
- **Probabilidade**: Chance de exploracao real (nao teorica)
- **Detectabilidade**: Defesas atuais detectariam? (inversamente proporcional)
- **Esforco**: Complexidade para o atacante (skill + tempo + recursos)

## Agentes Envolvidos

| Agente | Papel na Offense Layer |
|--------|----------------------|
| Peter Kim | Estrategia, recon, attack paths, reporting |
| Georgia Weidman | Exploitation validation, priv esc, post-exploit safety |
| Rogue | Adversary simulation, hipoteses criativas, purple team |
| Ripper | Credential attacks (autorizado) |
| Fuzzer | Input/protocol fuzzing para descoberta de vulns |
| Busterer | Enumeracao rapida, brute-force |
| Dirber | Web content discovery |

## Regras de Seguranca Operacional

1. **Nunca** executar exploits destrutivos (wipe, ransomware, fork bomb)
2. **Nunca** exfiltrar dados reais — apenas provar acesso
3. **Nunca** instalar backdoors persistentes sem autorizacao explicita
4. **Sempre** ter canal de comunicacao com o Blue Team (deconfliction)
5. **Sempre** manter log completo de todas as acoes
6. **Sempre** fazer cleanup ao final de cada sessao

## Outputs

- Findings com prova de conceito (finding-template)
- Relatorio tecnico (technical-report-template)
- Resumo executivo (executive-summary-template)
- Attack path analysis
- Recomendacoes priorizadas por ROI

## Quality Gates

- `pentest-execution-quality.md`
- `red-team/redteam-safe-testing-rules.md`
- `evidence-chain-quality.md`
- `security-report-quality.md`
