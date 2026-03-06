# Lab Setup Standard - Guia de Configuracao

## Objetivo
Padronizar a configuracao do ambiente de laboratorio do squad para pratica,
treinamento e validacao de ferramentas e tecnicas de seguranca.

## Infraestrutura Base

### Hypervisor
- **Recomendado**: Proxmox VE (open-source) ou VMware Workstation Pro
- **Minimo**: VirtualBox (para setups individuais)
- **Recursos**: 32GB RAM, 500GB SSD, CPU com VT-x/AMD-V
- **Network**: multiplas interfaces para segmentacao

### Redes Virtuais
- **Management Network**: 10.0.0.0/24 (acesso administrativo)
- **Attack Network**: 10.10.0.0/24 (rede de ataque)
- **Target Network**: 10.20.0.0/24 (alvos vulneraveis)
- **Isolated Network**: 10.30.0.0/24 (malware analysis)
- **NAT**: saida controlada para internet quando necessario

## Maquinas Virtuais Essenciais

### Attack Machines
- Kali Linux (latest) - primary attack platform
- Parrot Security OS - alternative attack platform
- Commando VM (Windows) - Windows-based attack platform
- Custom Ubuntu com ferramentas do squad

### Vulnerable Targets
- Metasploitable 2 e 3 - alvos classicos para pratica
- DVWA (Damn Vulnerable Web Application)
- HackTheBox/TryHackMe VPN - desafios online
- VulnHub machines - VMs vulneraveis downloadaveis
- DVNA (Damn Vulnerable Node Application)
- WebGoat / Juice Shop (OWASP)

### Infrastructure Targets
- Windows Server 2019/2022 (Active Directory lab)
- Domain Controller com usuarios e GPOs
- Windows 10/11 workstations joined ao dominio
- Linux servers (Ubuntu/CentOS) com servicos vulneraveis

### Defensive Infrastructure
- Security Onion (NSM platform)
- ELK Stack (SIEM lab)
- TheHive + Cortex (IR platform)
- Wazuh (endpoint detection)

## Setup Automatizado
- Ansible playbooks para provisioning de VMs
- Vagrant files para ambientes reproduziveis
- Terraform para lab em cloud (AWS/Azure)
- Scripts de reset para restaurar estado inicial

## Regras do Lab
1. Lab e ISOLADO da rede de producao - sem excecoes
2. Nao conectar maquinas vulneraveis a internet
3. Documentar todas as modificacoes no ambiente
4. Reset semanal de VMs comprometidas
5. Backups do estado clean de cada VM
6. VPN obrigatoria para acesso remoto ao lab

## Manutencao
- Atualizar attack tools mensalmente
- Adicionar novos alvos trimestralmente
- Revisar segmentacao de rede semestralmente
- Documentar mudancas no wiki do squad

## Notas do Squad
O lab e o espaco mais importante para desenvolvimento de habilidades.
Investir em hardware adequado e manter o ambiente funcional e atualizado.
