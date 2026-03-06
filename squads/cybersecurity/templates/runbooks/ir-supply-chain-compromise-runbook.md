# IR Runbook — Supply Chain Compromise

> Runbook de resposta a comprometimento de cadeia de suprimentos.
> Inclui dependencias de software, servicos de terceiros e fornecedores.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Supply Chain Compromise
- **Severidade Padrao Inicial:** CRITICAL
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Indicadores de Supply Chain Compromise

- [ ] Alerta de vulnerabilidade critica em dependencia (CVE)
- [ ] Pacote malicioso detectado em repositorio (npm, PyPI, Maven)
- [ ] Comportamento anomalo de software de terceiro
- [ ] Notificacao do fornecedor sobre comprometimento
- [ ] Advisory publico sobre supply chain attack
- [ ] Alerta de SCA (Software Composition Analysis)
- [ ] Assinatura digital invalida em update de software
- [ ] [INDICADOR_ADICIONAL]

### 2.2 Fontes de Deteccao

- SCA tool: [FERRAMENTA_SCA]
- Dependency scanning: [DEPENDABOT / SNYK / RENOVATE]
- Threat intelligence: [FONTE_TI]
- Advisory feeds: [NVD / GITHUB_ADVISORIES / VENDOR]
- [FONTE_ADICIONAL]

## 3. Triage (Triagem)

- [ ] Identificar componente comprometido: [NOME_VERSAO]
- [ ] Determinar tipo de comprometimento:
  - [ ] Dependencia direta com vulnerabilidade critica
  - [ ] Pacote malicioso (typosquatting, takeover)
  - [ ] Update legltimo contaminado
  - [ ] Comprometimento de build/CI pipeline do fornecedor
  - [ ] Credenciais do fornecedor comprometidas
- [ ] Verificar se o componente esta em uso na organizacao
- [ ] Listar todos os sistemas e aplicacoes que utilizam o componente
- [ ] Determinar versoes afetadas vs. versoes seguras
- [ ] Avaliar se o comprometimento foi explorado em nosso ambiente

## 4. Containment (Contencao)

### 4.1 Acoes Imediatas

- [ ] Bloquear download de versoes comprometidas no artifact registry
- [ ] Isolar sistemas que executam a versao comprometida
- [ ] Bloquear IOCs associados (C2, dominios, IPs)
- [ ] Pausar pipelines de CI/CD que utilizam o componente
- [ ] Desabilitar integracoes com fornecedor comprometido (se aplicavel)

### 4.2 Avaliacao de Impacto

- [ ] Verificar logs de execucao do componente comprometido
- [ ] Verificar se houve comunicacao com C2
- [ ] Verificar se credenciais ou dados foram exfiltrados
- [ ] Verificar se malware se propagou para outros componentes
- [ ] Avaliar impacto em clientes (se produto afetado)

## 5. Investigation (Investigacao)

- [ ] Mapear SBOM (Software Bill of Materials) completo
- [ ] Identificar todas as instancias do componente (diretas e transitivas)
- [ ] Analisar diff entre versao limpa e comprometida
- [ ] Verificar integridade de outros componentes do mesmo fornecedor
- [ ] Analisar artefatos de build para sinais de tampering
- [ ] Correlacionar com advisories e threat intelligence

## 6. Eradication (Erradicacao)

- [ ] Atualizar para versao segura do componente
- [ ] Se nao ha versao segura: remover componente e encontrar alternativa
- [ ] Rebuild de todas as aplicacoes afetadas com dependencias limpas
- [ ] Verificar integridade dos artefatos de build
- [ ] Remover qualquer persistence deixada pelo componente malicioso
- [ ] Rotacionar credenciais acessiveis pelo componente comprometido
- [ ] [ACAO_ADICIONAL]

## 7. Recovery (Recuperacao)

- [ ] Deploy de versoes corrigidas em todos os ambientes
- [ ] Validar funcionamento das aplicacoes pos-correcao
- [ ] Reativar pipelines de CI/CD com componentes atualizados
- [ ] Monitorar aplicacoes para comportamento anomalo
- [ ] Comunicar clientes se produto afetado: [TEMPLATE_COMUNICACAO]
- [ ] [ACAO_ADICIONAL]

## 8. Post-Incident

- [ ] Postmortem detalhado
- [ ] Implementar/melhorar SCA e dependency scanning
- [ ] Criar/atualizar SBOM de todas as aplicacoes
- [ ] Revisar politica de gerenciamento de terceiros
- [ ] Implementar verificacao de integridade (checksum, signature)
- [ ] Considerar dependency pinning e lockfiles
- [ ] Revisar e restringir permissoes de CI/CD
- [ ] Atualizar este runbook

## 9. Contatos

| Papel | Contato | Canal |
|-------|---------|-------|
| IR Lead | [NOME] | [CANAL] |
| AppSec Team | [NOME] | [CANAL] |
| DevOps / Platform | [NOME] | [CANAL] |
| Fornecedor | [CONTATO_VENDOR] | [CANAL] |
| CISO | [NOME] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
