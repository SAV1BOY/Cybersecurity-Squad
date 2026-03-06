# Task: Credential Attack Testing

## Objetivo
Testar a robustez dos controles de credenciais da organizacao, incluindo politicas de senha, armazenamento de credenciais e resistencia a ataques de credential-based attacks.

## Agents
- **ripper** (lead) — Executa auditoria de credenciais
- **peter-kim** (support) — Prioriza attack paths baseados em credenciais

## Inputs
- Identity e privilege mapping
- Politicas de senha da organizacao
- Hashes coletados (com autorizacao) durante exploitation
- ROE com autorizacao explicita para credential testing

## Steps
1. Auditar politica de senhas contra best practices (NIST 800-63B)
2. Executar password spraying com lista controlada (se autorizado)
3. Testar Kerberoasting em service accounts do AD
4. Executar AS-REP roasting em contas sem pre-auth
5. Verificar credential storage (LSASS, SAM, credential managers)
6. Testar password reuse entre sistemas e servicos
7. Avaliar MFA implementation e bypass potenciais
8. Auditar secrets em repositorios de codigo e configuracoes
9. Documentar cada finding com evidencia e impacto
10. Registrar findings no `findings-registry`

## Output
- Relatorio de credential security com findings classificados
- Estatisticas de password quality (sem expor senhas reais)
- Lista de credential-based attack paths viáveis
- Recomendacoes de hardening de credenciais

## Quality Gates
- [ ] Credential testing autorizado explicitamente no ROE
- [ ] Senhas crackeadas nunca expostas em reports (apenas estatisticas)
- [ ] Password spraying com rate limiting para evitar lockout
- [ ] MFA avaliado em todas as contas privilegiadas
- [ ] Secrets em codigo/config identificados e reportados
- [ ] Checklist `kim-attack-path-prioritization` atendido
- [ ] Checklist `redteam-safe-testing-rules` validado
