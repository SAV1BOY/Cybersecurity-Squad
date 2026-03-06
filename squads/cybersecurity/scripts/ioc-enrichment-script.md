# IOC Enrichment Script

Script para enriquecer Indicators of Compromise com informacoes de multiplas fontes de threat intelligence.

## Descricao

Recebe uma lista de IOCs (IPs, dominios, hashes) e consulta diversas fontes de inteligencia para agregar contexto, facilitando a triagem e investigacao.

## Inputs

- `ioc_list` - Arquivo com lista de IOCs (um por linha) ou IOC individual
- `ioc_type` - Tipo do IOC (ip, domain, hash, url; ou auto para deteccao automatica)
- `sources` - Fontes a consultar (virustotal, abuseipdb, otx, shodan, whois)

## Tipos de IOC Suportados

| Tipo | Formato | Fontes Principais |
|------|---------|-------------------|
| IP Address | IPv4/IPv6 | AbuseIPDB, Shodan, OTX, VirusTotal |
| Domain | FQDN | VirusTotal, WHOIS, OTX, PassiveDNS |
| File Hash | MD5/SHA1/SHA256 | VirusTotal, OTX, MalwareBazaar |
| URL | http(s)://... | VirusTotal, URLhaus, OTX |

## Logica

1. Carregar lista de IOCs e validar formato
2. Detectar tipo de cada IOC automaticamente (se mode auto)
3. Para cada IOC:
   - Consultar cada fonte configurada via API
   - Agregar resultados em formato padronizado
   - Calcular reputation score consolidado
4. Gerar relatorio enriquecido

## Output por IOC

```
IOC: 203.0.113.50
Tipo: IP Address
Reputation: MALICIOUS (high confidence)

AbuseIPDB:
  Reports: 47 | Confidence: 95% | Categories: SSH Brute Force, Web Attack
Shodan:
  Portas: 22, 80, 443 | OS: Linux | Org: Example Hosting
VirusTotal:
  Detections: 12/87 vendors | Last seen: 2026-03-05
OTX:
  Pulses: 3 | Tags: APT29, Cobalt Strike

Historico de campanha: Associado a campanha de phishing detectada em 2026-02
Recomendacao: Bloquear e investigar conexoes no ambiente
```

## Output Consolidado

```
IOC Enrichment Report
Date: 2026-03-06
Total IOCs: 25

Malicious: 8 (32%)
Suspicious: 5 (20%)
Clean: 10 (40%)
Unknown: 2 (8%)
```

## Uso

```
ioc-enrichment --list iocs.txt --type auto --sources virustotal,abuseipdb,otx
```

## Rate Limiting

- Respeitar rate limits de cada API
- Implementar retry com backoff exponencial
- Cachear resultados recentes para evitar consultas duplicadas
