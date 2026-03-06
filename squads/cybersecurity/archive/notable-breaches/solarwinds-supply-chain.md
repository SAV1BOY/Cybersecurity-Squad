# SolarWinds Supply Chain Attack (2020)

Analise do ataque de supply chain via SolarWinds Orion que comprometeu milhares de organizacoes.

## O Que Aconteceu

Grupo APT (atribuido ao SVR russo, rastreado como APT29/Cozy Bear) comprometeu
o build system do SolarWinds e inseriu backdoor (SUNBURST) em atualizacoes
legitimas do Orion. Aproximadamente 18.000 organizacoes instalaram a atualizacao
comprometida, com aproximadamente 100 sendo alvos de exploracao ativa.

## Timeline

| Data | Evento |
|------|--------|
| Out 2019 | Atacantes acessam build environment da SolarWinds |
| Fev 2020 | Codigo malicioso (SUNBURST) inserido no Orion build |
| Mar 2020 | Atualizacoes comprometidas distribuidas para clientes |
| Dez 8, 2020 | FireEye descobre breach proprio e investiga |
| Dez 13, 2020 | FireEye publica detalhes sobre SUNBURST/SolarWinds |
| Dez 15, 2020 | Kill switch ativado para dominio C2 |

## Root Cause

1. **Build system comprometido**: CI/CD pipeline sem integridade verificavel
2. **Confianca implicita em vendor**: Updates automaticos sem verificacao adicional
3. **Privilegios excessivos do Orion**: Acesso amplo a rede para monitoramento
4. **Dwell time extremo**: Atacantes ativos por ~14 meses sem deteccao

## Impacto

- Agencias governamentais dos EUA (Treasury, Commerce, DHS)
- Empresas de tecnologia (Microsoft, Intel, Cisco)
- FireEye (red team tools roubadas)

## Licoes Aprendidas

- Supply chain e um vetor critico que requer controles especificos
- Build pipeline integrity (SLSA framework) e essencial
- Zero trust deve se aplicar a software de vendors confiáveis
- Monitoramento de DNS para C2 detection
- Threat hunting proativo para detectar adversarios sofisticados

## Como Detectariamos/Preveniríamos

- SCA e software bill of materials (SBOM) para dependencias
- Network monitoring para DNS beaconing anomalo
- Behavioral analysis de processos de software legitimo
- Segmentacao rigorosa para ferramentas de monitoramento
- Regular threat hunting focado em persistence mechanisms
