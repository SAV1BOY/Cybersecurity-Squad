# Incident Taxonomy

Taxonomia para classificacao padronizada de incidentes de seguranca.

## Categorias de Incidente

### 1. Malware
- **Ransomware**: Criptografia de dados com demanda de resgate
- **Trojan**: Malware disfarado de software legitimo
- **Worm**: Malware auto-propagavel
- **Rootkit**: Malware que esconde presenca no sistema
- **Cryptominer**: Uso nao autorizado de recursos para mineracao
- **RAT**: Remote Access Trojan para controle remoto

### 2. Phishing / Social Engineering
- **Spear Phishing**: Email direcionado a individuo especifico
- **Business Email Compromise (BEC)**: Impersonacao de executivo
- **Vishing**: Phishing via telefone
- **Smishing**: Phishing via SMS
- **Pretexting**: Manipulacao com historia fabricada

### 3. Unauthorized Access
- **Account Compromise**: Credenciais validas comprometidas
- **Privilege Escalation**: Obtencao de privilegios indevidos
- **Brute Force**: Tentativas massivas de autenticacao
- **Session Hijacking**: Sequestro de sessao ativa

### 4. Data Breach / Exposure
- **Data Exfiltration**: Extracao intencional de dados
- **Accidental Exposure**: Exposicao nao intencional (ex: S3 publico)
- **Insider Data Theft**: Roubo de dados por insider
- **Physical Data Loss**: Perda de dispositivo com dados

### 5. Denial of Service
- **DDoS**: Ataque distribuido de negacao de servico
- **Application DoS**: Exploracao de logica para indisponibilidade
- **Resource Exhaustion**: Esgotamento intencional de recursos

### 6. Supply Chain
- **Dependency Compromise**: Biblioteca maliciosa em supply chain
- **Vendor Breach**: Comprometimento via fornecedor
- **Update Hijack**: Atualizacao de software comprometida

## Severidade por Categoria

| Categoria | Severidade Tipica | SLA Resposta |
|-----------|-------------------|-------------|
| Ransomware | Critical | Imediato |
| Data Exfiltration | Critical | Imediato |
| Account Compromise | High | < 1 hora |
| Spear Phishing | Medium-High | < 4 horas |
| DDoS | Medium-High | < 1 hora |
| Cryptominer | Medium | < 24 horas |
| Accidental Exposure | Medium | < 4 horas |

## Uso

Classificar cada incidente na categoria mais especifica possivel.
A classificacao correta direciona o playbook de resposta adequado
e garante metricas consistentes para analise de tendencias.
