# Detection Rules Registry

Catalogo de todas as regras de deteccao implementadas no ambiente, incluindo SIEM, EDR e custom detections.

## Schema do Registro

| Rule ID | Name | MITRE ATT&CK | Data Source | Platform | Severity | Status | Author | Last Tested |
|---------|------|--------------|-------------|----------|----------|--------|--------|-------------|
| DET-001 | Brute Force Login Attempts | T1110.001 | Auth Logs | SIEM | High | Active | @soc-team | 2026-02-01 |
| DET-002 | Suspicious PowerShell Execution | T1059.001 | EDR | CrowdStrike | Critical | Active | @detection-eng | 2026-02-15 |
| DET-003 | Lateral Movement via SMB | T1021.002 | Network Logs | SIEM | High | Testing | @detection-eng | 2026-02-20 |
| DET-004 | Exfiltration via DNS Tunneling | T1048.001 | DNS Logs | SIEM | Critical | Draft | @soc-team | - |

## Status Validos

- **Draft**: Regra em desenvolvimento
- **Testing**: Em fase de tuning e validacao
- **Active**: Regra em producao gerando alertas
- **Disabled**: Desativada temporariamente
- **Deprecated**: Substituida ou obsoleta

## Campos de Metadados

Cada regra deve incluir: logica de deteccao, taxa de false positive esperada,
runbook de resposta associado, data de ultima revisao e cobertura MITRE ATT&CK.

## Processo de Lifecycle

1. **Criacao**: Hipotese de deteccao baseada em threat intelligence
2. **Desenvolvimento**: Escrita da query e logica
3. **Testing**: Validacao com dados sinteticos e reais
4. **Tuning**: Ajuste para reduzir false positives
5. **Deploy**: Ativacao em producao
6. **Revisao**: Avaliacao periodica de eficacia

## Cobertura MITRE ATT&CK

Manter mapeamento atualizado entre regras e tecnicas MITRE para identificar gaps
de deteccao. Objetivo minimo: cobertura de 80% das tecnicas mais prevalentes
conforme threat landscape do setor.
