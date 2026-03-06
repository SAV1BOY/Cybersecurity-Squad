# Task: Cloud Guardrails Setup

## Objetivo
Implementar guardrails preventivos em ambientes cloud para impedir misconfiguracoes de seguranca, garantindo compliance automatizado e postura de seguranca consistente.

## Agents
- **omar-santos** (lead) — Implementa guardrails cloud
- **cyber-chief** (support) — Alinha com governanca e compliance

## Inputs
- Politicas de seguranca da organizacao
- Requisitos regulatorios aplicaveis
- Arquitetura multi-account/project
- Baseline de seguranca desejado

## Steps
1. Definir baseline de seguranca obrigatorio para todas as contas
2. Implementar SCPs (Service Control Policies) / Organization Policies
3. Configurar AWS Config Rules / Azure Policy / GCP Organization Policy
4. Implementar tag enforcement para governance de recursos
5. Configurar budget alerts e cost anomaly detection
6. Bloquear criacao de recursos em regioes nao autorizadas
7. Implementar preventive controls para public exposure
8. Configurar detective controls para drift detection
9. Documentar guardrails e excecoes autorizadas
10. Registrar configuracao no `decisions-log`

## Output
- Guardrails preventivos implementados em todas as contas
- Politicas de organization-level documentadas
- Detective controls para drift detection ativos
- Registro de excecoes autorizadas

## Quality Gates
- [ ] SCPs/Organization Policies implementados
- [ ] Config Rules/Azure Policy configurados e ativos
- [ ] Tag enforcement funcional em todas as contas
- [ ] Public exposure preventivamente bloqueado
- [ ] Drift detection configurado e alertando
- [ ] Excecoes documentadas e aprovadas
- [ ] Checklist `cloud-multi-account-security` atendido
