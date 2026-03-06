# IR Layer — Framework Operacional

> Camada de resposta a incidentes: triage, contencao, erradicacao, recuperacao e melhoria.

## Objetivo

A IR Layer garante resposta estruturada, rapida e baseada em evidencias a incidentes de seguranca. O objetivo nao e apenas "apagar o fogo" — e entender o que aconteceu, conter o dano, erradicar a ameaca, recuperar operacoes e garantir que o mesmo incidente nao se repita.

## Principios

1. **Preparacao e 90% do sucesso** — Playbooks, contatos e ferramentas prontos ANTES do incidente
2. **Evidencia antes de acao** — Coletar evidencia antes de conter (quando possivel)
3. **Contencao reversivel** — Preferir acoes que podem ser desfeitas
4. **Comunicacao clara e cadenciada** — Stakeholders informados no tempo certo
5. **Scope antes de fix** — Entender a extensao antes de remediar
6. **Blameless por design** — Foco em sistema, nao em pessoa
7. **Cada incidente melhora a defesa** — Postmortem com acoes concretas

## Ciclo de Vida do Incidente (NIST 800-61)

### Fase 1: Preparacao
```
Antes do incidente:
- Playbooks documentados para cenarios comuns
- Contatos de escalonamento atualizados
- Ferramentas de coleta forense prontas
- Canais de comunicacao definidos (war room, bridge)
- Exercicios tabletop regulares (minimo trimestral)
- Backups verificados e restauraveis
- Runbooks testados e versionados
```

### Fase 2: Detection & Analysis
```
Ao detectar sinal:
1. TRIAGE (15 min): O que aconteceu? Qual o impacto potencial?
2. SCOPE: Quantos sistemas/usuarios afetados?
3. SEVERITY: P1/P2/P3/P4 baseado em impacto e urgencia
4. TIMELINE: Construir timeline de eventos (com gaps identificados)
5. EVIDENCE: Coletar logs, memoria, disco (integridade com hash)
6. HIPOTESE: Formular hipotese sobre vetor e extensao
7. ESCALAR: Conforme severidade e matriz de escalonamento
```

### Severidade

| Nivel | Descricao | SLA Response | Exemplos |
|-------|-----------|--------------|----------|
| P1 — Critico | Impacto massivo, dados sensiveis, sistemas criticos | 30 min | Ransomware, data breach, account takeover privilegiado |
| P2 — Alto | Impacto significativo, risco de escalacao | 2h | Malware detectado, credentials comprometidas |
| P3 — Medio | Impacto limitado, contido | 8h | Phishing bem-sucedido sem lateral movement |
| P4 — Baixo | Evento suspeito, sem impacto confirmado | 24h | Alerta de policy violation |

### Fase 3: Containment
```
Contencao curto prazo (imediata):
- Isolar host(s) afetado(s) (network isolation)
- Desabilitar conta(s) comprometida(s)
- Bloquear IP/dominio malicioso
- Revogar tokens/sessions comprometidos

Contencao longo prazo:
- Aplicar patches emergenciais
- Hardening adicional em sistemas afetados
- Monitoring reforçado no perimetro do incidente
```

### Fase 4: Eradication & Recovery
```
Erradicacao:
- Remover malware/backdoors
- Revogar e rotacionar TODAS as credentials potencialmente afetadas
- Identificar e remover persistencia
- Verificar integridade de sistemas

Recuperacao:
- Restaurar de backup limpo (se necessario)
- Re-deploy de sistemas comprometidos
- Monitorar sinais de re-compromisso (30 dias)
- Validar que servicos estao operacionais
```

### Fase 5: Post-Incident Activity
```
Postmortem (ate 5 dias uteis apos resolucao):
1. Timeline completa (sem gaps)
2. Root cause analysis (5 Whys ou Ishikawa)
3. O que funcionou bem
4. O que precisa melhorar
5. Acoes concretas com owners e prazos
6. Melhorias em deteccao, playbooks, processos
7. Comunicacao de lições aprendidas
```

## Comunicacao em Incidente

| Quando | Para Quem | O Que |
|--------|-----------|-------|
| T+30min (P1) | Lideranca tecnica | Situacao inicial, ações em curso |
| T+2h (P1) | Lideranca executiva | Impacto, contencao, proximo update |
| T+4h (P1) | Legal/compliance (se dados) | Obrigacoes regulatorias |
| Resolucao | Todos stakeholders | Resolucao, impacto final, next steps |
| T+5d | Time + lideranca | Postmortem completo |

## Agentes Envolvidos

| Agente | Papel na IR Layer |
|--------|------------------|
| Chris Sanders | Evidence collection, timeline, packet analysis, hunting |
| Omar Santos | Containment, hardening, SOC coordination |
| Shannon Runner | Anomaly detection, IOC enrichment |
| Marcus Carey | Communication, postmortem facilitation, lessons learned |
| Cyber Chief | Severity decisions, escalation, resource allocation |

## Outputs

- Incident report (timeline + RCA + actions)
- Evidence package (hashed, chain of custody)
- Postmortem document
- Detection improvements
- Updated playbooks
- Communication log

## Quality Gates

- `incident-triage-quality.md`
- `incident-response/ir-containment-checklist.md`
- `forensics-collection-quality.md`
- `evidence-chain-quality.md`
