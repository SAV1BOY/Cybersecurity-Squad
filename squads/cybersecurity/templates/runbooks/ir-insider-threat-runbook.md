# IR Runbook — Insider Threat

> Runbook de resposta a ameacas internas (maliciosas ou negligentes).
> Requer coordenacao com RH e Juridico. Todas as acoes devem ser documentadas.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Insider Threat
- **Severidade Padrao Inicial:** HIGH
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Indicadores de Insider Threat

- [ ] Download massivo de dados ou documentos
- [ ] Acesso a dados fora do escopo da funcao
- [ ] Uso de dispositivos de armazenamento USB nao autorizados
- [ ] Envio de dados para email pessoal ou cloud pessoal
- [ ] Atividade fora do horario normal sem justificativa
- [ ] Tentativas de bypass de controles de seguranca
- [ ] Comportamento incomum detectado por UEBA
- [ ] Denuncia de colega ou gestor

### 2.2 Fontes de Deteccao

- DLP: [FERRAMENTA_DLP]
- UEBA: [FERRAMENTA_UEBA]
- CASB: [FERRAMENTA_CASB]
- SIEM: [REGRA_SIEM]
- Report humano via [CANAL_DE_DENUNCIA]
- [FONTE_ADICIONAL]

## 3. Triage (Triagem)

> IMPORTANTE: Manter sigilo absoluto durante a investigacao.

- [ ] Classificar tipo de insider threat:
  - [ ] Malicioso intencional (exfiltracao, sabotagem)
  - [ ] Negligente (erro, falta de treinamento)
  - [ ] Comprometido (conta tomada por atacante externo)
- [ ] Verificar se o colaborador esta em processo de desligamento
- [ ] Avaliar nivel de acesso e privilegios do colaborador
- [ ] Identificar dados ou sistemas potencialmente afetados
- [ ] Notificar RH e Juridico ANTES de qualquer acao visivel

## 4. Investigacao

> Toda investigacao deve ser conduzida com autorizacao de [CARGO_AUTORIZADOR].

### 4.1 Coleta de Evidencias

- [ ] Revisar logs de acesso do usuario: [FERRAMENTA]
- [ ] Revisar logs de DLP/CASB
- [ ] Analisar historico de downloads e uploads
- [ ] Verificar acessos a repositorios e sistemas criticos
- [ ] Revisar comunicacoes corporativas (com autorizacao legal)
- [ ] Verificar dispositivos removiveis utilizados
- [ ] Analisar atividade em cloud storage pessoal

### 4.2 Cadeia de Custodia

| Evidencia | Coletada por | Data/Hora | Hash | Armazenamento |
|-----------|-------------|-----------|------|---------------|
| [TIPO_EVIDENCIA] | [NOME] | [DATA_HORA] | [SHA256] | [LOCALIZACAO_SEGURA] |
| [TIPO_EVIDENCIA] | [NOME] | [DATA_HORA] | [SHA256] | [LOCALIZACAO_SEGURA] |

## 5. Containment (Contencao)

> Contencao deve ser coordenada com RH e Juridico.

### 5.1 Contencao Discreta (investigacao em andamento)

- [ ] Aumentar nivel de monitoramento da conta
- [ ] Restringir acessos a dados mais sensiveis (sem alertar)
- [ ] Habilitar logging detalhado adicional
- [ ] [ACAO_ADICIONAL]

### 5.2 Contencao Ativa (apos decisao com RH/Juridico)

- [ ] Revogar acessos do colaborador
- [ ] Desabilitar conta corporativa
- [ ] Bloquear acesso VPN e remoto
- [ ] Recolher equipamentos corporativos
- [ ] Revogar acessos a terceiros e parceiros
- [ ] Alterar credenciais de sistemas compartilhados

## 6. Eradication

- [ ] Remover acessos residuais
- [ ] Revogar certificados e tokens do colaborador
- [ ] Verificar e remover backdoors ou acessos alternativos
- [ ] Revisar acessos delegados ou compartilhados
- [ ] Atualizar secrets e credenciais compartilhadas

## 7. Recovery

- [ ] Redistribuir responsabilidades do colaborador
- [ ] Verificar integridade de dados e sistemas acessados
- [ ] Restaurar dados alterados ou deletados (se aplicavel)
- [ ] Monitorar sistemas previamente acessados por [PERIODO]

## 8. Post-Incident

- [ ] Postmortem (restrito a participantes autorizados)
- [ ] Revisar e reforcar controles de DLP e UEBA
- [ ] Melhorar processo de offboarding
- [ ] Revisar politica de least privilege
- [ ] Treinamento de security awareness
- [ ] Atualizar este runbook

## 9. Contatos (Restrito)

| Papel | Contato | Canal Seguro |
|-------|---------|-------------|
| CISO | [NOME] | [CANAL_SEGURO] |
| RH | [NOME] | [CANAL_SEGURO] |
| Juridico | [NOME] | [CANAL_SEGURO] |
| IR Lead | [NOME] | [CANAL_SEGURO] |

---

*Template versao 1.0 — Cybersecurity Squad*
