# DFIR (Digital Forensics & Incident Response) Tooling

## Visao Geral
Ferramentas para investigacao forense digital e resposta a incidentes. O squad
utiliza estas ferramentas durante incidentes de seguranca e investigacoes forenses.

## Memory Forensics

### Volatility 3
- **Tipo**: framework de memory forensics
- **Uso**: analise de dumps de memoria RAM
- **Plugins**: process listing, network connections, registry, malware detection
- **OS suportados**: Windows, Linux, macOS
- **Dica**: coletar memoria antes de desligar sistema comprometido

### Rekall
- **Tipo**: memory forensics framework (alternativa)
- **Uso**: analise de memoria com abordagem profile-less
- **Diferencial**: nao requer profiles pre-gerados

## Disk Forensics

### Autopsy / The Sleuth Kit
- **Tipo**: plataforma de forense digital open-source
- **Uso**: analise de imagens de disco, file carving, timeline
- **Modulos**: hash lookup, keyword search, web artifacts
- **Interface**: GUI (Autopsy) e CLI (Sleuth Kit)

### FTK Imager
- **Tipo**: ferramenta de aquisicao forense
- **Uso**: criacao de imagens forenses de discos e memoria
- **Formatos**: E01, dd, AFF
- **Dica**: ferramenta gratuita essencial para aquisicao

### KAPE (Kroll Artifact Parser and Extractor)
- **Tipo**: triage e collection tool
- **Uso**: coleta rapida de artefatos forenses
- **Targets**: artefatos pre-definidos para coleta
- **Modulos**: processamento de artefatos coletados

## Endpoint Detection e Response

### Velociraptor
- **Tipo**: endpoint visibility e collection platform
- **Uso**: threat hunting, IR, coleta de artefatos em escala
- **VQL**: Velociraptor Query Language para queries custom
- **Diferencial**: agente leve, deployment em escala

### GRR Rapid Response
- **Tipo**: incident response framework (Google)
- **Uso**: investigacao remota de endpoints
- **Diferencial**: escala para milhares de endpoints

## Timeline Analysis

### Plaso / Log2Timeline
- **Tipo**: super timeline creation tool
- **Uso**: criar timeline unificada de multiplas fontes
- **Fontes**: logs, registry, filesystem, browser history
- **Output**: CSV, Elasticsearch, SQLite

### Timesketch
- **Tipo**: collaborative timeline analysis (Google)
- **Uso**: analise colaborativa de timelines forenses
- **Integracao**: Plaso output direto

## Network Forensics

### Wireshark / tshark
- **Tipo**: packet analyzer
- **Uso**: analise de capturas de trafego de rede

### Zeek (Bro)
- **Tipo**: network security monitor
- **Uso**: gerar logs estruturados de trafego de rede

## Malware Analysis

### YARA
- **Tipo**: pattern matching para malware
- **Uso**: criar regras para identificar malware
- **Integracao**: praticamente todas as ferramentas DFIR

### Cuckoo Sandbox / CAPE
- **Tipo**: automated malware analysis sandbox
- **Uso**: detonar e analisar malware em ambiente isolado

## Kit Essencial do Squad para IR
1. FTK Imager (aquisicao)
2. KAPE (triage e collection)
3. Volatility 3 (memory analysis)
4. Autopsy (disk analysis)
5. Plaso + Timesketch (timeline)
6. Velociraptor (endpoint collection em escala)

## Notas do Squad
Manter go-bags com ferramentas pre-configuradas em USB bootavel.
Praticar procedimentos de coleta regularmente para manter proficiencia.
