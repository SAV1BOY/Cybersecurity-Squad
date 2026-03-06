# Phishing Simulation Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a campanhas de phishing ETICO e AUTORIZADO.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia para planejamento e execucao de campanhas de phishing simulado com
objetivo de avaliar a resiliencia humana da organizacao. Foca em metricas objetivas,
feedback educativo e melhoria continua da conscientizacao em seguranca.

## Requisitos de Autorizacao
- Aprovacao formal da diretoria e do departamento juridico
- Alinhamento com RH sobre tratamento dos resultados (nao punitivo)
- Definicao de escopo: departamentos, niveis hierarquicos, periodo
- Politica de privacidade para tratamento de dados dos participantes
- Plano de comunicacao pos-campanha aprovado pela lideranca

## Etapas da Metodologia

### 1. Planejamento da Campanha
- Definicao de objetivos: taxa de click, taxa de report, awareness
- Selecao de pretextos alinhados com ameacas reais ao setor
- Criacao de templates de email com niveis de dificuldade variados
- Configuracao de infraestrutura: dominios, landing pages, tracking

### 2. Reconhecimento Controlado
- Coleta de informacoes publicas sobre a organizacao (OSINT autorizado)
- Identificacao de padroes de comunicacao interna
- Mapeamento de servicos utilizados para criacao de pretextos criveis
- Personalizacao de templates por departamento quando aplicavel

### 3. Preparacao Tecnica
- Registro de dominios similares (typosquatting controlado)
- Configuracao de SPF/DKIM/DMARC para entrega confiavel
- Implementacao de landing pages com formularios de captura
- Setup de tracking de abertura, click e submissao de credenciais
- Garantia de que credenciais capturadas nao sao armazenadas

### 4. Execucao da Campanha
- Envio escalonado para evitar sobrecarga de alertas
- Monitoramento em tempo real de metricas de engajamento
- Prontidao para interromper campanha se necessario
- Registro de usuarios que reportaram o phishing ao SOC

### 5. Metricas e Analise
- Taxa de abertura de email (open rate)
- Taxa de click em links maliciosos (click-through rate)
- Taxa de submissao de credenciais (compromise rate)
- Taxa de report ao SOC ou equipe de seguranca (report rate)
- Tempo medio entre recebimento e report (mean time to report)
- Segmentacao de resultados por departamento e senioridade

### 6. Feedback e Treinamento
- Pagina de feedback imediato apos click (momento educativo)
- Sessoes de treinamento direcionado para grupos de maior risco
- Comunicacao positiva destacando usuarios que reportaram corretamente
- Comparacao com campanhas anteriores para medir evolucao

## Ferramentas de Referencia
- GoPhish, King Phisher, Evilginx (demonstracao controlada apenas)
- Plataformas comerciais: KnowBe4, Proofpoint Security Awareness

## Contrapartida de Deteccao (Blue Team)
- Validacao de eficacia de email gateway e filtros anti-phishing
- Teste de deteccao de dominios typosquatted pelo DNS security
- Avaliacao do processo de report de phishing pelos usuarios
- Medicao de tempo de resposta do SOC a reports de phishing

## Integracao com Outros Frameworks
- Correlaciona com: credential-attack-methodology.md (credenciais expostas)
- Correlaciona com: exfiltration-detection-methodology.md (vetor email)
- Alimenta: programa de security awareness e metricas de risco humano
- Reporta para: dashboard de KPIs de seguranca corporativa
