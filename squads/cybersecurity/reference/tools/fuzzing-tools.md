# Fuzzing Tools

## Visao Geral
Ferramentas de fuzzing para descoberta de vulnerabilidades atraves de input
automatizado. O squad utiliza fuzzing em testes de aplicacoes, APIs e protocolos.

## Web Application Fuzzing

### ffuf (Fuzz Faster U Fool)
- **Tipo**: fast web fuzzer
- **Uso**: directory brute force, parameter fuzzing, virtual host discovery
- **Performance**: extremamente rapido e flexivel
- **Filtros**: por status code, tamanho, palavras, linhas
- **Dica**: ferramenta padrao do squad para fuzzing web

### Burp Intruder
- **Tipo**: web fuzzer integrado ao Burp Suite
- **Uso**: parameter fuzzing, brute force, token analysis
- **Modos**: Sniper, Battering Ram, Pitchfork, Cluster Bomb
- **Dica**: versao Pro necessaria para velocidade adequada

### wfuzz
- **Tipo**: web application fuzzer
- **Uso**: fuzzing de parametros, headers, cookies
- **Filtros**: flexiveis por multiplos criterios

## API Fuzzing

### Postman + Newman
- **Tipo**: API testing platform
- **Uso**: testes automatizados de APIs
- **Collection Runner**: execucao automatizada de testes

### RESTler
- **Tipo**: stateful REST API fuzzer (Microsoft)
- **Uso**: fuzzing inteligente de APIs REST
- **Diferencial**: entende dependencias entre endpoints

### APIFuzzer
- **Tipo**: API fuzzer baseado em OpenAPI spec
- **Uso**: gerar inputs de fuzz a partir de API spec

## Binary/Protocol Fuzzing

### AFL++ (American Fuzzy Lop Plus Plus)
- **Tipo**: coverage-guided fuzzer
- **Uso**: fuzzing de binarios e bibliotecas
- **Feedback**: instrumentacao para maximizar cobertura
- **Diferencial**: mais eficiente que fuzzing cego

### libFuzzer
- **Tipo**: in-process fuzzer (LLVM)
- **Uso**: fuzzing de funcoes C/C++ individuais
- **Integracao**: parte do LLVM/Clang toolchain

### Boofuzz
- **Tipo**: network protocol fuzzer
- **Uso**: fuzzing de protocolos de rede custom
- **Herdeiro**: sucessor do Sulley fuzzer
- **Uso**: encontrar bugs em implementacoes de protocolos

## Mutation e Generation

### Radamsa
- **Tipo**: general-purpose test case mutator
- **Uso**: gerar inputs mutados a partir de amostras validas
- **Dica**: facil de integrar em pipelines de teste

### Peach Fuzzer
- **Tipo**: smart fuzzing platform
- **Uso**: fuzzing baseado em modelos de protocolo
- **Pit files**: descricoes de formato para geracao inteligente

## Wordlists para Fuzzing
- **SecLists/Fuzzing**: payloads para web fuzzing
- **FuzzDB**: patterns de ataque e discovery
- **PayloadsAllTheThings**: payloads organizados por tipo

## Workflow de Fuzzing do Squad
1. Identificar superficie de ataque (inputs, parametros, endpoints)
2. Selecionar ferramenta adequada ao tipo de target
3. Preparar corpus inicial e wordlists relevantes
4. Executar fuzzing com monitoramento de crashes/erros
5. Triagem de resultados (crash analysis, deduplication)
6. Validar e reproduzir findings
7. Documentar e reportar vulnerabilidades confirmadas

## Notas do Squad
Fuzzing em producao requer cuidado extremo. Preferir ambientes de staging
ou lab. Monitorar impacto em performance durante testes.
