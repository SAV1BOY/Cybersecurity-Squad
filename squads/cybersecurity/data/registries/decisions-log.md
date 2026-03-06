# Decisions Log

Registro de decisoes tecnicas e estrategicas de seguranca, preservando contexto e racional.

## Schema do Registro

| Decision ID | Date | Title | Context | Decision | Alternatives Considered | Outcome | Decided By |
|-------------|------|-------|---------|----------|------------------------|---------|------------|
| DEC-2026-001 | 2026-01-10 | Escolha de SIEM platform | Necessidade de centralizar logs de seguranca | Adotar Elastic SIEM com stack open-source | Splunk (custo), Sentinel (lock-in), Sumo Logic (limitacoes) | Implementacao iniciada em Q1 | @ciso, @soc-lead |
| DEC-2026-002 | 2026-01-20 | Estrategia de vulnerability scanning | Cobertura insuficiente com scans manuais | Scanner automatizado semanal + DAST no CI/CD | Scan mensal manual (cobertura), SaaS only (custo) | Reducao de 40% no MTTR | @appsec-lead |
| DEC-2026-003 | 2026-02-05 | Politica de secrets management | API keys hardcoded em repositorios | HashiCorp Vault para centralizacao de secrets | AWS Secrets Manager (lock-in), dotenv (inseguro) | Migration em andamento | @devsecops-lead |

## Categorias de Decisao

- **Architecture**: Decisoes sobre arquitetura de seguranca
- **Tooling**: Selecao de ferramentas e plataformas
- **Policy**: Definicao ou alteracao de politicas
- **Process**: Mudancas em processos operacionais
- **Strategy**: Direcao estrategica do programa

## Formato de Registro

Cada decisao deve documentar:
1. **Contexto**: Problema ou necessidade que motivou a decisao
2. **Opcoes avaliadas**: Alternativas consideradas com pros/contras
3. **Decisao**: Escolha feita e justificativa principal
4. **Consequencias**: Impactos esperados e trade-offs aceitos
5. **Revisao**: Data para reavaliar a decisao se aplicavel

## Importancia

O decisions log evita re-discussoes ciclicas, preserva conhecimento institucional
e permite que novos membros entendam o historico do programa de seguranca.
Toda decisao significativa deve ser registrada dentro de 48h.
