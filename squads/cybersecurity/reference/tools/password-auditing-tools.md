# Password Auditing Tools

## Visao Geral
Ferramentas para auditoria de senhas, cracking de hashes e teste de politicas
de senha. Utilizadas em pentests e assessments de seguranca de credenciais.

## Password Cracking

### Hashcat
- **Tipo**: GPU-accelerated password cracker
- **Uso**: cracking de hashes com alta performance
- **Modos**: dictionary, brute force, rules, combinator, mask
- **Hashes**: suporte a 300+ algoritmos de hash
- **Performance**: ordens de magnitude mais rapido que CPU
- **Dica**: investir em hardware GPU para o squad

### John the Ripper
- **Tipo**: CPU-based password cracker
- **Uso**: cracking versatil com muitos formatos
- **Formatos**: shadow, NTLM, Kerberos, SSH, PDF, ZIP
- **Regras**: sistema de rules extensivo e customizavel
- **Diferencial**: suporte a formatos exoticos

## Credential Testing

### Hydra
- **Tipo**: online password brute forcer
- **Uso**: brute force de servicos de rede
- **Protocolos**: SSH, FTP, HTTP, SMB, RDP, MySQL, e mais
- **Dica**: usar com cautela para evitar lockouts

### CrackMapExec (NetExec)
- **Tipo**: network authentication testing tool
- **Uso**: testar credenciais em massa contra servicos Windows
- **Protocolos**: SMB, WinRM, LDAP, MSSQL, SSH
- **Diferencial**: post-exploitation e lateral movement

### Spray
- **Tipo**: password spraying tool
- **Uso**: testar senhas comuns contra muitos usuarios
- **Alvo**: Active Directory, Office 365, Exchange
- **Dica**: respeitar lockout policies

## Credential Dumping

### Mimikatz
- **Tipo**: Windows credential extraction tool
- **Uso**: extrair senhas, hashes, tickets Kerberos
- **Tecnicas**: sekurlsa, kerberos, lsadump
- **Dica**: uma das ferramentas mais detectadas por EDR

### Secretsdump (Impacket)
- **Tipo**: remote credential dumping
- **Uso**: extrair hashes do SAM, LSA secrets, NTDS.dit
- **Vantagem**: funciona remotamente via SMB/DCOM

## Wordlists e Resources

### SecLists
- **Tipo**: colecao de wordlists para security testing
- **Conteudo**: passwords, usernames, URLs, fuzzing payloads
- **Uso**: fonte padrao de wordlists para o squad

### CeWL (Custom Word List Generator)
- **Tipo**: gerador de wordlists customizadas
- **Uso**: criar wordlists a partir de websites do alvo
- **Dica**: incluir termos em portugues para alvos BR

## Workflow de Password Audit
1. Coletar hashes (NTDS.dit, shadow, application DBs)
2. Identificar tipo de hash
3. Ataque com dictionary + rules (Hashcat)
4. Mask attack para patterns comuns
5. Brute force incremental se necessario
6. Documentar resultados e estatisticas
7. Recomendar melhorias na politica de senhas

## Metricas para Relatorio
- Percentual de senhas crackeadas
- Tempo medio para crack
- Senhas mais comuns encontradas
- Conformidade com politica de senhas
- Recomendacoes de hardening

## Notas do Squad
Manter wordlists customizadas para o contexto brasileiro (nomes comuns,
times de futebol, cidades, datas). Resultados de auditorias devem ser
tratados com extremo cuidado e confidencialidade.
