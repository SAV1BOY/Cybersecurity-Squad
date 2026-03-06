# Applied Cryptography Reference - Ficha de Referencia

## Metadados
- **Titulo**: Applied Cryptography: Protocols, Algorithms, and Source Code in C
- **Autor**: Bruce Schneier
- **Referencia Complementar**: Crypto Engineering (Ferguson, Schneier, Kohno)
- **Categoria**: Cryptography / Security Fundamentals

## Descricao Geral
Referencia enciclopedica sobre criptografia aplicada. Cobre algoritmos, protocolos
e implementacoes com foco pratico. Complementado por Cryptography Engineering
para abordagens mais modernas.

## Conceitos-Chave
- Symmetric encryption (AES, ChaCha20, block cipher modes)
- Asymmetric encryption (RSA, ECC, key exchange)
- Hash functions e message authentication codes (HMAC)
- Digital signatures e certificate management
- Key management e key derivation functions
- TLS/SSL protocol internals
- Random number generation (CSPRNG)
- Common cryptographic pitfalls e anti-patterns
- Quantum computing impact on cryptography
- Post-quantum cryptography overview

## Por Que Importa para o Squad
Criptografia e o alicerce de quase toda seguranca digital. Erros criptograficos
sao comuns e devastadores. O squad precisa identificar implementacoes frageis
e recomendar alternativas seguras.

## Como o Squad Utiliza
- **Code Review**: identificar erros criptograficos em codigo
- **Architecture Review**: validar uso correto de protocolos
- **Pentest**: explorar falhas criptograficas encontradas
- **Consulting**: recomendar implementacoes seguras
- **Training**: referencia para duvidas criptograficas

## Complementa
- manico-iron-clad-java.md (crypto em Java)
- dowd-art-of-software-security.md (security assessment)
- mcgraw-software-security.md (secure development)

## Nivel de Profundidade
Intermediario a Avancado - requer base matematica para capitulos avancados.

## Notas do Squad
Nao implementar criptografia custom - usar bibliotecas validadas (libsodium,
OpenSSL). O squad deve focar em identificar anti-patterns, nao em criar
algoritmos proprios.
