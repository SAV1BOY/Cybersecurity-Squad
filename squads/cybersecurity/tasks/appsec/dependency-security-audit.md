# Task: Dependency Security Audit

## Objetivo
Auditar dependencias de terceiros (bibliotecas, frameworks, pacotes) quanto a vulnerabilidades conhecidas, licencas e riscos de supply chain attack.

## Agents
- **jim-manico** (lead) — Avalia risco de dependencias
- **command-generator** (support) — Gera comandos de SCA e auditoria

## Inputs
- Repositorios de codigo com manifests de dependencias
- SCA tools configurados (Snyk, Dependabot, OWASP Dependency-Check)
- CVE databases e advisory feeds

## Steps
1. Inventariar todas as dependencias diretas e transitivas
2. Executar SCA para identificar vulnerabilidades conhecidas
3. Classificar vulnerabilidades por severidade e explorabilidade
4. Avaliar dependencias abandonadas ou sem manutencao
5. Verificar integridade de pacotes (checksums, signatures)
6. Auditar licencas quanto a compliance e risco legal
7. Identificar dependencias com historico de supply chain attacks
8. Definir politica de update e patching para dependencias
9. Documentar findings com recomendacoes de remediacao
10. Registrar findings no `findings-registry`

## Output
- Inventario de dependencias com status de vulnerabilidade
- Lista de dependencias criticas para update ou substituicao
- Politica de dependency management documentada
- Registro no `findings-registry`

## Quality Gates
- [ ] Todas as dependencias (diretas e transitivas) inventariadas
- [ ] SCA executado com resultados triados
- [ ] Dependencias abandonadas identificadas e sinalizadas
- [ ] Integridade de pacotes verificada
- [ ] Licencas auditadas quanto a compliance
- [ ] Checklist `appsec-supply-chain` atendido
- [ ] Checklist `supply-chain-security-quality` validado
