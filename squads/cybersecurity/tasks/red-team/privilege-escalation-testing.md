# Task: Privilege Escalation Testing

## Objetivo
Testar caminhos de privilege escalation a partir de acessos obtidos, identificando como um atacante poderia elevar privilegios de usuario comum para admin/root/domain admin.

## Agents
- **georgia-weidman** (lead) — Executa testes de privilege escalation
- **rogue** (support) — Simula tecnicas adversarias de escalacao

## Inputs
- Acessos obtidos durante exploitation
- Identity e privilege mapping
- Configuracoes de sistema e policies (GPOs, sudoers, IAM)

## Steps
1. Enumerar privilegios atuais do acesso obtido
2. Identificar misconfigurations de sistema (SUID, weak permissions)
3. Verificar kernel e software vulnerabilities para local privesc
4. Testar AD misconfigurations (Kerberoasting, delegation abuse, GPO)
5. Verificar unquoted service paths e weak service permissions
6. Testar token impersonation e session hijacking
7. Avaliar cloud IAM misconfigurations para privilege escalation
8. Documentar cada path de escalacao com PoC reproduzivel
9. Classificar impacto de cada privilege escalation path
10. Registrar findings no `findings-registry`

## Output
- Lista de privilege escalation paths confirmados com PoC
- Classificacao de impacto por path (local admin, domain admin, root)
- Recomendacoes de hardening para cada path
- Evidencias hasheadas (SHA-256)

## Quality Gates
- [ ] Testes limitados ao escopo autorizado no ROE
- [ ] Cada path tem PoC reproduzivel documentado
- [ ] Impacto classificado por nivel de privilegio obtido
- [ ] Nenhuma persistencia instalada sem autorizacao
- [ ] Cleanup executado apos cada teste
- [ ] Checklist `weidman-privilege-escalation-audit` atendido
- [ ] Checklist `redteam-safe-testing-rules` validado

## Routing (config.yaml)

| Campo | Valor |
|-------|-------|
| Frameworks | privilege-escalation-methodology |
| Checklists | weidman/weidman-privilege-escalation-audit, red-team/redteam-safe-testing-rules |
| Templates | reports/finding-template |
| Registry | data/registries/findings-registry |

## Escalation & Handoff
- Se blocked > 4h: escalar para cyber-chief
- Se quality gate < 80%: rework loop (ver `docs/rework-loop-protocol.md`)
- Se fora do escopo: halt e notificar cyber-chief (ver `docs/delegation-protocol.md`)
- **Receives from**: vuln-validation
- **Delivers to**: report-findings
