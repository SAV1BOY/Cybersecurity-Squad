# OWASP MASVS — Mobile Application Security Verification Standard

## Overview

O OWASP Mobile Application Security Verification Standard (MASVS) define requisitos de seguranca para aplicacoes moveis em plataformas iOS e Android. Complementado pelo OWASP Mobile Application Security Testing Guide (MASTG), o MASVS fornece um framework abrangente para avaliar a seguranca de apps moveis em diferentes niveis de rigor. A versao 2.0 reestruturou completamente o padrao, eliminando os niveis L1/L2 em favor de profiles baseados em contexto de risco.

## Core Concepts

### Categorias de Requisitos (MASVS v2.0)

#### MASVS-STORAGE

Requisitos para protecao de dados armazenados no dispositivo:

- Armazenamento seguro de credenciais e tokens utilizando Keychain (iOS) ou Keystore (Android).
- Prevencao de data leakage via backups, logs, clipboard e screenshots.
- Criptografia de dados sensiveis em repouso com algoritmos e key management adequados.
- Limpeza de dados sensiveis da memoria apos uso.

#### MASVS-CRYPTO

Requisitos de criptografia para protecao de dados:

- Uso de algoritmos criptograficos atualizados e aprovados (AES-256, RSA-2048+, SHA-256+).
- Geracao e armazenamento seguro de chaves criptograficas.
- Ausencia de criptografia customizada ou algoritmos deprecados.
- Implementacao correta de random number generation.

#### MASVS-AUTH

Requisitos de autenticacao e gestao de sessoes:

- Autenticacao server-side como controle primario de acesso.
- Biometria e autenticacao local como segundo fator, nunca como unico mecanismo.
- Gestao de sessoes com token rotation e expiracao adequada.
- Step-up authentication para operacoes sensiveis.

#### MASVS-NETWORK

Requisitos de seguranca de comunicacao de rede:

- TLS 1.2+ obrigatorio para toda comunicacao com backends.
- Certificate pinning para conexoes com servidores proprios.
- Validacao de certificados sem bypass ou excecoes de seguranca.
- Protecao contra man-in-the-middle em redes nao confiaveis.

#### MASVS-PLATFORM

Requisitos de interacao segura com a plataforma mobile:

- Uso correto de permissions com principio de minimo privilegio.
- Validacao de input em IPC mechanisms (deep links, intents, URL schemes).
- Protecao contra WebView attacks e JavaScript injection.
- Configuracao segura de exported components.

#### MASVS-CODE

Requisitos de qualidade e seguranca do codigo:

- Protecao contra vulnerabilidades de memoria (buffer overflow, use-after-free).
- Assinatura de codigo e verificacao de integridade do app.
- Uso de compilacao com protecoes ativas (stack canaries, PIE, ARC).
- Remocao de codigo de debug e funcionalidades de teste.

#### MASVS-RESILIENCE

Requisitos de protecao contra reverse engineering e tampering:

- Deteccao de jailbreak e root no dispositivo.
- Anti-tampering mechanisms para verificar integridade do binario.
- Ofuscacao de codigo para dificultar analise estatica.
- Anti-debugging e anti-instrumentation techniques.

### Profiles de Teste

- **Security Testing** — Verificacao padrao de seguranca aplicavel a todos os apps.
- **Defense in Depth** — Controles adicionais para apps que processam dados sensiveis.
- **Resilience** — Protecoes contra reverse engineering para apps com propriedade intelectual critica.

## Practical Application

### Processo de Assessment Mobile

1. Classificar o app por risco de negocio e selecionar profiles aplicaveis.
2. Realizar analise estatica do binario para identificar configuracoes inseguras.
3. Conduzir analise dinamica com proxy interceptador e instrumentacao (Frida).
4. Testar armazenamento local por data leakage em filesystem, logs e backups.
5. Validar comunicacao de rede com TLS inspection e certificate pinning bypass.
6. Testar autenticacao e autorizacao no backend via API testing.
7. Avaliar mecanismos de resiliencia se aplicavel ao profile selecionado.

### Ferramentas de Teste

| Categoria | iOS | Android |
|-----------|-----|---------|
| Static Analysis | MobSF, otool, class-dump | MobSF, jadx, apktool |
| Dynamic Analysis | Frida, Objection | Frida, Objection, Drozer |
| Network | Burp Suite, mitmproxy | Burp Suite, mitmproxy |
| Storage | iExplorer, Keychain-Dumper | adb, SQLite browser |

## Squad Integration

### Aplicacao no Cybersecurity Squad

- O appsec-layer inclui assessment MASVS como requisito para releases de aplicacoes moveis.
- O offense-layer utiliza o MASTG como guia tecnico para pentests mobile.
- O finding-structure-standard mapeia findings mobile para categorias MASVS especificas.
- O owasp-asvs complementa o MASVS com requisitos de backend compartilhados entre web e mobile.
- O security-champion-program inclui modulo especifico de seguranca mobile para equipes de desenvolvimento.
- O retest-method define procedimentos de validacao especificos para remediacao de findings mobile.
- O security-kpi-dashboard rastreia conformidade MASVS por aplicacao mobile e por release.
