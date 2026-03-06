# Detection Playbooks

Playbooks para operacoes de deteccao no SOC com procedimentos padronizados.

## Estrutura de Detection Playbook

1. **Alert Name** - Nome descritivo da regra
2. **Data Source** - Log source e campos relevantes
3. **Detection Logic** - Query ou regra em pseudocodigo
4. **Triage Steps** - Procedimento de analise do alerta
5. **True Positive Indicators** - Sinais que confirmam ameaca
6. **False Positive Patterns** - Cenarios conhecidos de FP
7. **Response Actions** - O que fazer quando confirmado
8. **Escalation Criteria** - Quando escalar para tier 2/3

## Exemplo: Brute Force Detection

**Alert:** Multiple Failed Logins Followed by Success
**Data Source:** Authentication logs (AD, SIEM)
**Logic:** `failed_count >= 10 AND success == true WITHIN 30min FROM same source`

**Triage:**
- Verificar se source IP e corporativo ou externo
- Checar se usuario reportou atividade propria
- Analisar geolocation e user-agent do login bem-sucedido
- Verificar acoes pos-login (privilege escalation, data access)

**True Positive:** Login de IP externo nao usual + acoes anomalas pos-login
**False Positive:** Usuario esqueceu senha e tentou multiplas vezes

## Categorias de Playbooks Prioritarias

- Authentication anomalies (brute force, credential stuffing, impossible travel)
- Malware indicators (known IOCs, behavioral patterns)
- Data exfiltration (volume anomalies, unusual destinations)
- Privilege escalation (admin creation, policy changes)
- Lateral movement (pass-the-hash, remote execution)
