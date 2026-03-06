# Detection as Code Pattern

Padrao que aplica praticas de engenharia de software a regras de deteccao.

## Principio

Tratar regras de deteccao como codigo: versionadas, testadas, revisadas
por peers e deployadas via CI/CD pipeline automatizado.

## Workflow

```
1. Criar branch para nova deteccao
2. Escrever regra + test cases + documentacao
3. Executar testes automatizados (unit + integration)
4. Code review por peer do detection engineering team
5. Merge to main
6. CI/CD deploya automaticamente para SIEM/EDR
7. Monitorar performance em producao
```

## Estrutura do Repositorio

```
detection-rules/
  rules/
    initial-access/
      brute-force-ssh.yml
      phishing-link-click.yml
    execution/
      suspicious-powershell.yml
    lateral-movement/
      smb-psexec.yml
  tests/
    test_brute_force_ssh.py
    test_suspicious_powershell.py
  lib/
    helpers.py
    mitre_mapping.py
  .github/
    workflows/
      test-and-deploy.yml
  README.md
```

## Formato de Regra (Sigma-like)

```yaml
title: Brute Force SSH Detection
id: DET-042
status: production
description: Detecta multiplas tentativas de login SSH falhadas
author: detection-eng-team
date: 2026-01-15
mitre:
  tactic: Credential Access
  technique: T1110.001
logsource:
  product: linux
  service: sshd
detection:
  condition: failed_login count > 10 within 5m by src_ip
  fields: [src_ip, dest_ip, username, timestamp]
falsepositives:
  - Vulnerability scanners autorizados
level: high
```

## Testes Automatizados

- **Unit tests**: Validar que a logica da regra funciona com dados sinteticos
- **Integration tests**: Executar contra SIEM de teste com logs reais
- **Performance tests**: Garantir que a regra nao degrada performance do SIEM

## Beneficios

- Historico completo de mudancas em regras
- Qualidade garantida via code review e testes
- Rollback facil em caso de problemas
- Colaboracao entre analistas e engenheiros
