# Defense in Depth Pattern

Padrao de seguranca baseado em multiplas camadas de controles sobrepostos.

## Principio

Nenhum controle unico e suficiente. Implementar camadas independentes de defesa
garante que a falha de um controle nao resulte em comprometimento total.

## Camadas de Defesa

### 1. Perimeter Security
- Firewall, WAF, DDoS protection
- DNS filtering, email gateway
- Rate limiting e geo-blocking

### 2. Network Security
- Network segmentation e micro-segmentation
- IDS/IPS, network monitoring
- Zero trust network access (ZTNA)

### 3. Endpoint Security
- EDR/XDR em todos os endpoints
- Host-based firewall
- Application whitelisting
- Disk encryption

### 4. Application Security
- Input validation e output encoding
- Authentication e authorization robustos
- Secure session management
- SAST, DAST, SCA no pipeline

### 5. Data Security
- Encryption at rest e in transit
- Data loss prevention (DLP)
- Access controls granulares
- Data masking e tokenization

### 6. Identity Security
- Multi-factor authentication
- Privileged access management
- Just-in-time access
- Continuous identity verification

## Exemplo Pratico

Um ataque de SQL Injection seria bloqueado por:
1. WAF (camada perimetro) - bloqueia payloads conhecidos
2. Input validation (camada aplicacao) - rejeita caracteres invalidos
3. Parameterized queries (camada dados) - impede execucao de SQL injetado
4. Least privilege DB user (camada identidade) - limita impacto se explorado
5. Monitoring (camada deteccao) - alerta sobre queries anomalas

## Anti-Pattern

Confiar em uma unica camada (ex: "temos WAF, entao nao precisamos de
input validation") viola o principio e cria single points of failure.
