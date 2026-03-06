# NIST 800 Series - Guia Pratico

## Objetivo
Referencia pratica das publicacoes NIST SP 800 mais relevantes para o squad,
com orientacoes de aplicacao direta em projetos e operacoes.

## Publicacoes Prioritarias

### SP 800-53 Rev. 5 - Security and Privacy Controls
- **O que e**: catalogo abrangente de controles de seguranca e privacidade
- **Quando usar**: design de programas, gap analysis, compliance mapping
- **Familias-chave**: AC (Access Control), AU (Audit), IR (Incident Response),
  RA (Risk Assessment), SC (System/Comms Protection), SI (System/Info Integrity)
- **Dica pratica**: usar o control overlay approach para selecionar controles
  relevantes ao contexto especifico

### SP 800-61 Rev. 2 - Incident Handling Guide
- **O que e**: guia para preparacao, deteccao, analise, contencao e recuperacao
- **Quando usar**: construir programa de IR, criar playbooks
- **Fases**: Preparation, Detection & Analysis, Containment/Eradication/Recovery,
  Post-Incident Activity
- **Dica pratica**: usar como checklist durante incidentes reais

### SP 800-115 - Technical Guide to Security Testing
- **O que e**: guia tecnico para testes de seguranca
- **Quando usar**: planejar pentests, vulnerability assessments
- **Cobertura**: review techniques, target identification, vulnerability analysis,
  planning e execution
- **Dica pratica**: usar como base para metodologia de pentest

### SP 800-171 Rev. 3 - Protecting CUI
- **O que e**: requisitos para protecao de informacao controlada
- **Quando usar**: contratos governamentais, dados sensiveis
- **Familias**: 14 familias de controles derivadas do SP 800-53
- **Dica pratica**: mapear para requisitos LGPD quando aplicavel

### SP 800-86 - Forensic Techniques
- **O que e**: guia para integracao de tecnicas forenses em IR
- **Quando usar**: coleta de evidencias, analise forense
- **Dica pratica**: seguir procedimentos de chain of custody

### SP 800-63 - Digital Identity Guidelines
- **O que e**: framework para identidade digital e autenticacao
- **Quando usar**: design de sistemas de autenticacao
- **Dica pratica**: referencia para requisitos de MFA

## Aplicacao Pratica no Squad
1. Selecionar publicacoes relevantes ao escopo do projeto
2. Extrair controles aplicaveis ao contexto
3. Mapear para frameworks complementares (ISO, CIS)
4. Documentar gaps e recomendacoes priorizadas
5. Acompanhar implementacao com metricas

## Notas do Squad
Manter versoes atualizadas das publicacoes. NIST atualiza frequentemente
e mudancas podem impactar avaliacoes em andamento.
