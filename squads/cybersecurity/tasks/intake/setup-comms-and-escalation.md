# Task: Setup Comms & Escalation

## Objetivo
Configurar canais de comunicacao, definir escalation paths e estabelecer protocolos de notificacao para o engagement de seguranca.

## Agents
- **cyber-chief** (lead) — Define estrutura de comunicacao
- **marcus-carey** (support) — Valida protocolos de comunicacao sob pressao

## Inputs
- Documento de ROE aprovado
- Lista de stakeholders e contatos
- Politica de comunicacao da organizacao

## Steps
1. Definir canais primarios e secundarios de comunicacao (Slack, email, phone)
2. Configurar canal seguro para compartilhamento de findings criticos
3. Documentar escalation path com niveis de severidade
4. Definir SLA de resposta para cada nivel de severidade
5. Estabelecer protocolo de deconfliction com SOC/Blue Team
6. Criar lista de distribuicao para status updates
7. Definir frequencia de status reports (diario, semanal)
8. Documentar out-of-band communication procedures
9. Testar canais de comunicacao antes do inicio do engagement
10. Registrar configuracao no `decisions-log`

## Output
- Documento de communication plan
- Escalation matrix com contatos e SLAs
- Canal seguro configurado e testado
- Deconfliction protocol documentado

## Quality Gates
- [ ] Canais de comunicacao testados e funcionais
- [ ] Escalation path cobre todos os niveis de severidade
- [ ] SLA de resposta definido para Critical, High, Medium, Low
- [ ] Deconfliction process com SOC/Blue Team estabelecido
- [ ] Out-of-band procedures documentados para emergencias
- [ ] Status update frequency acordada com stakeholders
- [ ] Checklist `carey-communication-under-pressure` validado
