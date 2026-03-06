# IR Runbook — Data Breach

> Runbook de resposta a incidentes de vazamento ou violacao de dados.
> Envolve requisitos regulatorios (LGPD) e comunicacao obrigatoria.

---

## 1. Informacoes do Runbook

- **Tipo de Incidente:** Data Breach / Data Leak
- **Severidade Padrao Inicial:** CRITICAL
- **Owner:** [NOME_DO_RESPONSAVEL]
- **Ultima Revisao:** [DATA]
- **Aprovado por:** [NOME_DO_APROVADOR]

## 2. Detection (Deteccao)

### 2.1 Indicadores de Data Breach

- [ ] Alerta de DLP (Data Loss Prevention)
- [ ] Dados da organizacao encontrados externamente
- [ ] Exfiltracao detectada via network monitoring
- [ ] Acesso massivo a dados sensiveis
- [ ] Report de terceiro sobre dados expostos
- [ ] Alerta de cloud storage publico
- [ ] [INDICADOR_ADICIONAL]

### 2.2 Fontes de Deteccao

- DLP: [FERRAMENTA_DLP]
- CASB: [FERRAMENTA_CASB]
- SIEM: [REGRA_SIEM]
- Dark web monitoring: [FERRAMENTA]
- [FONTE_ADICIONAL]

## 3. Triage (Triagem)

- [ ] Confirmar que dados reais foram comprometidos (nao dados de teste)
- [ ] Identificar tipo de dados: [PII / FINANCEIRO / SAUDE / CREDENCIAIS / IP]
- [ ] Estimar volume de registros afetados
- [ ] Identificar titulares dos dados afetados
- [ ] Determinar se dados estao publicamente acessiveis
- [ ] Verificar se a exfiltracao ainda esta em andamento
- [ ] Classificar conforme LGPD: [INCIDENTE_DE_SEGURANCA_COM_DADOS_PESSOAIS]

## 4. Containment (Contencao)

### 4.1 Acoes Imediatas

- [ ] Interromper exfiltracao ativa (bloquear canal)
- [ ] Revogar acessos da fonte do vazamento
- [ ] Remover dados de locais publicos (takedown request)
- [ ] Isolar sistemas comprometidos
- [ ] Preservar evidencias antes de qualquer alteracao

### 4.2 Se Dados em Repositorio Publico

- [ ] Solicitar takedown na plataforma (GitHub, Pastebin, etc.)
- [ ] Rotacionar credenciais expostas
- [ ] Limpar historico de commits se aplicavel

### 4.3 Se Dados em Dark Web / Forums

- [ ] Documentar evidencia (screenshots com timestamp)
- [ ] Avaliar autenticidade dos dados
- [ ] Monitorar evolucao da publicacao
- [ ] Contactar [EMPRESA_THREAT_INTEL] para monitoramento

## 5. Investigation (Investigacao)

- [ ] Determinar causa raiz do vazamento
- [ ] Identificar todos os dados comprometidos (inventario completo)
- [ ] Mapear timeline da exfiltracao
- [ ] Identificar threat actor (se aplicavel)
- [ ] Verificar se houve acesso por terceiros nao autorizados
- [ ] Avaliar impacto regulatorio (LGPD Art. 48)

## 6. Notificacoes Obrigatorias (LGPD)

### 6.1 ANPD (Autoridade Nacional de Protecao de Dados)

- **Prazo:** [PRAZO_CONFORME_REGULAMENTACAO]
- **Responsavel:** [DPO_NOME]
- **Informacoes a comunicar:**
  - Descricao da natureza dos dados pessoais afetados
  - Titulares envolvidos
  - Medidas tecnicas e de seguranca utilizadas
  - Riscos relacionados ao incidente
  - Medidas adotadas para reverter ou mitigar

### 6.2 Titulares dos Dados

- **Prazo:** [PRAZO]
- **Canal de comunicacao:** [EMAIL / SITE / CARTA]
- **Template de comunicacao:** [REFERENCIA_AO_TEMPLATE_DE_COMUNICACAO]

## 7. Recovery (Recuperacao)

- [ ] Corrigir causa raiz
- [ ] Implementar controles adicionais de DLP
- [ ] Monitorar dados comprometidos em dark web
- [ ] Oferecer suporte aos titulares afetados: [MEDIDAS_DE_SUPORTE]
- [ ] Restaurar servicos afetados
- [ ] [ACAO_ADICIONAL]

## 8. Post-Incident

- [ ] Postmortem detalhado
- [ ] Revisao de politicas de classificacao de dados
- [ ] Revisao de controles de acesso a dados sensiveis
- [ ] Treinamento de conscientizacao
- [ ] Relatorio para board / diretoria
- [ ] Atualizacao de controles e este runbook

## 9. Contatos

| Papel | Nome | Canal |
|-------|------|-------|
| Incident Commander | [NOME] | [CANAL] |
| DPO | [NOME] | [CANAL] |
| Juridico | [NOME] | [CANAL] |
| CISO | [NOME] | [CANAL] |
| Comunicacao | [NOME] | [CANAL] |

---

*Template versao 1.0 — Cybersecurity Squad*
