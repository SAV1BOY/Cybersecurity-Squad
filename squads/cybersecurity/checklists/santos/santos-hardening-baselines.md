# Santos - Hardening Baselines

Checklist para definicao e manutencao de baselines de hardening.

## Definicao de Baselines
- [ ] CIS Benchmarks selecionados para cada tecnologia em uso
- [ ] Benchmark level definido (Level 1 vs Level 2) por ambiente
- [ ] Custom controls adicionais identificados para requisitos internos
- [ ] Baseline aprovado por security e operations teams
- [ ] Baseline versionado e armazenado em repositorio
- [ ] Exceptions process definido para desvios justificados
- [ ] Baseline review schedule definido (semestral/anual)

## Operating System Baselines
- [ ] Windows Server baseline definido (CIS + custom)
- [ ] Windows Workstation baseline definido
- [ ] Linux Server baseline definido (por distribuicao)
- [ ] macOS baseline definido (se aplicavel)
- [ ] Patch management policy integrada ao baseline
- [ ] Local firewall rules padrao definidas
- [ ] Audit policy padrao definida

## Network Device Baselines
- [ ] Router baseline definido (por vendor/model)
- [ ] Switch baseline definido
- [ ] Firewall baseline definido
- [ ] Wireless AP baseline definido
- [ ] Load balancer baseline definido
- [ ] Management access standardizado (SSH, MFA, ACL)
- [ ] Logging padrao definido para cada tipo de device

## Application e Database Baselines
- [ ] Web server baseline definido (Apache, Nginx, IIS)
- [ ] Application server baseline definido
- [ ] Database baseline definido (por engine: MySQL, PostgreSQL, MSSQL)
- [ ] Container runtime baseline definido (Docker, containerd)
- [ ] Kubernetes baseline definido (CIS Kubernetes Benchmark)

## Cloud Baselines
- [ ] AWS baseline definido (CIS AWS Foundations)
- [ ] Azure baseline definido (CIS Azure Foundations)
- [ ] GCP baseline definido (CIS GCP Foundations)
- [ ] IaC templates alinhados com baselines
- [ ] Cloud-native services baseline definido

## Automacao e Compliance
- [ ] Automated scanning tools configurados (CIS-CAT, InSpec, Lynis)
- [ ] Scan schedule definido (weekly/monthly)
- [ ] Compliance dashboard operacional
- [ ] Non-compliance alerting configurado
- [ ] Auto-remediation implementada para controles de baixo risco
- [ ] Golden images criadas a partir dos baselines

## Governanca
- [ ] Baseline ownership definido por tecnologia
- [ ] Change management process para baseline updates
- [ ] Compliance reporting para management (monthly)
- [ ] Deviation register mantido com justificativas
- [ ] Baseline effectiveness medida via vulnerability assessments
- [ ] New technology onboarding inclui baseline definition
