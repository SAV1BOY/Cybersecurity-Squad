# Red Team Maturity Model — Framework Interno

> Modelo de maturidade para operacoes ofensivas: de ad-hoc a otimizado.

## Niveis de Maturidade

### Level 1: Ad-hoc
- Pentest esporadico, sem metodologia fixa
- Ferramentas basicas (Nmap, Burp)
- Report com lista de vulns sem contexto
- Sem reteste sistematico
- Sem metricas

### Level 2: Repeatable
- Metodologia documentada (PTES-based)
- Playbooks para cenarios comuns
- Findings estruturados (finding-structure-standard)
- Reteste apos correcao
- Metricas basicas (vulns encontradas, severity distribution)

### Level 3: Defined
- Red Team com objetivos de negocio (nao apenas "encontrar vulns")
- Attack path analysis (cadeia de ataque, nao vulns isoladas)
- Purple team exercises (loop com Blue Team)
- Cobertura ATT&CK mapeada
- Metricas de efetividade (coverage, detection rate)

### Level 4: Managed
- Adversary simulation baseada em threat intelligence
- TTPs customizados por threat actor relevante
- Metricas avancadas: dwell time, detection evasion rate
- Continuous red teaming (nao apenas engajamentos pontuais)
- Red team tooling customizado

### Level 5: Optimized
- Red Team como servico interno contínuo
- Automacao de TTPs para regressao
- Breach & Attack Simulation (BAS) integrado ao CI/CD
- Feedback loop automatizado: Red finding -> Blue detection -> Validate
- Benchmarking contra threat actors reais
- Contribuicao para threat intelligence da industria

## Assessment

Para cada nivel, avaliar:
1. **Pessoas**: Skills, treinamento, certificacoes
2. **Processos**: Metodologia, playbooks, cadencia
3. **Tecnologia**: Ferramentas, automacao, infra de lab
4. **Metricas**: O que e medido e como e usado
5. **Integracao**: Como se conecta com Blue Team e dev teams

## Roadmap de Evolucao

```
Level 1 -> 2: Documentar metodologia, criar playbooks, estruturar findings
Level 2 -> 3: Adicionar attack paths, iniciar purple team, mapear ATT&CK
Level 3 -> 4: Customizar TTPs por intel, continuous testing, tooling avancado
Level 4 -> 5: Automacao, BAS, feedback loop, benchmarking
```

## Agentes Envolvidos

- **Peter Kim**: Avaliacao e evolucao da maturidade ofensiva
- **Georgia Weidman**: Qualidade tecnica e reproduzibilidade
- **Rogue**: Adversary simulation e criatividade
- **Cyber Chief**: Estrategia e investimento
