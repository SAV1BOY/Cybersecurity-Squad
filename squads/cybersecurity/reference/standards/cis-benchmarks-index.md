# CIS Benchmarks e Controls - Indice de Referencia

## Visao Geral
O Center for Internet Security (CIS) publica benchmarks de hardening e controles
de seguranca baseados em consenso da comunidade. Sao referencias praticas e
acionaveis para configuracao segura de sistemas.

## CIS Controls v8
Framework de 18 controles priorizados por eficacia contra ameacas reais.

### Implementation Groups (IGs)
- **IG1**: controles basicos para todas as organizacoes (baseline essencial)
- **IG2**: controles para organizacoes com complexidade moderada
- **IG3**: controles avancados para ambientes de alto risco

### Controles Prioritarios para o Squad
1. Inventory and Control of Enterprise Assets
2. Inventory and Control of Software Assets
3. Data Protection
4. Secure Configuration of Enterprise Assets and Software
5. Account Management
6. Access Control Management
7. Continuous Vulnerability Management
8. Audit Log Management
9. Email and Web Browser Protections
10. Malware Defenses

## CIS Benchmarks (Hardening Guides)
Guias detalhados de configuracao segura para tecnologias especificas.

### Benchmarks Mais Utilizados pelo Squad
- **Windows Server** 2019/2022 - hardening de servidores
- **Ubuntu/RHEL Linux** - hardening de servidores Linux
- **AWS/Azure/GCP Foundations** - cloud security baseline
- **Kubernetes** - container orchestration security
- **Docker** - container runtime security
- **Microsoft 365** - productivity suite hardening
- **PostgreSQL/MySQL** - database hardening
- **Apache/Nginx** - web server hardening
- **Active Directory** - domain security

## Como o Squad Aplica
- **Hardening Projects**: implementar benchmarks em infraestrutura
- **Compliance Audits**: verificar aderencia a benchmarks
- **Cloud Security**: baseline para ambientes cloud
- **Automation**: scripts de hardening baseados em benchmarks
- **Gap Analysis**: identificar desvios de configuracao

## Ferramentas de Automacao
- CIS-CAT Pro (assessment tool oficial)
- InSpec profiles para CIS benchmarks
- Ansible/Terraform para aplicar benchmarks
- Cloud-native tools (AWS Config, Azure Policy)

## Notas do Squad
Priorizar IG1 como baseline minimo para todos os clientes. Automatizar
verificacao de conformidade com CIS benchmarks usando ferramentas de IaC.
