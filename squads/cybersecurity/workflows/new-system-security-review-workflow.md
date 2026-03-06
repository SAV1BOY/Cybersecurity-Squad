# New System Security Review Workflow

Processo de avaliacao de seguranca para novos sistemas, aplicacoes ou servicos antes do deploy em producao.

## Objetivo

Garantir que todo novo sistema passe por uma avaliacao de seguranca adequada antes de entrar em operacao, identificando e mitigando riscos de forma proativa.

## Inputs

- Formulario de intake preenchido pelo time solicitante
- Documentacao tecnica do sistema (arquitetura, data flows)
- Classificacao de dados que o sistema processara
- Timeline planejado para go-live

## Stages

### 1. Intake e Classification

- Responsavel: **Review Intake Agent**
- Receber formulario de solicitacao de review
- Classificar o sistema por criticidade (tier 1, 2 ou 3)
- Ponto de decisao: **Classificacao de risco do sistema?**
  - Tier 1 (critico) -> review completo obrigatorio
  - Tier 2 (moderado) -> review padrao
  - Tier 3 (baixo risco) -> self-assessment com validacao

### 2. Documentation Review

- Responsavel: **Security Architect Agent**
- Revisar arquitetura e identificar componentes de risco
- Analisar data flows e classificacao de dados
- Verificar integracao com sistemas existentes

### 3. Threat Modeling

- Responsavel: **Threat Model Lead Agent**
- Conduzir threat model baseado na arquitetura
- Identificar ameacas especificas ao novo sistema
- Priorizar riscos para avaliacao detalhada

### 4. Security Requirements Validation

- Responsavel: **Security Architect Agent**
- Verificar compliance com security baseline da organizacao
- Validar autenticacao, autorizacao, encryption e logging
- Confirmar que requisitos regulatorios estao atendidos

### 5. Technical Assessment

- Responsavel: **AppSec Agent** ou **Infra Security Agent**
- Executar vulnerability scan e configuration review
- Testar controles de seguranca implementados
- Ponto de decisao: **Vulnerabilidades criticas encontradas?**
  - Sim -> bloquear deploy e exigir correcao
  - Nao -> prosseguir com findings menores

### 6. Third-Party Risk Assessment (se aplicavel)

- Responsavel: **Third Party Risk Agent**
- Avaliar postura de seguranca de vendors envolvidos
- Revisar contratos e clausulas de seguranca
- Verificar certificacoes e auditorias do vendor

### 7. Review Decision

- Responsavel: **Security Review Board**
- Consolidar findings de todas as avaliacoes
- Ponto de decisao: **Sistema aprovado para producao?**
  - Aprovado -> emitir clearance com condicoes se necessario
  - Aprovado condicional -> definir prazo para resolver condicoes
  - Bloqueado -> listar requisitos obrigatorios para re-review

### 8. Post-Launch Monitoring

- Responsavel: **Detection Engineer Agent**
- Configurar monitoramento e alertas de seguranca
- Programar vulnerability scan recorrente
- Agendar review de follow-up em 90 dias

## Decision Points

| Ponto | Condicao | Acao |
|-------|----------|------|
| Sistema processa PII | Dados pessoais envolvidos | Exigir avaliacao LGPD e DPO review |
| Sistema exposto a internet | Servico publico | Exigir pentest antes do launch |
| Vendor sem certificacao | Terceiro sem SOC 2 ou ISO 27001 | Avaliar risco e exigir mitigacoes |
| Timeline apertado | Go-live antes do review completo | Avaliar risco de launch sem review |

## Outputs

- Relatorio de security review com decisao formal
- Lista de findings e recomendacoes
- Clearance document (se aprovado)
- Plano de monitoramento pos-launch
