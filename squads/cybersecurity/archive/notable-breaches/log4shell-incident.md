# Log4Shell Incident (2021)

Analise da vulnerabilidade Log4Shell (CVE-2021-44228) e seu impacto global.

## O Que Aconteceu

Uma vulnerabilidade critica de remote code execution foi descoberta no Apache
Log4j 2, uma biblioteca de logging Java extremamente difundida. A falha
permitia execucao remota de codigo via JNDI injection em qualquer input
que fosse logado pela biblioteca.

## Timeline

| Data | Evento |
|------|--------|
| Nov 24, 2021 | Alibaba Cloud reporta vulnerabilidade a Apache |
| Dez 1, 2021 | Primeiras exploracoes detectadas in the wild |
| Dez 9, 2021 | PoC publicado no GitHub |
| Dez 10, 2021 | Apache lanca Log4j 2.15.0 com fix parcial |
| Dez 13, 2021 | CVE-2021-45046 - bypass do fix original |
| Dez 14, 2021 | Log4j 2.16.0 lancado |
| Dez 17, 2021 | Log4j 2.17.0 lancado (fix final) |

## Root Cause

1. **Feature perigosa**: JNDI lookup habilitado por default em input do usuario
2. **Ubiquidade da biblioteca**: Log4j presente em milhoes de aplicacoes
3. **Transitive dependency**: Muitas apps incluiam Log4j indiretamente
4. **Dificuldade de inventario**: Organizacoes nao sabiam onde tinham Log4j

## Impacto

- CVSS 10.0 - score maximo possivel
- Estimativa de 3 bilhoes de dispositivos afetados
- Explorada por grupos de ransomware, cryptominers e APTs
- Semanas de esforco de remediacao para maioria das organizacoes

## Licoes Aprendidas

- Software Bill of Materials (SBOM) e essencial para saber o que voce tem
- Dependency scanning (SCA) deve cobrir transitive dependencies
- WAF rules para virtual patching enquanto fix definitivo e aplicado
- Resposta a vulnerabilidades criticas requer processo de emergencia
- Open-source critical dependencies precisam de mais suporte e auditoria
- Logging libraries nao devem processar input nao sanitizado

## Como Detectariamos/Preveniríamos

- SCA continuo com alertas para CVEs criticas em dependencias
- WAF com regras para JNDI injection patterns
- Network monitoring para conexoes LDAP/RMI outbound anomalas
- SBOM atualizado para identificacao rapida de componentes afetados
- Egress filtering para bloquear conexoes outbound nao autorizadas
- Runtime protection (RASP) para detectar exploitation attempts
