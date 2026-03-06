# Task: Cloud Logging Setup

## Objetivo
Configurar e validar logging abrangente em ambientes cloud, garantindo visibilidade para deteccao de ameacas, investigacao de incidentes e compliance.

## Agents
- **omar-santos** (lead) — Configura logging em cloud
- **chris-sanders** (support) — Valida adequacao para deteccao e investigacao

## Inputs
- Arquitetura de cloud (multi-account/project structure)
- Requisitos regulatorios de retencao de logs
- Detection coverage matrix
- Politica de logging existente

## Steps
1. Mapear fontes de log disponiveis por cloud provider
2. Habilitar CloudTrail/Activity Log/Audit Log em todas as contas
3. Configurar VPC Flow Logs / NSG Flow Logs
4. Habilitar logging de servicos criticos (IAM, storage, compute)
5. Centralizar logs em SIEM ou log aggregation platform
6. Definir retencao de logs conforme requisitos regulatorios
7. Configurar alertas para eventos de seguranca criticos
8. Validar que logs capturam informacoes suficientes para investigacao
9. Testar pipeline de log ingestion end-to-end
10. Registrar configuracao no `decisions-log`

## Output
- Cloud logging configurado e centralizado
- Politica de retencao de logs documentada
- Alertas para eventos criticos configurados
- Pipeline de ingestion validado end-to-end

## Quality Gates
- [ ] CloudTrail/Activity Log habilitado em todas as contas
- [ ] VPC Flow Logs configurados em redes criticas
- [ ] Logs centralizados em plataforma de aggregation
- [ ] Retencao conforme requisitos regulatorios
- [ ] Alertas de seguranca criticos configurados
- [ ] Checklist `cloud-logging-and-trails` atendido
- [ ] Checklist `santos-soc-readiness` validado
