# Discovery Layer — Framework Operacional

> Camada de descoberta: mapear tudo que existe, tudo que pode ser atacado, e tudo que precisa ser defendido.

## Objetivo

A Discovery Layer e a fundacao de qualquer operacao de seguranca. Sem saber o que existe, nao ha como proteger, testar ou monitorar. Esta camada produz o inventario real (nao o "oficial") de ativos, fluxos de dados, trust boundaries e superficie de ataque.

## Principios

1. **Descoberta antes de tudo** — Nao teste o que voce nao mapeou
2. **Inventario real > inventario oficial** — O que roda em producao e o que importa
3. **Ativos desconhecidos sao o maior risco** — Shadow IT, APIs esquecidas, subdominios abandonados
4. **Priorizacao por exposicao** — Internet-facing primeiro, depois interno
5. **Repetivel e atualizavel** — Descoberta nao e evento unico, e processo continuo

## Componentes da Descoberta

### 1. Asset Discovery (Inventario de Ativos)
- **Network scanning**: Ranges de IP, portas, servicos
- **DNS enumeration**: Subdominios, registros MX/TXT/CNAME, zone transfers
- **Cloud inventory**: AWS/GCP/Azure accounts, regions, services
- **Application inventory**: Web apps, APIs, microservices, mobile backends
- **Identity inventory**: IdPs, service accounts, federation trusts
- **Data stores**: Databases, object storage, file shares, backups

### 2. Attack Surface Mapping
- **External surface**: O que e visivel da internet (Cartographer + Busterer)
- **Internal surface**: O que e acessivel dentro da rede (Cartographer)
- **Application surface**: Endpoints, parametros, funcionalidades (Dirber + Fuzzer)
- **Identity surface**: Contas, permissoes, delegacoes, trust paths
- **Supply chain surface**: Dependencias, third-party integrations, SaaS

### 3. Data Flow Mapping
- **Fluxos de dados sensiveis**: PII, financeiros, saude, credenciais
- **Trust boundaries**: Onde dados cruzam limites de confianca
- **Encryption points**: Onde dados sao cifrados/decifrados
- **Storage points**: Onde dados descansam (at rest)
- **Access points**: Quem pode acessar cada fluxo

### 4. Trust Boundary Identification
- **Network boundaries**: DMZ, VPC, segments, peering
- **Identity boundaries**: Tenants, domains, federation
- **Application boundaries**: Microservice boundaries, API gateways
- **Data boundaries**: Classification levels, jurisdictions

## Playbook de Descoberta

### Fase 1: Passive Recon (sem tocar no alvo)
```
1. DNS records (whois, dig, nslookup)
2. Certificate transparency logs (crt.sh)
3. Public repositories (GitHub, GitLab — leaks)
4. Search engine dorking (Google, Shodan, Censys)
5. OSINT de infraestrutura (ASN, BGP, IP ranges)
6. Cloud service enumeration (S3 buckets, Azure blobs)
```

### Fase 2: Active Recon (com autorizacao)
```
1. Port scanning (top ports -> full scan)
2. Service identification (versoes, banners)
3. Web crawling (sitemap, robots.txt, links)
4. API endpoint discovery (swagger, graphql introspection)
5. Subdomain brute-force (wordlists curadas)
6. Virtual host enumeration
```

### Fase 3: Inventario e Priorizacao
```
1. Consolidar todos os ativos descobertos
2. Classificar por exposicao (external/internal)
3. Classificar por criticidade (dados sensiveis, funcao de negocio)
4. Identificar owners (quem e responsavel)
5. Mapear lacunas (o que deveria existir mas nao foi encontrado)
6. Produzir mapa visual de superficie
```

## Agentes Envolvidos

| Agente | Papel na Discovery |
|--------|-------------------|
| Cartographer | Mapeamento completo, consolidacao, visualizacao |
| Busterer | Enumeracao rapida, brute-force de subdominios/dirs |
| Dirber | Enumeracao de conteudo web, endpoints, files |
| Peter Kim | Recon estrategico, priorizacao de caminhos de ataque |
| Cyber Chief | Scoping, autorizacao, priorizacao geral |

## Outputs

- `data/registries/asset-registry.md` — Inventario completo
- `trackers/asset-inventory-tracker.md` — Tracker de acompanhamento
- Mapa de superficie de ataque (visual)
- Lista priorizada de alvos para proxima fase

## Quality Gate

Checklist obrigatoria: `asset-inventory-quality.md` + `attack-surface-mapping-quality.md`

## Integracao

- **Alimenta**: Offense Layer, Defense Layer, AppSec Layer, CloudSec Layer
- **Recebe de**: Intake (scope e autorizacao)
- **Atualiza**: A cada mudanca significativa de infraestrutura ou novo engajamento

## Used By

### Tasks (config.yaml routing)
- asset-discovery
- attack-surface-mapping
- asset-scoping
- data-flow-mapping

### Agents
- cartographer
- busterer
- dirber

### Related Checklists
- asset-inventory-quality
- attack-surface-mapping-quality

### Cross-References
- Config routing: `config.yaml`
- Quality gate system: `docs/quality-gate-system.md`
