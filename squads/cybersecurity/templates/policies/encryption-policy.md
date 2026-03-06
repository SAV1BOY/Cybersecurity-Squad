# Encryption Policy Template

> Politica de criptografia e gerenciamento de chaves.
> Define requisitos para protecao criptografica de dados.

---

## 1. Informacoes do Documento

- **Titulo:** Politica de Criptografia
- **Versao:** [VERSAO]
- **Data de Vigencia:** [DATA]
- **Responsavel:** [NOME_DO_RESPONSAVEL]
- **Aprovado por:** [NOME_DO_APROVADOR]
- **Proxima Revisao:** [DATA_PROXIMA_REVISAO]

## 2. Objetivo

[DESCREVA_O_OBJETIVO_DA_POLITICA_DE_CRIPTOGRAFIA]

## 3. Escopo

- **Aplica-se a:** Todos os dados e comunicacoes da organizacao
- **Sistemas cobertos:** [TODOS / LISTA_ESPECIFICA]
- **Excecoes:** [EXCECOES_COM_APROVACAO_DE]

## 4. Algoritmos e Protocolos Aprovados

### 4.1 Algoritmos Simetricos

| Algoritmo | Tamanho Minimo de Chave | Uso Aprovado | Status |
|-----------|------------------------|--------------|--------|
| AES | 256 bits | Criptografia de dados | Aprovado |
| ChaCha20-Poly1305 | 256 bits | Criptografia de dados | Aprovado |
| [ALGORITMO] | [TAMANHO] | [USO] | [STATUS] |

### 4.2 Algoritmos Assimetricos

| Algoritmo | Tamanho Minimo de Chave | Uso Aprovado | Status |
|-----------|------------------------|--------------|--------|
| RSA | 2048 bits (4096 recomendado) | Assinatura, key exchange | Aprovado |
| ECDSA | P-256 ou superior | Assinatura digital | Aprovado |
| Ed25519 | 256 bits | Assinatura digital | Aprovado |
| [ALGORITMO] | [TAMANHO] | [USO] | [STATUS] |

### 4.3 Hashing

| Algoritmo | Uso Aprovado | Status |
|-----------|--------------|--------|
| SHA-256 / SHA-3 | Integridade, fingerprinting | Aprovado |
| bcrypt / Argon2 | Password hashing | Aprovado |
| [ALGORITMO] | [USO] | [STATUS] |

### 4.4 Algoritmos Proibidos

- MD5 (para qualquer proposito criptografico)
- SHA-1 (para assinaturas digitais)
- DES / 3DES
- RC4
- [ALGORITMO_PROIBIDO]

### 4.5 Protocolos

| Protocolo | Versao Minima | Uso |
|-----------|---------------|-----|
| TLS | 1.2 (1.3 recomendado) | Comunicacao em transito |
| SSH | 2 | Acesso remoto |
| IPsec | [VERSAO] | VPN |
| [PROTOCOLO] | [VERSAO] | [USO] |

## 5. Requisitos por Cenario

### 5.1 Data at Rest (Dados em Repouso)

- Dados confidenciais e restritos: criptografia obrigatoria
- Discos de laptops e endpoints: [BITLOCKER / FILEVAULT / LUKS]
- Bancos de dados: [TDE / COLUMN_LEVEL / APPLICATION_LEVEL]
- Cloud storage: [SSE / CMK / CSE]
- Backups: criptografia obrigatoria com [METODO]

### 5.2 Data in Transit (Dados em Transito)

- TLS obrigatorio para todas as comunicacoes externas
- mTLS para comunicacao entre servicos: [OBRIGATORIO / RECOMENDADO]
- Cipher suites aprovadas: [LISTA_OU_REFERENCIA]
- Certificate pinning: [OBRIGATORIO_PARA / RECOMENDADO]

### 5.3 Data in Use (Dados em Uso)

- [REQUISITOS_ESPECIFICOS_SE_APLICAVEL]

## 6. Gerenciamento de Chaves

### 6.1 Armazenamento

- Chaves armazenadas em: [HSM / KMS / VAULT]
- Proibido armazenar chaves em codigo fonte ou configuracao
- Separacao de chaves por ambiente: [PROD / STAGING / DEV]

### 6.2 Rotacao

| Tipo de Chave | Frequencia de Rotacao |
|---------------|----------------------|
| Chaves de criptografia de dados | [PERIODO] |
| Chaves de API | [PERIODO] |
| Certificados TLS | [PERIODO — ANTES_DA_EXPIRACAO] |
| Chaves de signing | [PERIODO] |
| [TIPO] | [PERIODO] |

### 6.3 Revogacao e Destruicao

- Processo de revogacao: [PROCESSO]
- Destruicao segura de chaves: [METODO]
- Registro de destruicao: [OBRIGATORIO]

## 7. Certificados Digitais

- CA interna: [CA_INTERNA_SE_EXISTENTE]
- CA externa: [CA_EXTERNA_APROVADA]
- Monitoramento de expiracao: [FERRAMENTA]
- Renovacao automatica: [SIM / NAO — PROCESSO]

## 8. Responsabilidades

| Papel | Responsabilidade |
|-------|-----------------|
| Security Team | [RESPONSABILIDADES] |
| DevOps / Platform | [RESPONSABILIDADES] |
| Desenvolvedores | [RESPONSABILIDADES] |
| [PAPEL] | [RESPONSABILIDADES] |

## 9. Violacoes

O descumprimento desta politica pode resultar em [CONSEQUENCIAS].

## 10. Historico de Revisoes

| Versao | Data | Autor | Descricao |
|--------|------|-------|-----------|
| [VERSAO] | [DATA] | [NOME] | [DESCRICAO] |

---

*Template versao 1.0 — Cybersecurity Squad*
